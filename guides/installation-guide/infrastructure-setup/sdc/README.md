---
description: Deployment on SDC
---

# SDC

#### Topics covered:

* [Introduction to SDC](./#overview)
* [Automating the deployment process](./#automating-the-deployment-process)
* [Installation steps](./#installation-steps)

## Overview

Running Kubernetes on-premise gives a cloud-native experience on SDC when it comes to deploying DIGIT.

Whether States have their own on-premise data centre or have decided to forego the various managed cloud solutions, there are a few things one should know when getting started with on-premise K8s.

One should be familiar with Kubernetes and the [control plane](https://kubernetes.io/docs/concepts/overview/components/#master-components) consists of the Kube-apiserver, Kube-scheduler, Kube-controller-manager and an ETCD datastore. For managed cloud solutions like [Google’s Kubernetes Engine (GKE)](https://cloud.google.com/kubernetes-engine/) or [Azure’s Kubernetes Service (AKS)](https://azure.microsoft.com/en-us/services/kubernetes-service/), it also includes the cloud-controller-manager. This is the component that connects the cluster to external cloud services to provide networking, storage, authentication, and other support features.

To successfully deploy a bespoke Kubernetes cluster and achieve a cloud-like experience on SDC, one needs to replicate all the same features you get with a managed solution. At a high level, this means that we probably want to:

* Automate the deployment process
* Choose a networking solution
* Choose a right storage solution
* Handle security and authentication

The subsequent sections look at each of these challenges individually, and provide enough of a context required to help in getting started.

## Automating The Deployment Process

Using a tool like Ansible can make deploying Kubernetes clusters on-premise trivial.

When deciding to manage your own Kubernetes clusters, we need to set up a few proofs-of-concept (PoC) clusters to learn how everything works, perform performance and conformance tests, and try out different configuration options.

After this phase, automating the deployment process is an important if not necessary step to ensure consistency across any clusters you build. For this, you have a few options, but the most popular are:

* [**kubeadm**](https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm/): a low-level tool that helps you bootstrap a minimum viable Kubernetes cluster that conforms to best practices
* [**kubespray**](https://github.com/kubernetes-sigs/kubespray): an Ansible playbook that helps deploy production-ready clusters

If you already using Ansible, Kubespray is a great option, otherwise, we recommend writing automation around Kubeadm using your preferred playbook tool after using it a few times. This will also increase your confidence and knowledge of Kubernetes.

## Installation Steps

{% content-ref url="1.-sdc-pre-requisites.md" %}
[1.-sdc-pre-requisites.md](1.-sdc-pre-requisites.md)
{% endcontent-ref %}

{% content-ref url="2.-infra-as-code-kubespray.md" %}
[2.-infra-as-code-kubespray.md](2.-infra-as-code-kubespray.md)
{% endcontent-ref %}

{% content-ref url="../../../../get-started/installation-guide/digit-deployment/" %}
[digit-deployment](../../../../get-started/installation-guide/digit-deployment/)
{% endcontent-ref %}

{% content-ref url="../../../data-setup-guide/bootstrap-digit.md" %}
[bootstrap-digit.md](../../../data-setup-guide/bootstrap-digit.md)
{% endcontent-ref %}



