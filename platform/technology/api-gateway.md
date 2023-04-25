# API Gateway

## Overview

API Gateway provides a unified interface for a set of microservices so that clients do not need to know about all the details of microservices internals.&#x20;

**DIGIT** uses [**Netflix** **ZUUL**](../core-services/zuul-service.md) as API Gateway. It serves as an edge service that proxies requests to multiple back-end services. It provides a unified “front door” to our ecosystem. This allows any browser, mobile app or any other user interface to consume underlying services.

## Reasons For Using Zuul

* Provides easier API interface to clients
* Can be used to prevent exposing the internal micro-services structure to the outside world.
* Allows to refactor microservices without forcing the clients to refactor consuming logic
* Can centralize cross-cutting concerns like security, monitoring, rate limiting etc

## Zuul Components

Zuul has mainly four types of filters that enable us to intercept the traffic in different timelines of the request processing for any particular transaction. We can add any number of filters for a particular URL pattern.

* **pre-filters** – are invoked before the request is routed.
* **post filters** – are invoked after the request has been routed.
* **route filters** – are used to route the request.
* **error filters** – are invoked when an error occurs while handling the request.

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

