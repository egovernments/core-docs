# Monitoring

There are many monitoring tools out there. Before choosing what we would work with on our clients Clusters, we had to take many things into consideration. We use Prometheus and Grafana for Monitoring of our and our client’s clusters.

![](https://miro.medium.com/max/1400/0\*tbNYcUWT5XdWoVBO.png)

## Introduction <a href="#c581" id="c581"></a>

Monitoring is an important pillar of DevOps best practices. This gives you important information about the performance and status of your platform. This is even more true in distributed environments such as Kubernetes and microservices.

One of Kubernetes’ great strengths is its ability to extend its services and applications. When you reach thousands of applications, it’s impractical to manually monitor or use scripts. You need to adopt a scalable surveillance system! This is where Prometheus and Grafana come in.

Prometheus makes it possible to collect, store, and use platform metrics. Grafana, on the other hand, connects to Prometheus, allowing you to create beautiful dashboards and charts.

Today we’ll talk about what Prometheus is and the best way to deploy it to Kubernetes, with the operator. We will see how to set up a monitoring platform using Prometheus and Grafana.

This tutorial provides a good starting point for observability and goes a step further!

### Prometheus <a href="#f4d6" id="f4d6"></a>

Prometheus is a free open source event monitoring and notification application developed on SoundCloud in 2012. Since then, many companies and organizations have adopted and contributed to them.\
In 2016, the Cloud Native Computing Foundation (CNCF) launched the Prometheus project shortly after Kubernetes

The timeline below shows the development of the Prometheus project.

![](https://miro.medium.com/max/1284/0\*RQlhSVCUq4DmNDkH.png)

## Concepts <a href="#169d" id="169d"></a>

Prometheus is considered Kubernetes’ default monitoring solution and was inspired by Google’s [Borgman](https://static.googleusercontent.com/media/research.google.com/en/pubs/archive/43438.pdf). Use HTTP pull requests to collect metrics from your application and infrastructure. It’s targets are discovered via service discovery or static configuration. Time series push is supported through the intermediate gateway.

![](https://miro.medium.com/max/1400/0\*L\_ibDR\_yo4dkASyn.png)

```
Metrics exposed by a Prometheus target has the following format: <metric name>{<label name>=<label value>, ...}
```

Prometheus records real-time metrics in a time series database (TSDB). It provides a dimensional data model, ease of use, and scalable data collection. It also provides PromQL, a flexible query language to use this dimensionality.

![](https://miro.medium.com/max/1400/0\*yW\_QRSkS6px7wjZc.png)

The above architecture diagram shows that Prometheus is a multi-component monitoring system. The following parts are built into the Prometheus deployment:

* The Prometheus server scrapes and stores time series data. It also provides a user interface for querying metrics.
* The [Client libraries](https://prometheus.io/docs/instrumenting/clientlibs/) are used for instrumenting application code.
* [Pushgateway ](https://prometheus.io/docs/instrumenting/exporters/)supports collecting metrics from short-lived jobs.
* Prometheus also has a service [exporter](https://github.com/prometheus/alertmanager) for services that do not directly instrument metrics.
* The Alertmanager takes care of real-time alerts based on triggers

## Why Choose The Prometheus Operator? <a href="#aa28" id="aa28"></a>

Kubernetes provides many objects (pods, deploys, services, ingress, etc.) for deploying applications.\
Kubernetes allows you to create custom resources via custom resource definitions (CRDs).

The CRD object implements the final application behavior. This improves maintainability and reduces deployment effort. When using the [Prometheus operator](https://github.com/prometheus-operator/prometheus-operator), each component of the architecture is taken from the CRD. This makes Prometheus setup easier than traditional installations.

Prometheus Classic installation requires a server configuration update to add new metric endpoints. This allows you to register a new endpoint as a target for collecting metrics. Prometheus operators use monitor objects ([PodMonitor](https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#podmonitor), [ServiceMonitor](https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#servicemonitor)) to dynamically discover endpoints and scrape metrics.

```
Prometheus Operator saves you time in installing and maintaining Prometheus. Provides monitoring objects for dynamically collecting metrics without updating the Prometheus configuration.
```

## Deploying Prometheus With The Operator <a href="#718c" id="718c"></a>

kube-prometheus-stack is a series of Kubernetes manifests, Grafana dashboards, and Prometheus rules. Make use of Prometheus using the operator to provide easy-to-use end-to-end monitoring of Kubernetes clusters.

[**Github Link**](https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack)

This collection is available and can be deployed using a Helm Chart. You can deploy your monitor stack from a single command line-first time with Helm? Check out this [article](https://medium.com/@apotitech/k8s-quickstart-helm-3667d58e1f29) for a helm tutorial.

## Installing Helm <a href="#ab21" id="ab21"></a>

```
$ brew install helm
```

Not using Mac?

```
Take a look at this documentation, to find the appropriate setup for you: https://helm.sh/docs/intro/install/#through-package-managers
```

## Creating the dedicated monitoring namespace <a href="#6a56" id="6a56"></a>

In Kubernetes, _namespaces_ provide a mechanism for isolating groups of resources within a single cluster. We create a namespace named _monitoring_ to prepare the new deployment:

```
$ kubectl create namespace monitoring
```

## Installing kube-prometheus-stack with Helm <a href="#f728" id="f728"></a>

Add the Prometheus chart repository and update the local cache:

```
$ helm repo add prometheus-community https://prometheus-community.github.io/helm-charts$ helm repo update
```

Deploy the _kube-stack-prometheus_ chart in the namespace monitoring with Helm:

```
$ helm upgrade --namespace monitoring --install kube-stack-prometheus prometheus-community/kube-prometheus-stack --set prometheus-node-exporter.hostRootFsMount.enabled=false
```

`hostRootFsMount.enabled` is to be set to `false` to work on Docker Desktop on Macbook.

Now, CRDs are installed in the namespace. You can verify with the following kubectl command:

```
$ kubectl get -n monitoring crds                                                           NAME                                        CREATED ATalertmanagerconfigs.monitoring.coreos.com   2022-03-15T10:54:41Zalertmanagers.monitoring.coreos.com         2022-03-15T10:54:42Zpodmonitors.monitoring.coreos.com           2022-03-15T10:54:42Zprobes.monitoring.coreos.com                2022-03-15T10:54:42Zprometheuses.monitoring.coreos.com          2022-03-15T10:54:42Zprometheusrules.monitoring.coreos.com       2022-03-15T10:54:42Zservicemonitors.monitoring.coreos.com       2022-03-15T10:54:42Zthanosrulers.monitoring.coreos.com          2022-03-15T10:54:42Z
```

Here is what we have running now in the namespace:

The chart has installed Prometheus components and Operator, Grafana — and the following exporters:

* [prometheus-node-exporter](https://github.com/prometheus/node\_exporter) exposes hardware and OS metrics
* [kube-state-metrics](https://github.com/kubernetes/kube-state-metrics) listens to the Kubernetes API server and generates metrics about the state of the objects

Our monitoring stack with Prometheus and Grafana is up and ready!

## Connecting To Prometheus Web Interface <a href="#4aae" id="4aae"></a>

The Prometheus web UI is accessible through port-forward with this command:

```
$ kubectl port-forward --namespace monitoring svc/kube-stack-prometheus-kube-prometheus 9090:9090
```

Opening a browser tab on [http://localhost:9090](http://localhost:9090/) shows the Prometheus web UI. We can retrieve the metrics collected from exporters:

![](https://miro.medium.com/max/1400/0\*zd8JqLK14jW28Gk4.png)

Going to the _“Status>Targets”_ and you can see all the metric endpoints discovered by the Prometheus server:

![](https://miro.medium.com/max/1400/0\*RlcWdsmSOKXqWEq3.png)

### Connecting To Grafana <a href="#58fa" id="58fa"></a>

The credentials to connect to the Grafana web interface are stored in a Kubernetes Secret and encoded in base64. We retrieve the username/password couple with these two commands:

```
$ kubectl get secret --namespace monitoring kube-stack-prometheus-grafana -o jsonpath='{.data.admin-user}' | base64 -d$ kubectl get secret --namespace monitoring kube-stack-prometheus-grafana -o jsonpath='{.data.admin-password}' | base64 -d
```

We create the port-forward to Grafana with the following command:

```
$ kubectl port-forward --namespace monitoring svc/kube-stack-prometheus-grafana 8080:80
```

Open your browser and go to [http://localhost:8080](http://localhost:8080/) and fill in previous credentials:

![](https://miro.medium.com/max/1334/0\*GzWIwpCuaKdyyLRT.png)

The kube-stack-prometheus deployment has provisioned Grafana dashboards:

![](https://miro.medium.com/max/1400/0\*s2fJ46FWAhY38sq-.png)

Here we can see one of them showing compute resources of Kubernetes pods:

![](https://miro.medium.com/max/1400/0\*4Px0EJ2kFoKalkmJ.png)

That’s all folks. Today, we looked at installing Grafana and Prometheus on our K8s Cluster.
