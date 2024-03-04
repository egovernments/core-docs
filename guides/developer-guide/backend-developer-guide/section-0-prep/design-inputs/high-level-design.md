---
description: Available design artifacts
---

# High Level Design

## API Specs

Find below the Open API specifications defined for this guide:

[Birth Registration](https://github.com/egovernments/DIGIT-OSS/blob/master/tutorials/backend-developer-guide/btr-services/birth-registration-api-spec.yaml)

## Process Workflow Diagram

![Basic workflow/swimlane diagram](<../../../../../.gitbook/assets/image (21) (1).png>)

## Registries

As a part of this guide, we are going to build a single birth registry. We will re-use the user registry from the DIGIT core. This will capture the mother and father details and store them in the user registry. The baby's details will remain in the birth registry.&#x20;

## Services

A single birth service will manage the registry.

## System Architecture Diagram

<figure><img src="../../../../../.gitbook/assets/Ideas (1).png" alt=""><figcaption><p>Images in red show the new birth registration service modules</p></figcaption></figure>

