---
description: High-level overview of DIGIT deployment
---

# DIGIT Deployment

## Basics

DIGIT is an open-source, customizable platform that lends itself to extensibility. New modules can be built on top of the platform to suit new use-cases or existing modules can be modified or replaced. To enable this, in addition to deploying DIGIT, a CD/CI pipeline should be set up. CD/CI pipelines enable the end user to automate & simplify the build/deploy process.

DIGIT comes with configurable "CI as code", "Deploy as code" etc.. which can be utilized to set up the pipelines and deploy new modules. More on that in the steps below.&#x20;

<mark style="color:orange;">**Note: Changing the DIGIT code has implications for upgrades. That is, you may not be able to upgrade to the latest version of DIGIT depending on the changes that have been made. New modules are generally not a problem for upgrades.**</mark>&#x20;

## Steps

* [x] Fork code from DIGIT GitHub Repository into the organization umbrella. The recommendation is to have it under the entity that will own it.&#x20;
* [x] All code work needs to happen from this new Git repository. Standard branching practices need to be followed:&#x20;
  * One branch per environment - dev, qa, uat&#x20;
  * Developers to follow best practices for branching, code-checking, PRs etc..&#x20;
* [x] Follow DIGIT installation docs and install the latest version **(v2.7)**. Installation steps given below:&#x20;
  1. **Quickstart install (Single VM setup)** - for dev and test – [Reference docs ](quick-setup/)
  2. **Full installation (cluster setup)** - for UAT – [Reference docs ](production-setup/aws/)
  3. Add an extra node to the Kube cluster to deploy Prometheus/Jaeger&#x20;
     * Enable Jaeger and Prometheus post-installation (ONLY for production) as they are not enabled by default. These are our observability tools. Refer to [the docs ](../operations-guide/observability/egov-monitoring-and-alerting-setup.md)for detailed steps.&#x20;
* [x] [Setup CD/CI pipeline](production-setup/ci-cd-set-up/) – This enables you to change code for individual modules/ add new modules (ILMS), build individual modules and deploy them into your environment.&#x20;
* [x] Develop on top of DIGIT&#x20;
  1. Design Guide - [Reference docs](../design-guide/)
  2. Create a new module. Follow the [development guide](../developer-guide/backend-developer-guide/)&#x20;
  3. Build the new module (part of the development guide) [using Jenkins](production-setup/ci-cd-set-up/ci-cd-build-job-pipeline-setup.md) → [Reference docs ](production-setup/ci-cd-set-up/ci-cd-build-job-pipeline-setup.md)
  4. Deploy the new module into your DIGIT environment

