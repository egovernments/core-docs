---
title: DIGIT Infra Setup
---

# Overview

DIGIT can be deployed on a public cloud like AWS, Azure or a private cloud.

# Pre-reads

* Learn the basics of Kubernetes: [https://www.youtube.com/watch?v=PH-2FfFD2PU\&t=3s](https://www.youtube.com/watch?v=PH-2FfFD2PU\&t=3s)
* Learn the [basics of kubectl](https://www.tutorialspoint.com/kubernetes/kubernetes_kubectl_commands.htm) commands

{% hint style="info" %}
<mark style="color:orange;">**Note:**</mark> To deploy DIGIT using GitHub Actions, refer to the document - [DIGIT Deployment Using GithubActions](https://core.digit.org/guides/installation-guide/digit-deployment/deployment-using-github-actions). With this installation approach, there's no need to manually create the infrastructure as GitHub Actions will automatically handle the creation and deployment of DIGIT.
{% endhint %}

### Virtual Machine Sizing

For a baseline deployment, we recommend a **minimum of 4 VMs or Nodes**.

**Recommended VM Configuration:**

<table><thead><tr><th width="162.766845703125" align="center" valign="middle">Resource</th><th width="173.579833984375" align="center">Recommended Per Node</th><th align="center">Total Cluster Capacity</th></tr></thead><tbody><tr><td align="center" valign="middle">vCpu</td><td align="center">4 cores</td><td align="center">16 cores</td></tr><tr><td align="center" valign="middle">Memory</td><td align="center">16 GB</td><td align="center">64 GB</td></tr><tr><td align="center" valign="middle">Storage</td><td align="center">100 GB</td><td align="center">400 GB</td></tr></tbody></table>

Choose your cloud and follow the instructions to set up a Kubernetes cluster before deploying.

{% content-ref url="../../guides/installation-guide/infrastructure-setup/aws/" %}
[aws](../../guides/installation-guide/infrastructure-setup/aws/)
{% endcontent-ref %}

{% content-ref url="../../guides/installation-guide/infrastructure-setup/azure/" %}
[azure](../../guides/installation-guide/infrastructure-setup/azure/)
{% endcontent-ref %}

{% content-ref url="https://app.gitbook.com/s/051YseixNq69PlJkCdKt/deploy/installation-guide/infrastructure-setup/google-cloud-platform-gcp" %}
[Google Cloud Platform (GCP)](https://app.gitbook.com/s/051YseixNq69PlJkCdKt/deploy/installation-guide/infrastructure-setup/google-cloud-platform-gcp)
{% endcontent-ref %}

{% content-ref url="../../guides/installation-guide/infrastructure-setup/sdc/" %}
[sdc](../../guides/installation-guide/infrastructure-setup/sdc/)
{% endcontent-ref %}
