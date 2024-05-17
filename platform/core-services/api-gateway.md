---
description: Deployment With Spring Cloud
---

# API Gateway

## Overview

To ensure Long Term Support for the DIGIT platform, we're auditing our core services for outdated dependencies. The present API gateway, built using Netflix Zuul, has few dependencies that will become obsolete soon. Hence we are building a new Gateway on top of spring cloud gateway to address this issue.&#x20;

**What is Spring Cloud Gateway and how is it different from Zuul?**

Spring Cloud Gateway and Zuul serve similar purposes as API gateways but differ in their underlying architecture and design philosophies. Spring Cloud Gateway is well-suited for modern, reactive applications, while Zuul is more established and may be preferred in traditional, blocking I/O environments. Ultimately, the choice between the two depends on the specific requirements.

**Navigating the new Gateway codebase**&#x20;

The new Gateway codebase is well modularised where each module hold similar files and named that makes it self explanatory as it identifies the tasks each actor performs. Below is a snapshot of the current directory structure.&#x20;

![](<../../.gitbook/assets/image (315).png>)&#x20;

**Config**: It contains the configuration-related files for example Application Properties etc.

**Constants**: It contains the constants referenced frequently within the codebase. Add any constant string literal here and then access it via this file.

**Filters**: This folder is the heart of the API gateway since it contains all the **PRE**, **POST**, and **ERROR** filters. For those new to filters: Filters intercept incoming and outgoing requests, allowing developers to apply various functionalities such as authentication, authorisation, rate limiting, logging, and transformation to these requests and responses.

**Model**: contains the P.O.J.O required in the gateway.

**Producer**: contains code related to pushing data onto Kafka.

**Rate limiters** contain files for initialising the relevant bean for custom rate limiting.

**Utils**: contains the helper function which can be reused across the project.&#x20;

This introduction provides you with the basics of the gateway and its project structure, offering a high-level overview of the Gateway's functionality.

When a request is received, the Gateway verifies if it matches any predefined routes. If a match is found, it undergoes a series of filters, each performing specific validation or enrichment tasks. The exact order of these filters will be discussed later. For now, it's important to understand that the Gateway checks restricted routes for proper authentication and authorization.&#x20;

Additionally, there's an option to whitelist certain APIs as open endpoints or mixed-mode endpoints, allowing skipping of authentication or authorization for those specific APIs. Upon receiving a request, the Gateway first checks for an existing route definition that matches the request path. If a match is found, it begins executing the pre-filters in the specified order.

**Pre-Filter**

1. RequestStartTimerFilter:  Sets request start time&#x20;
2. CorrelationIdFilter: Generate and set a correlationId in each request to help track it in the downstream service
3. AuthPreCheckFilter: Checks for if Authorisation has to be performed
4. PreHookFilter: Sends a pre-hook request
5. RbacPreFilter: Checks if Authentication has to be performed or not
6. AuthFilter: Authenticate the request
7. RbacFilter: Authorise the request
8. RequestEnrichmentFilter: Enrich the request with userInfo & correlationId

**Error-Filter**

This filter handles all the errors shown either during the processing of the request or from the downstream service.

## Gateway Routes & Properties Configuration

Currently, the gateway routes are generated based on whether the gateway flag has been enabled by a service at the helm chart and based on this flag a go script is run in the Init container which automatically generates the relevant properties for all the services opted in for gateway.

At the service helm chart level, there are options to customise the RateLimiting by defining the following properties.

* gateway-replenishRate:&#x20;
* gateway-burstCapacity:
* gateway-keyResolver: \[ ipKeyResolver or userKeyResolver ] If not provided spring will use the default principalKeyResolver automatically

<figure><img src="../../.gitbook/assets/image (2) (2).png" alt=""><figcaption></figcaption></figure>

If Rate limiting properties are provided for a particular service then a default rate limiting will be applied to the services controlled at the gateway level.

