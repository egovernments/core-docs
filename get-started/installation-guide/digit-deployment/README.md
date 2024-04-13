---
description: High-level overview of DIGIT deployment
---

# DIGIT Deployment

## Basics

DIGIT is an open-source, customizable platform that lends itself to extensibility. New modules can be built on top of the platform to suit new use-cases or existing modules can be modified or replaced. To enable this, in addition to deploying DIGIT, a CI/CD pipeline should be set up. CD/CI pipelines enable the end user to automate & simplify the build/deploy process.

DIGIT comes with configurable "CI as code", "Deploy as code" etc.. which can be utilized to set up the pipelines and deploy new modules. More on that in the steps below.&#x20;

<mark style="color:orange;">**Note: Changing the DIGIT code has implications for upgrades. That is, you may not be able to upgrade to the latest version of DIGIT depending on the changes that have been made. New modules are generally not a problem for upgrades.**</mark>&#x20;

## Pre-reads

* Find out more on kubernetes manifests: [https://www.youtube.com/watch?v=ohSUtEfDefc](https://www.youtube.com/watch?v=ohSUtEfDefc)
* Learn how to manage env values, secrets of any service deployed in kubernetes [https://www.youtube.com/watch?v=OW244LxB4oI](https://www.youtube.com/watch?v=OW244LxB4oI)
* Explore how to port forward to a pod running inside k8s cluster and work locally [https://www.youtube.com/watch?v=TT3nd5n5Yus](https://www.youtube.com/watch?v=TT3nd5n5Yus)
* Find the SOPs to secure your keys/creds: [https://www.youtube.com/watch?v=DWzJ87KbwxA](https://www.youtube.com/watch?v=DWzJ87KbwxA)

## Deployment Strategies

<table data-view="cards"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><mark style="color:blue;"><strong>Deployment - Key Concepts</strong></mark></td><td>This section contains the list of documents that explains the key concepts required for DIGIT  deployment.</td><td></td></tr><tr><td><a href="https://core.digit.org/v/2.9-lts/guides/installation-guide/digit-deployment/deployment-using-golang"><mark style="color:blue;"><strong>Deployment Using Golang</strong></mark></a></td><td>If you're already running DIGIT and want to deploy using Go exclusively, this document is your go-to reference.</td><td></td></tr><tr><td><a href="https://core.digit.org/v/2.9-lts/guides/installation-guide/digit-deployment/deployment-using-helmfile"><mark style="color:blue;"><strong>Deployment Using Helmfil</strong></mark></a><mark style="color:blue;"><strong>e</strong></mark></td><td>If you're deploying DIGIT for the first time, we recommend using the Helmfile documentation for guidance.</td><td></td></tr><tr><td><a href="https://core.digit.org/v/2.9-lts/guides/installation-guide/digit-deployment/deployment-using-githubactions"><mark style="color:blue;"><strong>Deployment using GithubActions</strong></mark></a></td><td>For a one-click deployment of DiGIT, please refer to this document.</td><td></td></tr></tbody></table>

* [x] [Setup CD/CI pipeline](../../../guides/installation-guide/infrastructure-setup-guide/ci-cd-set-up/) – This enables you to change code for individual modules/ add new modules (ILMS), build individual modules and deploy them into your environment.&#x20;
* [x] Develop on top of DIGIT&#x20;
  1. Design Guide - [Reference docs](../../design-guide/)
  2. Create a new module. Refer to the steps in the [development guide](../../developer-guide/backend-developer-guide/).
  3. Build the new module (part of the development guide) [using Jenkins](../../../guides/installation-guide/infrastructure-setup-guide/ci-cd-set-up/ci-cd-build-job-pipeline-setup.md) → [Reference docs](../../../guides/installation-guide/infrastructure-setup-guide/ci-cd-set-up/ci-cd-build-job-pipeline-setup.md).
  4. Deploy the new module into your DIGIT environment.

