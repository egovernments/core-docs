---
description: >-
  In this tutorial, we will go through the step by step process of setup central
  dashboard Monitoring
---

# Central  Monitoring Dashboard Setup

## Pre-reads

[https://github.com/kubecost/cost-analyzer-helm-chart#kubecost-helm-chart](https://github.com/kubecost/cost-analyzer-helm-chart#kubecost-helm-chart)\
[https://prometheus.io/docs/introduction/overview/](https://prometheus.io/docs/introduction/overview/)\
[https://grafana.com/docs/](https://grafana.com/docs/)\
\


## Pre-requisites

* DIGIT uses [golang](https://golang.org/doc/install#download) (required v1.13.3) automated scripts to deploy the builds onto Kubernetes - [Linux](https://golang.org/dl/go1.13.3.linux-amd64.tar.gz) or [Windows](https://golang.org/dl/go1.13.3.windows-amd64.msi) or [Mac](https://golang.org/dl/go1.13.3.darwin-amd64.pkg)
* All DIGIT services are packaged using helm charts[ ![](https://helm.sh/img/favicon-152.png)Installing Helm](https://helm.sh/docs/intro/install/)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) is a CLI to connect to the kubernetes cluster from your machine
* [Install Visualstudio](https://code.visualstudio.com/download) IDE Code for better code/configuration editing capabilities
* Git
* cost-analyzer - [cost-analyzer](https://github.com/egovernments/DIGIT-DevOps/tree/master/deploy-as-code/helm/charts/backbone-services/cost-analyzer)  must be deployed on the client side&#x20;
* Prometheus-operator - [prometheus](https://github.com/egovernments/DIGIT-DevOps/tree/master/deploy-as-code/helm/charts/backbone-services/prometheus-operator) must be deployed on the client side&#x20;
* prometheus-kafka-exporter (A Prometheus exporter acts as a proxy between such an applications and the Prometheus server) - [prometheus-kafka-exporter](https://github.com/egovernments/DIGIT-DevOps/tree/master/deploy-as-code/helm/charts/backbone-services/prometheus-kafka-exporter) must be deployed on the client side&#x20;

### Step 1: Install the Prometheus Operator on each client cluster

{% embed url="https://core.digit.org/guides/operations-guide/observability/egov-monitoring-and-alerting-setup" %}

### Step 2: Exposes the prometheus Operator&#x20;

exposes the  prometheus Operator using nginx-ingress rule in each client cluster. This makes it easy to access Prometheus metrics in central-dashboard clusters

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  annotations:
    certmanager.k8s.io/cluster-issuer: letsencrypt-prod  //By using this annotation, a certificate will be issued
  labels:
    app: prometheus-operator
  name: prometheus-prometheus
  namespace: monitoring
spec:
  rules:
  - host: <host_name>                     //Replace with prometheus host
    http:
      paths:
      - backend:
          service:
            name: prometheus-prometheus
            port:
              number: 9090
        path: /
        pathType: ImplementationSpecific
  tls:
  - hosts:
    - <host_name>                         //Replace with prometheus host
    secretName: <host_name>-tls-certs     //Replace with prometheus host
```

**Note**: Ensure you create the CANAME DNS record with the hostname and loadbalancer ID.

### Step 3: Install cost-analyzer on each client cluster

Kubecost provides the visibility into current and historical Kubernetes spend and resource allocation. These provide cost transparency in Kubernetes environments.

You can deploy the cost-analyzer using one of the below methods.

&#x20;    1\. Deploy using go lang deployer

```
git clone https://github.com/egovernments/DIGIT-DevOps.git
cd DIGIT-DevOps/deploy-as-code/egov-deployer
go run main.go -e <environment_name> "cost-analyzer"
```

&#x20;   2\.  Deploy using Jenkin’s deployment job. (here we are using deploy-to-dev, you can choose your environment specific deployment job )

<figure><img src="../../.gitbook/assets/Screenshot from 2022-12-21 18-15-34.png" alt=""><figcaption></figcaption></figure>

### Step 4: Install Grafana on the central-dashboard cluster

Below grafana configuration should be added to the environments file, and then Grafana should be deployed using one of the following methods.

Based on the number of client clusters, you have to add datasources. There should be one entry per client cluster as shown below

```
grafana: 
  image:
    repository: grafana/grafana
    tag: 9.0.0

  initContainers:
    gitSync:
      enabled: true
      repo: "git@github.com:egovernments/configs"  // repo contain the dashboard json files 
      branch: "central-dashboard"                 
  ingress:
    hostName: central-dashboard.digit.org  //central-dashboard hostname
    context: ""
    additionalAnnotations: | 
  grafana.ini:
    server:
      root_url: "%(protocol)s://%(domain)s"
      serve_from_sub_path: true 

  env: |
    - name: GF_SERVER_DOMAIN
      value: {{ .Values.ingress.hostName | quote }}    
  datasources:                // Configure Grafana to use prometheus datasources
    datasources.yaml:
      apiVersion: 1
      datasources:
      - name: DIGIT-Dev
        type: prometheus
        url: https://<Dev_hostname>  //Add exposed hostname for dev environment to access the dev prometheus metrics
        isDefault: false 
      - name: DIGIT-QA
        type: prometheus
        url: https://<QA_hostname>
        isDefault: false
      - name: DIGIT-UAT
        type: prometheus
        url: https://<UAT_hostname>
        isDefault: false
      - name: DIGIT-Staging
        type: prometheus
        url: https://<Staging_hostname>   
        isDefault: false
```

1.  Deploy using go lang deployer

    ```
    git clone https://github.com/egovernments/DIGIT-DevOps.git
    cd DIGIT-DevOps/deploy-as-code/egov-deployer
    go run main.go -e <environment_name> "grafana"
    ```


2.  Deploy using Jenkin’s deployment job.



    <figure><img src="../../.gitbook/assets/Screenshot from 2022-12-21 18-33-51.png" alt=""><figcaption></figcaption></figure>

### Step 4: DNS Mapping

To access the monitoring central dashboard with this https://central-dashboard.digit.org url. Ensure you create the CANAME DNS record with the hostname and loadbalancer ID.
