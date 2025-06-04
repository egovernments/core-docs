---
description: Provision infra for DIGIT on GCP using Terraform
---

# Google Cloud Platform (GCP)

## Overview <a href="#overview" id="overview"></a>

[Google Kubernetes Engine (GKE)](https://cloud.google.com/kubernetes-engine/docs/concepts/kubernetes-engine-overview) is a GCP service for deploying, managing, and scaling distributed and containerised workloads. With GKE, you can easily provision a cluster on GCP using [Terraform](https://www.terraform.io/intro/index.html)**,** which automates the process. The DIGIT services configuration will be deployed using [Helm](https://helm.sh/docs/).

## Pre-reads <a href="#pre-reads" id="pre-reads"></a>

* Know about EKS: [![](https://www.youtube.com/s/desktop/cbfd6f42/img/logos/favicon_32x32.png)Creating a GKE cluster (demo)](https://www.youtube.com/watch?v=hxpGC19PzwI)
* Know what is terraform: [![](https://www.youtube.com/s/desktop/cbfd6f42/img/logos/favicon_32x32.png)Introduction to HashiCorp Terraform with Armon Dadgar](https://youtu.be/h970ZBgKINg)

## Installation Steps <a href="#installation-steps" id="installation-steps"></a>

* [GCP Pre-requisites](gcp-pre-requisites.md)
* [Setup GCP Account](setup-gcp-account.md)
* [Provision Infrastructure](gcp-provision-infrastructure.md)
