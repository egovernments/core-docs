---
title: Azure prerequisites
---

# Overview

The Azure Kubernetes Service (AKS) is one of the Azure services for deploying, managing and scaling any distributed and containerised workloads. Here we can provision the AKS cluster on Azure from the ground up using [**Terraform**](https://www.terraform.io/intro/index.html) **(**&#x69;nfra-as-code) and then deploy the DIGIT platform services as config-as-code using [**Helm**](https://helm.sh/docs/).

# Pre-reads <a href="#pre-read" id="pre-read"></a>

* [Learn more about AKS](https://www.youtube.com/watch?v=i5aALhhXDwc\&ab_channel=DevOpsCoach)​
* [Learn what Terraform is](https://youtu.be/h970ZBgKINg)

# **Pre-requisites**​

1. Azure subscription: If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com\&utm_source=microsoft.com\&utm_medium=docs\&utm_campaign=visualstudio) before you begin.
2. Install Azure [CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
3. Configure Terraform: Follow the directions in the article, [Terraform and configure access to Azure](https://docs.microsoft.com/en-us/azure/developer/terraform/get-started-cloud-shell)
4. Azure service principal: Follow the directions in the Create the service principal section in the article, [Create an Azure service principal with Azure CLI](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?view=azure-cli-latest). Take note of the values for the appId, displayName, password, and tenant.
5. Install [kubectl](https://kubernetes.io/docs/tasks/tools/) on your local machine, which helps you interact with the Kubernetes cluster.
6. Install [Helm](https://helm.sh/docs/intro/install/), which helps you package the services along with the configurations, environments, secrets, etc, into [Kubernetes manifests.](https://devspace.cloud/docs/cli/deployment/kubernetes-manifests/what-are-manifests)

{% hint style="info" %}
Explore AKS concepts using the links given below -

* [Kubernetes Fundamentals](https://medium.com/the-programmer/kubernetes-fundamentals-for-absolute-beginners-architecture-components-1f7cda8ea536)
* [AKS Fundamentals](https://docs.microsoft.com/en-us/azure/aks/concepts-clusters-workloads)
* [Manually Provision AKS](https://docs.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-portal)
{% endhint %}
