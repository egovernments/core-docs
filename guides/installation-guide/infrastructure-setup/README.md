---
description: Setup infrastructure required for deploying DIGIT
---

# Infrastructure Setup

#### Topics Covered:

* [List of pre-reads for a better understanding](./#pre-reads)
* [Choose your cloud for setup](./#1.-choose-your-cloud)

## Basics

DIGIT can be deployed on public cloud like AWS, Azure or private cloud.&#x20;

## Pre-reads

* Learn the basics of Kubernetes: [https://www.youtube.com/watch?v=PH-2FfFD2PU\&t=3s](https://www.youtube.com/watch?v=PH-2FfFD2PU\&t=3s)
* Learn the [basics of kubectl](https://www.tutorialspoint.com/kubernetes/kubernetes\_kubectl\_commands.htm) commands

## Choose Your Cloud

<mark style="color:orange;">**Note:**</mark> If you want to deploy DIGIT using Github Actions, you can refer directly to  [DIGIT Deployment Using GithubActions](https://core.digit.org/guides/installation-guide/digit-deployment/deployment-using-github-actions). There's no need to create the infrastructure manually because Github Actions will automatically create and deploy DIGIT.

Choose your cloud and follow the instructions to set up a Kubernetes cluster before moving on to deployment.

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

