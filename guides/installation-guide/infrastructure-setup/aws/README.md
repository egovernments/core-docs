---
description: Provision infra for DIGIT on AWS using Terraform
---

# AWS

#### Topics covered:

* [AWS deployment basics](./#overview)
* [Pre-reads before deployment](./#pre-reads)
* [Steps to install ](./#prerequisites)

## Overview

The [**Amazon Elastic Kubernetes Service (EKS)**](https://docs.aws.amazon.com/eks/latest/userguide/what-is-eks.html) is one of the AWS services for deploying, managing, and scaling any distributed and containerized workloads. Here we can provision the EKS cluster on AWS from the ground up and using an automated way (infra-as-code) using [**terraform**](https://www.terraform.io/intro/index.html) and then deploy the DIGIT services config-as-code using [**Helm**](https://helm.sh/docs/).

## Pre-reads

* Know about EKS: [https://www.youtube.com/watch?v=SsUnPWp5ilc](https://www.youtube.com/watch?v=SsUnPWp5ilc)
* Know what is terraform: [https://youtu.be/h970ZBgKINg](https://youtu.be/h970ZBgKINg)

## Installation Steps <a href="#prerequisites" id="prerequisites"></a>

{% content-ref url="1.-pre-requisites.md" %}
[1.-pre-requisites.md](1.-pre-requisites.md)
{% endcontent-ref %}

{% content-ref url="2.-understanding-eks.md" %}
[2.-understanding-eks.md](2.-understanding-eks.md)
{% endcontent-ref %}

{% content-ref url="3.-setup-aws-account.md" %}
[3.-setup-aws-account.md](3.-setup-aws-account.md)
{% endcontent-ref %}

{% content-ref url="4.-provisioning-infra-using-terraform.md" %}
[4.-provisioning-infra-using-terraform.md](4.-provisioning-infra-using-terraform.md)
{% endcontent-ref %}

{% content-ref url="../../../../get-started/installation-guide/digit-deployment/deployment-using-golang/prepare-deployment-configuration.md" %}
[prepare-deployment-configuration.md](../../../../get-started/installation-guide/digit-deployment/deployment-using-golang/prepare-deployment-configuration.md)
{% endcontent-ref %}

{% content-ref url="../../../../get-started/installation-guide/digit-deployment/deployment-using-golang/deploy-digit.md" %}
[deploy-digit.md](../../../../get-started/installation-guide/digit-deployment/deployment-using-golang/deploy-digit.md)
{% endcontent-ref %}

{% content-ref url="../../../data-setup-guide/bootstrap-digit.md" %}
[bootstrap-digit.md](../../../data-setup-guide/bootstrap-digit.md)
{% endcontent-ref %}
