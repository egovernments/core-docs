---
description: >-
  This doc will cover how you can set up the monitoring and alerting on existing
  k8s cluster either with help of go lang script or Jenkins deployment Jobs.
---

# eGov Monitoring & Alerting Setup

[Prometheus](https://github.com/prometheus) is an open-source system monitoring and alerting toolkit originally built at [SoundCloud](https://soundcloud.com/)



## Pre-reads

[https://prometheus.io/docs/introduction/overview](https://prometheus.io/docs/introduction/overview/)[\
](https://prometheus.io/docs/introduction/overview/)[OAuth2-Proxy Setup](https://core.digit.org/guides/operations-guide/oauth2-proxy-setup)

## Pre-requisites <a href="#prerequisites" id="prerequisites"></a>

* DIGIT uses [golang](https://golang.org/doc/install#download) (required v1.13.3) automated scripts to deploy the builds onto Kubernetes - [Linux](https://golang.org/dl/go1.13.3.linux-amd64.tar.gz) or [Windows](https://golang.org/dl/go1.13.3.windows-amd64.msi) or [Mac](https://golang.org/dl/go1.13.3.darwin-amd64.pkg)
* All DIGIT services are packaged using helm charts[ ![](https://helm.sh/img/favicon-152.png)Installing Helm](https://helm.sh/docs/intro/install/)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) is a CLI to connect to the kubernetes cluster from your machine
* [Install Visualstudio](https://code.visualstudio.com/download) IDE Code for better code/configuration editing capabilities
* Git
* [OAuth2-Proxy Setup](https://core.digit.org/guides/operations-guide/oauth2-proxy-setup)



![Architectur](https://4016629814-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FX13sH0e4xi7bV1juDmGX%2Fuploads%2FHGVP5LUgHpOYCkXE3BWe%2Fimage.png?alt=media\&token=e97745b4-f1c7-468f-b60c-d5149f470d79)

[prometheus-operator](https://github.com/egovernments/eGov-infraOps/tree/master/helm/charts/backbone-services/prometheus-operator) chart includes multiple components and is suitable for a variety of use-cases.

The default installation is intended to suit monitoring a kubernetes cluster the chart is deployed onto. It closely matches the kube-prometheus project.

* [prometheus-operator](https://github.com/coreos/prometheus-operator)
* [prometheus](https://prometheus.io/)
* [alertmanager](https://prometheus.io/)
* [node-exporter](https://github.com/helm/charts/tree/master/stable/prometheus-node-exporter)
* [kube-state-metrics](https://github.com/helm/charts/tree/master/stable/kube-state-metrics)
* [grafana](https://github.com/helm/charts/tree/master/stable/grafana)
* service monitors to scrape internal kubernetes components
  * kube-apiserver
  * kube-scheduler
  * kube-controller-manager
  * etcd
  * kube-dns/coredns
  * kube-proxy

With the installation, the chart also includes dashboards and alerts.

**Deployment steps:**

1. Add the below grafana init container parameters to your [env config file](https://github.com/egovernments/DIGIT-DevOps/tree/master/deploy-as-code/helm/environments)
   1. Chose your env config file, if you are deploying **monitoring and alerting** into the qa environment chose qa.yaml similarly for uat, dev, and other environments.

<pre><code>grafana:
  initContainers:
    gitSync:
      enabled: true
      repo: "git@github.com:egovernments/configs" #REPLACE with your configs repo
<strong>      branch: "&#x3C;branch_name>" #REPLACE with config repo branch name
</strong>  dashboardsFolder: /work-dir/configs/monitoring-dashboards    
</code></pre>

Depending upon your environment config file update the configs repo branch (like for qa.yaml add qa branch and uat.yaml it would be UAT the branch)

2\. Add [monitoring-dashboards](https://github.com/egovernments/configs/tree/master/monitoring-dashboards) folder to the configs repo's branch which you selected in 1st step.

3\. Enable the serviceMonitor in the nginx-ingress configs which are available in the same \<env>.yaml and redeploy the nginx-ingress.

```
nginx-ingress:
  replicas: 1
  default-backend-service: "egov/nginx"
  namespace: egov
  cert-issuer: "letsencrypt-prod"
  ssl-protocols: "TLSv1.2 TLSv1.3"
  ssl-ciphers: "EECDH+CHACHA20:EECDH+AES"
  ssl-ecdh-curve: "X25519:prime256v1:secp521r1:secp384r1"
  controller:
    image:
      repository: egovio/nginx-ingress-controller
      tag: "0.26.1"     
    metrics:            #To collect the matrics data from nginx-ingress.
      enabled: true
      serviceMonitor:   #To enable the service monitoring of nginx-ingress
        enabled: true
    service:
      prometheusRule:
        enabled: true
```

`go run main.go deploy -e <environment_name> -c 'nginx-ingress'`

4\. To enable alerting, Add alertmanager secret in \<env>-secrets.yaml

If you want you can change the slack channel and other details like group\_wait, group\_interval, and repeat\_interval according to your values.

![](https://4016629814-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FX13sH0e4xi7bV1juDmGX%2Fuploads%2FVCRiKUv6eowPrhc62u4j%2Fimage.png?alt=media\&token=8ad9e108-a828-4298-b8c6-3d1840ecc08e)

5\.  You can deploy the prometheus-operator using one of the below methods.

&#x20;    1\. Deploy using go lang deployer

&#x20;          `go run main.go deploy -e <environment_name> -c 'prometheus-operator,grafana,prometheus-kafka-exporter'`

&#x20;   2\. Deploy using Jenkin’s deployment job. (here we are using deploy-to-dev, you can choose your environment specific deployment job )

![](https://4016629814-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FX13sH0e4xi7bV1juDmGX%2Fuploads%2FzeEDfZqccpKNfzTmkHGK%2Fimage.png?alt=media\&token=23980983-a47e-488c-81ff-1e5e9908289b)

You can connect to the monitoring console at [https://](https://qa.digit.org/monitoring/?orgId=1)[\<your\_domin\_name>/](https://egov-micro-qa.egovernments.org/tracing/search)[monitoring/](https://qa.digit.org/monitoring/?orgId=1)

## **To create a new panel in the existing dashboard:-**   <a href="#to-create-a-new-panel-in-the-existing-dashboard" id="to-create-a-new-panel-in-the-existing-dashboard"></a>

1. &#x20;Login to the dashboard and click on add panel &#x20;

![](https://4016629814-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FX13sH0e4xi7bV1juDmGX%2Fuploads%2FbQrNDpGnRLQxdVEGXu2g%2Fimage.png?alt=media\&token=98fc7d75-a31c-4684-983b-414ff03b56a2)

1. Set all required queries and apply the changes. Export the JSON file by clicking on the save dashboard

![](https://4016629814-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FX13sH0e4xi7bV1juDmGX%2Fuploads%2FzWL5LzMozVf4pE736o46%2Fimage.png?alt=media\&token=d4ef8402-be09-477d-9dc3-0622932e256c)

3\. Go to the configs repo and select your branch. In the branch look for the monitoring-dashboards folder and update the existing \*-dashboard.json with a newly exported JSON file.
