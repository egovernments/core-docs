---
description: >-
  Here we are going to learn how to install helm and why we are helm in
  DIGIT-DevOps
---

# Helm Installation

Before installing Helm you need to know about **Yaml files.**\
**Yaml file: Yaml files (Yet Another Markup Language)** are used to transmit the data in web applications. \
**Json file: Json files (JavaScript Object Notation)** are a standard text-based format to view the structured data of javascript object syntax.

JSON and YAML files are both used to transfer data between web applications. The key difference is that YAML files use indentation similar to Python to indicate the level of your code, unlike JSON.

### Pre-requisites

1. Git (please visit the **GitOps** page if you haven't installed Git).
2. Install Visual Studio [https://code.visualstudio.com/download](https://code.visualstudio.com/download) IDE Code for better code visualization/editing capabilities
3. Install Golang [https://go.dev/doc/install#download](https://go.dev/doc/install#download)(required version:V1.13.3)
4. Kubectl (see **working with Kubernetes** page to install kubectl)

* **What is helm?** helm can be defined as a [package manager for Kubernetes](#user-content-fn-1)[^1]. It is used to deploy (to extend) the applications and services easily into the Kubernetes cluster in the form of Helm charts.
* **What are helm charts?** It [consists of a set of templates ](#user-content-fn-2)[^2]and a file containing variables used to fill these templates based on the custom values and configurations.
* **Why are we using helm in DIGIT?**
  1. Greatly improved productivity
  2. Reduced complexity of deployments
  3. More streamlined CI/CD pipeline

Helm charts are written in YAML and contain everything your developers need to deploy a container to a Kubernetes cluster. You may be used to creating Pods, Deployments, Services etc. in Kubernetes via the kubectl create command. This way of creating objects is indeed valid and great for learning purposes. However, when running Kubernetes in production you often want to have all your objects defined as .yaml files. This makes it easier for others to know what’s running in the cluster and allows for your deployments to be version-controlled.

#### &#x20;To install Helm, follow the link provided below         [https://helm.sh/docs/intro/install/](https://helm.sh/docs/intro/install/)



[^1]: 

[^2]: 
