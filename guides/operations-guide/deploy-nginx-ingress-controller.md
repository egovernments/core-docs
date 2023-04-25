---
description: >-
  In this tutorial, we will go through the step by step process to deploy an
  NGINX ingress controller on a Kubernetes cluster.
---

# Deploy Nginx-Ingress-Controller

The vast majority of Kubernetes clusters are used to host containers that process incoming requests from microservices to full web applications. Having these incoming requests come into a central location, then get handed out via services in Kubernetes, is the most secure way to configure a cluster. That central incoming point is an ingress controller.

NGINX is the most popularly used ingress controller for Kubernetes clusters. NGINX has most of the features enterprises are looking for, and will work as an ingress controller for Kubernetes regardless of which cloud, virtualization platform, or Linux operating system your Kubernetes cluster is running on.

### Pre-reads

* [https://docs.nginx.com/nginx-ingress-controller/](https://docs.nginx.com/nginx-ingress-controller/)\


### Pre-requisites <a href="#prerequisites" id="prerequisites"></a>

* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) is a CLI to connect to the kubernetes cluster from your machine
* [Install Visualstudio](https://code.visualstudio.com/download) IDE Code for better code/configuration editing capabilities
* All DIGIT services are packaged using helm charts[ ![](https://helm.sh/img/favicon-152.png)Installing Helm](https://helm.sh/docs/intro/install/)
* DIGIT uses [golang](https://golang.org/doc/install#download) (required v1.13.3) automated scripts to deploy the builds onto Kubernetes - [Linux](https://golang.org/dl/go1.13.3.linux-amd64.tar.gz) or [Windows](https://golang.org/dl/go1.13.3.windows-amd64.msi) or [Mac](https://golang.org/dl/go1.13.3.darwin-amd64.pkg)
* Git

### Install NGINX Ingress Controller

A Kubernetes service account is required to run NGINX as a service within the cluster. The service account needs to have following roles:

* A cluster role to allow it to get, list, and read the configuration of all services and events. This role could be limited if you were to have multiple ingress controllers installed within the cluster. But in most cases, limiting access for this service account may not be needed.
* A namespace-specific role to read and update all the ConfigMaps and other items that are specific to the NGINX Ingress controller’s own configuration.

Clone the following [DIGIT-DevOps](https://github.com/egovernments/DIGIT-DevOps) repo (If not already done as part of Infra setup), you may need to [install git](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository-from-github/cloning-a-repository) and then run [git clone](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository-from-github/cloning-a-repository) it to your machine.

```
git clone -b release https://github.com/egovernments/DIGIT-DevOps
code DIGIT-DevOps/config-as-code/environments/egov-demo-template.yaml
```

The following configurations should be added to the environment file if they are not already there

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
    metrics:
      enabled: true
      serviceMonitor:
        enabled: false  // To enable the service monitor, make sure you have installed the serviceMonitor CRD.  
    service:
      annotations: 
        service.beta.kubernetes.io/aws-load-balancer-type: nlb   // for Network Load Balancing (NLB) 
        enabled: true 
      prometheusRule:   
        enabled: false  // To enable prometheus rules, make sure you have deployed prometheus.
        
cert-manager:
  email: "<email_id>" // replace with email id to verify the domain
  images:
    - "quay.io/jetstack/cert-manager-controller:v0.10.1"
  namespace: egov
                
```

### &#x20;To apply this configuration, run the following command:

```
cd DIGIT-DevOps/deploy-as-code/deployer
go run main.go -c -e egov-demo-template 'nginx-ingress,cert-manager'
```





\
