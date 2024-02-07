---
description: API interface details
---

# API Gateway

## Overview

API Gateway provides a unified interface for a set of microservices so that clients do not need to know about all the details of microservices internals.&#x20;

**DIGIT** uses [**Netflix** **ZUUL**](../../core-services/zuul-service.md) as API Gateway. It serves as an edge service that proxies requests to multiple back-end services. It provides a unified “front door” to our ecosystem. This allows any browser, mobile app or any other user interface to consume underlying services.

## Reasons For Using Zuul

1. Easier API interface for clients: Zuul provides a simplified and standardized interface for clients to interact with microservices, streamlining the process of accessing various functionalities.
2. Protection of internal microservices structure: Zuul acts as a gateway, preventing the exposure of the internal microservices architecture to external clients, enhancing security and maintaining system integrity.
3. Facilitates microservices refactoring: Zuul allows for seamless refactoring of microservices without requiring clients to modify their consuming logic, ensuring flexibility and minimizing disruptions during updates or changes.
4. Centralization of cross-cutting concerns: Zuul enables the centralization of common functionalities such as security, monitoring, and rate limiting, simplifying management and ensuring consistent implementation across microservices.

## Zuul Components

Zuul has mainly four types of filters that enable us to intercept the traffic in different timelines of the request processing for any particular transaction. We can add any number of filters for a particular URL pattern.

<img src="../../../.gitbook/assets/file.excalidraw.svg" alt="" class="gitbook-drawing">

## Zuul Features

* Microservice authentication and security
* Authorization
* API Routing
* Open APIs using Whitelisting
* RBAC filter
* Logout filter for the finance module
* Property module tax calculation filter for firecess
* Request enrichment filter:
  * Addition of co-relation id
  * Addition of authenticated user’s userinfo to requestInfo.
* Error filter:
  * Error response formatting

Following are the feature enhancements in the latest version.

* Validation filter to check if a tenant of a particular module is enabled or not.
* Multitenancy Validation Filter. Take the tenant id from the Req body or Query Param and validate against the additional tenant role or primary tenant role.
* DevOps efficiency: API response time logging and sending notifications if it is taking more time.

