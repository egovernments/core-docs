---
description: >-
  Here we are going to learn how to install helm and why we are helm in
  DIGIT-DevOps
---

# Helm installation:

Before installing Helm you need to know about **Yaml files.**\
**Yaml file: Yaml files (Yet another Markup Language)**are used to transmitting the data in web applications. \
**Json file: Json  files (JavaScript Object Notation)** are a standard text based format to view the structured data of javascript object syntax.

[Both Json and yaml files are used for transmitting data between web applications but the only difference is, In Yaml file there is indentation like python that shows the level of your code unlike Json](#user-content-fn-1)[^1]

### Prerequisites:

1. Git(please visit **GitOps** page if you didn't installed Git)
2. Install visual studio [https://code.visualstudio.com/download](https://code.visualstudio.com/download) IDE Code for better code visualization/editing capabilities
3. Install Golang [https://go.dev/doc/install#download](https://go.dev/doc/install#download)(required version:V1.13.3)
4. Kubectl(see **working with kubernetes** page to install kubectl)

* **What is helm?** helm can be defined as [package manager for kubernetes](#user-content-fn-2)[^2] It is used to deploy(to extend) the applications and services easily into kubernetes cluster in the form of Helm charts.
* **what are helm charts?** It [consists set of templates ](#user-content-fn-3)[^3]and a file containing variables used to fill these templates based on the custom values and configurations.
* **Why we are using helm in DIGIT?**

1. Greatly improved productivity
2. Reduced complexity of deployments
3. More streamlined CI/CD pipeline

Helm charts are written in YAML and contain everything your developers need to deploy a container to a Kubernetes cluster.You may be used to creating Pods, Deployments, Services etc. in Kubernetes via the kubectl create command. This way of creating objects is indeed valid and great for learning purposes. However, when running Kubernetes in production you often want to have all your objects defined as .yaml files. This makes it easier for others to know what’s running in the cluster, and allows for your deployments to be version controlled.

#### &#x20;To install Helm, follow the link provided below         [https://helm.sh/docs/intro/install/](https://helm.sh/docs/intro/install/)



[^1]: 

[^2]: 

[^3]: 
