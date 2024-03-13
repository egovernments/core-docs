# Gateway: The Spring Cloud Way

## Overview

To ensure Long Term Support for the DIGIT platform, we're auditing our core services for outdated dependencies. The present API gateway, built using Netflix Zuul, has few dependencies that will become obsolete soon. Hence we are building a new Gateway on top of spring cloud gateway to address this issue.&#x20;

**What is Spring Cloud Gateway and how is it different from Zuul?**

Spring Cloud Gateway and Zuul serve similar purposes as API gateways but differ in their underlying architecture and design philosophies. Spring Cloud Gateway is well-suited for modern, reactive applications, while Zuul is more established and may be preferred in traditional, blocking I/O environments. Ultimately, the choice between the two depends on the specific requirements.

**Navigating the new Gateway codebase**&#x20;

The new Gateway codebase is well modularised where each module hold similar files and named that makes it self explanatory as it identifies the tasks each actor performs. Below is a snapshot of the current directory structure.&#x20;

![](<../../../.gitbook/assets/image (315).png>)&#x20;

**Config**: It contains the configuration related files for example Application Properties etc.

**Constants**: It contains the constants referenced frequently within the codebase. Add any constant string literal here and then access it via this file.

**Filters**: This folder is the heart of the API gateway  since it contains all the **PRE** , **POST** , **ERROR** filters. For those who are new to filters: Filters intercept incoming requests and outgoing responses, allowing developers to apply various functionalities such as authentication, authorisation, rate limiting, logging, and transformation to these requests and responses.

**Model**: It contains the P.O.J.O required in the gateway.

**Producer**: It contains code related to pushing data onto Kafka.

**Rate limiters**: It contains files related to initialising the relevant bean for custom rate limiting.

**Utils**: It contains the helper function which can be reused across the project.&#x20;

This introduction provides you with the basics of the gateway and its project structure, offering a high-level overview of the Gateway's functionality.

Whenever a request is received the Gateway checks if it matches with any pre-defined routes. In case it does, it applies a series of filters wherein each filter performs certain validation or enrichment. We will discuss the exact order of filters later on. For the time being it is enough to understand that it checks the restricted routes for proper authentication and authorisation. Although there is an option to whitelist some of the APIs as open endpoint or mixed-mode endpoint so that authentication or authorisation can be skipped for certain APIs.

Whenever a request is received by a gateway it first checks for existing route definition that matches the request path. If a match is found, it starts executing the pre - filters in the given order.

**Pre - Filter**

1. RequestStartTimerFilter :  Sets request start time&#x20;
2. CorrelationIdFilter : Generate and sets a correlationId in each request so as to help tracking it in downstream service
3. AuthPreCheckFilter : Checks for if Authorisation has to be performed
4. PreHookFilter : Sends a pre-hook request
5. RbacPreFilter : Checks if Authentication has to be performed or not
6. AuthFilter : Authenticate the request
7. RbacFilter : Authorise the request
8. RequestEnrichmentFilter : Enrich the request with userInfo & correlationId

**Error - Filter**

This filter handles all the error that are throw either during processing the request or from the downstream service.

## Gateway Routes & Properties Configuration

Currently the gateway routes are generated based on the whether the gateway flag has been enabled by a service at hem chart and based on this flag a go script is run in Init container which automatically generated the relevant properties for all the services opted in for gateway.

At service helm chart level there are options to customise the RateLimiting by defining following properties

* gateway-replenishRate:&#x20;
* gateway-burstCapacity:
* gateway-keyResolver: \[ ipKeyResolver or userKeyResolver ] if not provided spring will use the default principalKeyResolver automatically

<figure><img src="../../../.gitbook/assets/image (2) (2).png" alt=""><figcaption></figcaption></figure>

If Rate limiting properties are provided for a particular service then a default rate limiting will be applied to those service which controlled at the gateway level.













