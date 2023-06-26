# Deployment Architecture

On this page:

* [Sample Kubernetes architecture](deployment-architecture.md#sample-kubernetes-architecture)
* [DIGIT deployment architecture](deployment-architecture.md#digit-deployment-architecture)
* [CI/CD flow](deployment-architecture.md#ci-cd-flow)
* [Deployment scripts](deployment-architecture.md#deployment-scripts)

## Overview

This section contains architectural details about DIGIT deployment. It discusses the various activities in a sequence of steps to provision required infra and deploy DIGIT.

## Sample Kubernetes Architecture

<div align="left">

<figure><img src="../../../../.gitbook/assets/image (169).png" alt=""><figcaption></figcaption></figure>

</div>

## DIGIT Deployment Architecture

<figure><img src="../../../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

## CI/CD Flow

* Every code commit is well-reviewed and squash merge to branches through Pull Requests.
* Trigger the CI Pipeline that ensures code quality, vulnerability assessments, and CI tests before building the artefacts.
* Artefact is version controlled based on Semantic versioning based on the nature of the change.
* After successful CI, Jenkins bakes the Docker Images with the versioned artefacts and pushes the baked Docker image to Docker Registry.
* Deployment Pipeline pulls the built Image and pushes it to the corresponding environment.

## Deployment Scripts

* As all the DIGIT services are containerized and deployed on Kubernetes, we need to prepare deployment manifests. The same can be found [here](https://github.com/egovernments/Train-InfraOps).
* DIGIT has built helm charts using the standard helm approach to ease managing the service-specific configs, customisations, switch/toggle, secrets, etc.
* Golang base Deployment script that reads the values from the helm charts template and deploys into the cluster.
* Each env will have one master yaml template that will have the definition of all the services to be deployed, and their dependencies like Config, Env, Secrets, DB Credentials, Persistent Volumes, Manifest, Routing Rules, etc.

