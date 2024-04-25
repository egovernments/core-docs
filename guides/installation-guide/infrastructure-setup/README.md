---
description: Setup infrastructure required for deploying DIGIT
---

# Infrastructure Setup

#### Topics Covered:

* [List of pre-reads for a better understanding](./#pre-reads)
* [Choose your cloud for setup](./#1.-choose-your-cloud)

## Basics

DIGIT can be deployed on a public cloud like AWS, Azure or a private cloud.&#x20;

## Pre-reads

* Learn the basics of Kubernetes: [https://www.youtube.com/watch?v=PH-2FfFD2PU\&t=3s](https://www.youtube.com/watch?v=PH-2FfFD2PU\&t=3s)
* Learn the [basics of kubectl](https://www.tutorialspoint.com/kubernetes/kubernetes\_kubectl\_commands.htm) commands

## Choose Your Cloud

{% hint style="info" %}
<mark style="color:orange;">**Note:**</mark> To deploy DIGIT using Github Actions, refer to the document - [DIGIT Deployment Using GithubActions](https://core.digit.org/guides/installation-guide/digit-deployment/deployment-using-github-actions). With this installation approach, there's no need to manually create the infrastructure as GitHub Actions will automatically handle the creation and deployment of DIGIT.
{% endhint %}

Choose your cloud and follow the instructions to set up a Kubernetes cluster before deploying.

{% content-ref url="aws/" %}
[aws](aws/)
{% endcontent-ref %}

{% content-ref url="azure/" %}
[azure](azure/)
{% endcontent-ref %}

{% content-ref url="sdc/" %}
[sdc](sdc/)
{% endcontent-ref %}





&#x20;

