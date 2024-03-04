# Obtaining SSL certificates with the help of cluster-issuer

## Pre-Reads

{% embed url="https://cert-manager.io/docs/" %}

## Pre-requisites

* DIGIT uses [golang](https://golang.org/doc/install#download) (required v1.13.3) automated scripts to deploy the builds onto Kubernetes - [Linux](https://golang.org/dl/go1.13.3.linux-amd64.tar.gz) or [Windows](https://golang.org/dl/go1.13.3.windows-amd64.msi) or [Mac](https://golang.org/dl/go1.13.3.darwin-amd64.pkg).
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) is a CLI to connect to the kubernetes cluster from your machine
* [Install Visualstudio](https://code.visualstudio.com/download) IDE Code for better code/configuration editing capabilities
* All DIGIT services are packaged using helm charts[ ![](https://helm.sh/img/favicon-152.png)Installing Helm](https://helm.sh/docs/intro/install/)
* Git

## **What is Cert-manager**

Cert-manager adds certificates and certificate issuers as a resource types in kubernetes cluster,and **simplifies the process of obtaining, renewing and using those certificates**. It will ensure certificates are valid and up-to-date, and attempt to renew certificates at a configured time before expiring.

## What is SSL Certificate

SSL Certificate is a digital certificate that authenticates a website's identity and enables encrypted connection. SSL stands for **Secure Sockets Layer**, a security protocol that creates an encrypted link between a web server and a web browser. SSL cetificates keeps **internet connections secure** and prevents criminals from reading or modifying information transferred between two systems.

* Cert-Manager can issue certificates from a variety of supported sources, including [Let's Encrypt](https://letsencrypt.org/), [HashiCorp Vault](https://www.vaultproject.io/), and [Venafi](https://www.venafi.com/) as well as private PKI.
* In eGov Organization we are using **letsencrypt-prod,letsencrypt-staging** as a certificate-issuer.
* First, we have to clone DIGIT-DevOps repo.

```
$ git clone https://github.com/egovernments/DIGIT-DevOps.git
```

* Check the cert-manager chart templates which contains yaml files of clusterissuer and clusterrole in the below link.

[https://github.com/egovernments/DIGIT-DevOps/tree/release/config-as-                      code/helm/charts/backbone-services/cert-manager/templates](https://github.com/egovernments/DIGIT-DevOps/tree/release/config-as-code/helm/charts/backbone-services/cert-manager/templates)

* If we want to override any values in the chart. Open **values.yaml** and customize the chart.

[https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/helm/charts/backbone-services/cert-manager/values.yaml](https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/helm/charts/backbone-services/cert-manager/values.yaml)

* Open egov-demo template in the Visual Studio code.

```
$ code DIGIT-DevOps/config-as-code/environments/egov-demo.yaml
```

* Check whether the below configurations is present in your environment file. If not add these  configurations in your environment file.

<figure><img src="../../../.gitbook/assets/Screenshot from 2022-12-19 15-32-23.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/Screenshot from 2022-12-20 11-01-33.png" alt=""><figcaption></figcaption></figure>

## Deploying cert-manager

&#x20;Run the following command to deploy only the cert-manager.

```
$ cd DIGIT-DevOps/deploy-as-code/deployer
$ go run main.go -c -e egov-demo 'cert-manager'
```

* After deploying check the certificate is issued or not using the below command.&#x20;

```
$ kubectl get certificates -n <namespace_name>
```

* The following output will be displayed.

<figure><img src="../../../.gitbook/assets/Screenshot from 2022-12-20 11-19-13.png" alt=""><figcaption></figcaption></figure>

* Once the certificate is issued we can see it in secrets.

```
$ kubectl get secrets
```

* The following output will be displayed

<figure><img src="../../../.gitbook/assets/Screenshot from 2022-12-20 11-20-37.png" alt=""><figcaption></figcaption></figure>

* To know about the cluster-issuers used in our deployement we can use the following command.

```
$ kubectl get clusterissuers
```

* The following output will be displayed

<figure><img src="../../../.gitbook/assets/Screenshot from 2022-12-20 11-24-07.png" alt=""><figcaption></figcaption></figure>
