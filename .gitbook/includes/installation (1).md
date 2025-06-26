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

Choose your cloud and follow the instructions to set up a Kubernetes cluster before deploying.

{% content-ref url="../../guides/installation-guide/infrastructure-setup/aws/" %}
[aws](../../guides/installation-guide/infrastructure-setup/aws/)
{% endcontent-ref %}

{% content-ref url="../../guides/installation-guide/infrastructure-setup/azure/" %}
[azure](../../guides/installation-guide/infrastructure-setup/azure/)
{% endcontent-ref %}

{% content-ref url="../../guides/installation-guide/infrastructure-setup/sdc/" %}
[sdc](../../guides/installation-guide/infrastructure-setup/sdc/)
{% endcontent-ref %}
