# Tracing

## Pre-reads

{% content-ref url="../../../focus-areas/devops/14.-telemetry.md" %}
[14.-telemetry.md](../../../focus-areas/devops/14.-telemetry.md)
{% endcontent-ref %}

This doc covers the steps on how to deploy an **OpenTelemetry** collector on Kubernetes. We will then use an OTEL instrumented (Go) **application** provided by OpenTelemetry to send traces to the **Collector**. From there, we will bring the trace data to a **Jaeger** **collector**. Finally, the traces will be visualised using the **Jaeger** **UI**.

This image shows the flow between the **application**, OpenTelemetry **collector** and **Jaeger**.

![](https://miro.medium.com/max/1400/1\*8wbA6DvV0jepbkNbsr8yag.png)

> This OpenTelemetry [repository](https://github.com/open-telemetry/opentelemetry-go/tree/main/example/otel-collector) provides a complete demo on how you can deploy OpenTelemetry on Kubernetes, **we can use this as a starting point.**

## **Pre-requisites**

To start off, we need a **Kubernetes** cluster you can use any of your existing Kubernetes clusters that has got the apx 2vCPUs, 4GB RAM, and 100GB Storage.&#x20;

### Local Kubernetes Cluster Setup &#x20;

Skip this in case you have the existing cluster.

In case, you don't have the ready Kubernetes but you have a good local machine with at least 4GB RAM left, you can use a local instance of [Kind](https://kind.sigs.k8s.io/). The [application](https://github.com/open-telemetry/opentelemetry-go/blob/main/example/otel-collector/main.go) will access this Kubernetes cluster through a NodePort (on port 30080). So make sure this port is free.

```
conn, err := grpc.DialContext(ctx, "localhost:30080", grpc.WithTransportCredentials(insecure.NewCredentials()), grpc.WithBlock())
```

To use **NodePort** with **Kind**, we need to first enable it.

> [_Extra port mappings_](https://kind.sigs.k8s.io/docs/user/configuration/#extra-port-mappings) _can be used to port forward to the kind nodes. This is a cross-platform option to get traffic into your kind cluster._

`vim kind-config.yaml`

```
kind: ClusterapiVersion: kind.x-k8s.io/v1alpha4nodes:- role: control-plane  # port forward 30080 on the host to 30080 on this node  extraPortMappings:  - containerPort: 30080    hostPort: 30080- role: worker
```

Create the cluster with: `kind create cluster --config kind-config.yaml`

```
Creating cluster "kind" ... ✓ Ensuring node image (kindest/node:v1.24.0) 🖼 ✓ Preparing nodes 📦 📦 ✓ Writing configuration 📜 ✓ Starting control-plane 🕹️ ✓ Installing CNI 🔌 ✓ Installing StorageClass 💾 ✓ Joining worker nodes 🚜Set kubectl context to "kind-kind"You can now use your cluster with:kubectl cluster-info --context kind-kindThanks for using kind! 😊
```

Once our Kubernetes cluster is up, we can start deploying **Jaeger**.

## What is Jaeger? <a href="#309b" id="309b"></a>

[Jaeger](https://www.jaegertracing.io/) is an open-source distributed tracing system for tracing transactions between distributed services. It’s used for monitoring and troubleshooting complex [microservices](https://microservices.io/) environments. By doing this, we can view traces and analyse the application’s behaviour.

### Why do we need it? <a href="#6302" id="6302"></a>

Using a tracing system (like Jaeger) is especially important in [microservices](https://microservices.io/) environments since they are considered a lot more difficult to debug than a single **monolithic** application.

### Problems that [Jaeger](https://www.jaegertracing.io/) addresses? <a href="#f91d" id="f91d"></a>

* Distributed tracing monitoring
* Performance and latency optimisation
* Root cause analysis
* Service dependency analysis

## Deploy Jaeger <a href="#c0dc" id="c0dc"></a>

To deploy Jaeger on the Kubernetes cluster, we can make use of the [Jaeger operator](https://www.jaegertracing.io/docs/1.36/operator/).

> Operators are pieces of software that ease the operational complexity of running another piece of software.

## Deploy Jaeger Operator <a href="#4cf9" id="4cf9"></a>

You first install the Jaeger Operator on Kubernetes. This operator will then watch for new Jaeger custom resources (CR).

There are different ways of installing the **Jaeger Operator** on Kubernetes:

* using **Helm**
* using **Deployment** files

> Before you start, pay attention to the [Prerequisite](https://www.jaegertracing.io/docs/1.36/operator/#prerequisite) section.
>
> Since version 1.31 the Jaeger Operator uses webhooks to validate Jaeger custom resources (CRs). This requires an installed version of the cert-manager.

## Installing Cert-Manager <a href="#3e08" id="3e08"></a>

[_**cert-manager**_](https://cert-manager.io/) _is a powerful and extensible X.509 certificate controller for Kubernetes and OpenShift workloads. It will obtain certificates from a variety of Issuers, both popular public Issuers as well as private Issuers, and ensure the certificates are valid and up-to-date, and will attempt to renew certificates at a configured time before expiry._

Installation of **cert-manager** of is very simple, just run:

```
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.9.1/cert-manager.yaml
```

> By default, **cert-manager** will be installed into the cert-manager namespace.

You can verify the installation by following the instructions [here](https://cert-manager.io/docs/installation/verify/)

With **cert-manager** installed, let’s continue with the deployment of **Jaeger**

## Installing Jaeger Operator Using Helm <a href="#13b8" id="13b8"></a>

Jump over to [Artifact Hub](https://artifacthub.io/packages/helm/jaegertracing/jaeger-operator) and search for jaeger-operator

Add the Jaeger Tracing Helm repository:

`helm repo add jaegertracing` [`https://jaegertracing.github.io/helm-charts`](https://jaegertracing.github.io/helm-charts)

To install the chart with the release name `my-release` (in the default namespace)

```
helm install my-release jaegertracing/jaeger-operator
```

You can also install a specific version of the helm chart:

```
helm install my-release jaegertracing/jaeger-operator --version 2.25.0
```

Verify that it’s installed on Kubernetes:

`helm list -A`

> You can also deploy the Jaeger operator using **deployment files**.
>
> `kubectl create -f https://github.com/jaegertracing/jaeger-operator/releases/download/v1.36.0/jaeger-operator.yaml`

At this point, there should be a **jaeger-operator** deployment available.

`kubectl get deployment my-jaeger-operator`

```
NAME                 READY   UP-TO-DATE   AVAILABLE   AGEmy-jaeger-operator   1/1     1            1           2m58s
```

The operator is now ready to create Jaeger instances.

## Deploy Jaeger All-in-One <a href="#abf4" id="abf4"></a>

The **operator** that we just installed doesn’t do anything itself, it just means that we can create **jaeger** resources/instances that we want the jaeger operator to manage.

The simplest possible way to create a Jaeger instance is by deploying the **All-in-one** **strategy**, which installs the `all-in-one` image, and includes the **agents**, **collector**, **query** and the J**aeger UI** in a single pod using in-memory storage.

Create a yaml file like the following. The name of the Jaeger instance will be `simplest`

`vim simplest.yaml`

```
apiVersion: jaegertracing.io/v1kind: Jaegermetadata:  name: simplest
```

`kubectl apply -f simplest.yaml`

After a little while, a new in-memory all-in-one instance of Jaeger will be available, suitable for quick demos and development purposes.

When the Jaeger instance is up and running, we can check the **pods** and **services**.

`kubectl get pods`

```
NAME                     READY STATUS    RESTARTS   AGEsimplest-656d7cf5c8-lff7b 1/1  Running   0          3m55s
```

`kubectl get services`

To get the pod name, query for the pods belonging to the simplest Jaeger instance:

![](https://miro.medium.com/max/1400/1\*sA3Xf7l\_o77s0poLNWvWAg.png)

Query the logs from the pod:

`kubectl logs -l app.kubernetes.io/instance=simplest`

```
{"level":"info","ts":1660155049.86027,"caller":"channelz/logging.go:50","msg":"[core]Channel Connectivity change to READY","system":"grpc","grpc_log":true}{"level":"info","ts":1660155049.8612773,"caller":"grpc/builder.go:120","msg":"Agent collector connection state change","dialTarget":":14250","status":"READY"}{"level":"info","ts":1660155049.8617437,"caller":"app/server.go:241","msg":"Starting HTTP server","port":16686,"addr":":16686"}{"level":"info","ts":1660155049.8621716,"caller":"app/server.go:260","msg":"Starting GRPC server","port":16685,"addr":":16685"}
```

### Let’s open the Jaeger UI <a href="#ad0c" id="ad0c"></a>

Use port-forwarding to access the [Jaeger UI](http://127.0.0.1:16686/search)

`kubectl port-forward svc/simplest-query 16686:16686`

```
Forwarding from 127.0.0.1:16686 -> 16686Forwarding from [::1]:16686 -> 16686
```

Jaeger UI

![](https://miro.medium.com/max/1400/1\*ZaBDx\_6zL8NtpCfazTrwZA.png)

## Deploy Open Telemetry Collector <a href="#eaf0" id="eaf0"></a>

To deploy the OpenTelemetry collector, we will use this [otel-collector.yaml](https://github.com/open-telemetry/opentelemetry-go/blob/main/example/otel-collector/k8s/otel-collector.yaml) file as a starting point. The yaml file consists of a **ConfigMap**, **Service** and a **Deployment**.

`vim otel-collector.yaml`

Make sure to change the name of the **jaeger collector** (exporter) to match the one we deployed above. In our case, that would be:

```
exporters:      jaeger:        endpoint: "simplest-collector.default.svc.cluster.local:14250"
```

Also, pay attention to [**receivers**](https://github.com/open-telemetry/opentelemetry-go/tree/main/example/otel-collector). This part creates the receiver on the Collector side and opens up the port `4317` for receiving traces, which enables the application to send data to the OpenTelemetry Collector.

```
...  otel-collector-config: |    receivers:      otlp:        protocols:          grpc:            endpoint: "0.0.0.0:4317"...
```

Apply the file with: `kubectl apply -f otel-collector.yaml`

```
configmap/otel-collector-conf createdservice/otel-collector createddeployment.apps/otel-collector created
```

Verify that the OpenTelemetry Collector is up and running.

`kubectl get deployment`

`kubectl logs deployment/otel-collector`

```
"Everything is ready. Begin running and processing data."
```

## Run Application <a href="#fe54" id="fe54"></a>

Time to send some trace data to our OpenTelemetry collector.

> _Remember, that the application access the Kubernetes cluster through a NodePort on port 30080. The Kubernetes service will bind the `4317` port used to access the OTLP receiver to port `30080` on the Kubernetes node._
>
> _By doing so, it makes it possible for us to access the Collector by using the static address `<node-ip>:30080`. In case you are running a local cluster, this will be `localhost:30080`._ [_Source_](https://github.com/open-telemetry/opentelemetry-go/tree/main/example/otel-collector)

This [repository](https://github.com/open-telemetry/opentelemetry-go/blob/main/example/otel-collector/main.go) contains an (SDK) instrumented application written in **Go**, that simulates an application.

`go run main.go`

```
2022/08/10 20:31:37 Waiting for connection...2022/08/10 20:31:37 Doing really hard work (1 / 10)2022/08/10 20:31:38 Doing really hard work (2 / 10)2022/08/10 20:31:39 Doing really hard work (3 / 10)2022/08/10 20:31:40 Doing really hard work (4 / 10)2022/08/10 20:31:41 Doing really hard work (5 / 10)2022/08/10 20:31:42 Doing really hard work (6 / 10)2022/08/10 20:31:43 Doing really hard work (7 / 10)2022/08/10 20:31:44 Doing really hard work (8 / 10)2022/08/10 20:31:45 Doing really hard work (9 / 10)2022/08/10 20:31:46 Doing really hard work (10 / 10)2022/08/10 20:31:47 Done!
```

## Viewing the data <a href="#611f" id="611f"></a>

Let’s check out the telemetry data generated by our sample application

Again, we can use port-forwarding to access Jaeger UI.

```
kubectl port-forward svc/simplest-query 16686:16686
```

Open the web-browser and go to [http://127.0.0.1:16686/](http://127.0.0.1:16686/)

Under Service select **test-service** to view the generated traces.

![](https://miro.medium.com/max/1400/1\*FrgRm1lvFZz6OzT-smeoIw.png)![](https://miro.medium.com/max/1400/1\*YijRHBoe4BpoFCHZA0RZ5A.png)

The **service name** is specified in the `main.go` [file](https://github.com/open-telemetry/opentelemetry-go/blob/main/example/otel-collector/main.go).

```
res, err := resource.New(ctx,  resource.WithAttributes(   // the service name used to display traces in backends   semconv.ServiceNameKey.String("test-service"),  ),
```

The [application](https://github.com/open-telemetry/opentelemetry-go/blob/main/example/otel-collector/main.go) will access this Kubernetes cluster through a NodePort (on port 30080). The **URL** is specified here:

```
conn, err := grpc.DialContext(ctx, "localhost:30080", grpc.WithTransportCredentials(insecure.NewCredentials()), grpc.WithBlock()) if err != nil {  return nil, fmt.Errorf("failed to create gRPC connection to collector: %w", err) }
```

Done

This document has covered how we deploy an **OpenTelemetry** collector on **Kubernetes**. Then we sent trace data to this collector using an Otel **SDK** instrumented **application** written in Go. From there, the traces were sent to a Jaeger collector and visualised in J**aeger UI**.



[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
