# Deploy DIGIT

## Overview

This page details the steps to deploy the core platform services and reference applications.

The steps here can be used to deploy:

* DIGIT core platform services
* Public Grievance & Redressal module
* Trade Licence module
* Property Tax module
* Water & Sewerage module etc.

## **Pre-requisites**

1. DIGIT uses [golang](https://golang.org/doc/install#download) (required v1.13.3) automated scripts to deploy the builds onto Kubernetes - [Linux](https://golang.org/dl/go1.13.3.linux-amd64.tar.gz) or [Windows](https://golang.org/dl/go1.13.3.windows-amd64.msi) or [Mac](https://golang.org/dl/go1.13.3.darwin-amd64.pkg)
2. All DIGIT services are packaged using helm charts[ <img src="https://helm.sh/img/favicon-152.png" alt="" data-size="line">Installing Helm](https://helm.sh/docs/intro/install/)
3. [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) is a CLI to connect to the Kubernetes cluster from your machine
4. Install [CURL](https://help.ubidots.com/en/articles/2165289-learn-how-to-install-run-curl-on-windows-macosx-linux) for making API calls
5. [Install VisualStudio](https://code.visualstudio.com/download) IDE Code for better code/configuration editing capabilities
6. [Install Postman](https://www.postman.com/downloads/) to run digit bootstrap scripts

## Run Deployer

Once all the deployments configs are ready, run the command given below. Input the necessary details as prompted on the screen and the interactive installer will take care of the rest.

Run the egov-deployer golang script from the [DIGIT-Devops repo](https://github.com/egovernments/DIGIT-DevOps).

```
root@ip:# cd DIGIT-DevOps/deploy-as-code/egov-deployer

root@ip:# go run digit_setup.go
```

The interactive installer will prompt you for:

1. Whether the Kubernetes cluster is already set up
2. The path to the target environment's kubeconfig file
3. The DIGIT version to install
4. The DIGIT modules to install (for example, PGR)
5. Whether to preview the rendered manifests before deploying
6. Whether to proceed with the installation

All done, wait and watch for 10 min. The DIGIT setup is complete, and the application will run on the URL.

<mark style="color:red;">**Note:**</mark>

* <mark style="color:red;">**If you do not have your domain yet, you can edit the host file entries and map the nginx-ingress-service load balancer id like below**</mark>
  * <mark style="color:red;">**When you find it, add the following lines to the host file, save and close it.**</mark>
  * <mark style="color:red;">**`aws-load-balancer-id digit.try.com`**</mark>
* <mark style="color:red;">**If you have a GoDaddy account or similar and a DNS records edit access you can map the load balancer id to desired DNS. Create a**</mark> [<mark style="color:red;">**cname**</mark>](https://in.godaddy.com/help/add-a-cname-record-19236) <mark style="color:red;">**record with the load balancer ID and domain.**</mark>

You can now test the DIGIT application status in the command prompt/terminal using the command below.

```
curl -Is https://digit.try.com/employee/login |  head -n 1

OutPut:
HTTP/2 200
```
