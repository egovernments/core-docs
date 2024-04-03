---
description: High-level overview of DIGIT deployment
---

# DIGIT Deployment

## Basics

DIGIT is an open-source, customizable platform that lends itself to extensibility. New modules can be built on top of the platform to suit new use-cases or existing modules can be modified or replaced. To enable this, in addition to deploying DIGIT, a CI/CD pipeline should be set up. CD/CI pipelines enable the end user to automate & simplify the build/deploy process.

DIGIT comes with configurable "CI as code", "Deploy as code" etc.. which can be utilized to set up the pipelines and deploy new modules. More on that in the steps below.&#x20;

<mark style="color:orange;">**Note: Changing the DIGIT code has implications for upgrades. That is, you may not be able to upgrade to the latest version of DIGIT depending on the changes that have been made. New modules are generally not a problem for upgrades.**</mark>&#x20;

## Deployment Strategies

<table data-view="cards"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><a href="https://app.gitbook.com/o/-MEQmzNGXk5ajuZujG7E/s/egsIWleSdyH9rMLJ8ShI/~/changes/110/guides/installation-guide/digit-deployment/deployment-using-go"><mark style="color:blue;"><strong>Deployment Using Golang</strong></mark></a></td><td>If you're already running DIGIT and want to deploy using Go exclusively, this document is your go-to reference.</td><td></td></tr><tr><td><a href="https://app.gitbook.com/o/-MEQmzNGXk5ajuZujG7E/s/egsIWleSdyH9rMLJ8ShI/~/changes/110/guides/installation-guide/digit-deployment/deployment-using-helmfile"><mark style="color:blue;"><strong>Deployment Using Helmfile</strong></mark></a></td><td>If you're deploying DIGIT for the first time, we recommend using the Helmfile documentation for guidance.</td><td></td></tr><tr><td><a href="https://app.gitbook.com/o/-MEQmzNGXk5ajuZujG7E/s/egsIWleSdyH9rMLJ8ShI/~/changes/110/guides/installation-guide/digit-deployment/deployment-using-githubactions"><mark style="color:blue;"><strong>Deployment using GithubActions</strong></mark></a></td><td>For a one-click deployment of DiGIT, please refer to this document.</td><td></td></tr></tbody></table>

* [x] [Setup CD/CI pipeline](../setup-guide/ci-cd-set-up/) – This enables you to change code for individual modules/ add new modules (ILMS), build individual modules and deploy them into your environment.&#x20;
* [x] Develop on top of DIGIT&#x20;
  1. Design Guide - [Reference docs](../../design-guide/)
  2. Create a new module. Refer to the steps in the [development guide](../../developer-guide/backend-developer-guide/).
  3. Build the new module (part of the development guide) [using Jenkins](../setup-guide/ci-cd-set-up/ci-cd-build-job-pipeline-setup.md) → [Reference docs](../setup-guide/ci-cd-set-up/ci-cd-build-job-pipeline-setup.md).
  4. Deploy the new module into your DIGIT environment.

