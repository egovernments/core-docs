---
description: Deployment With Spring Cloud
---

# API Gateway

## Overview

We are updating our core services to remove outdated dependencies and ensure long-term support for the DIGIT platform. The current API gateway uses Netflix Zuul, which has dependencies that will soon be obsolete. To address this, we are building a new gateway using Spring Cloud Gateway.

**What is Spring Cloud Gateway and how is it different from Zuul?**

Spring Cloud Gateway and Zuul both function as API gateways but differ in architecture and design. Spring Cloud Gateway is ideal for modern, reactive applications, while Zuul is better suited for traditional, blocking I/O environments. The choice between them depends on your specific needs.

**Navigating the new Gateway codebase**&#x20;

The new Gateway codebase is well-organized, with each module containing similar files and names. This makes it easy to understand the tasks each part performs. Below is a snapshot of the current directory structure.

![](<../../../.gitbook/assets/image (315).png>)&#x20;

**Config**: It contains the configuration-related files for example Application Properties etc.

**Constants**: It contains the constants referenced frequently within the codebase. Add any constant string literal here and then access it via this file.

**Filters**: This folder is the heart of the API gateway since it contains all the **PRE**, **POST**, and **ERROR** filters. For those new to filters: Filters intercept incoming and outgoing requests, allowing developers to apply various functionalities such as authentication, authorisation, rate limiting, logging, and transformation to these requests and responses.

**Model**: contains the P.O.J.O required in the gateway.

**Producer**: contains code related to pushing data onto Kafka.

**Rate limiters** contain files for initialising the relevant bean for custom rate limiting.

**Utils**: contains the helper function which can be reused across the project.&#x20;

The above paragraphs provide a basic overview of the gateway's functionality and project structure.

When a request is received, the gateway checks if it matches any predefined routes. If a match is found, the request goes through a series of filters, each performing specific validation or enrichment tasks. The exact order of these filters is discussed later.

The gateway also ensures that restricted routes have proper authentication and authorization. Some APIs can be whitelisted as open or mixed-mode endpoints, allowing them to bypass authentication or authorization.

Upon receiving a request, the gateway first looks for a matching route definition. If a match is found, it starts executing the pre-filters in the specified order.

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

This filter handles all the errors shown either during the request processing or from the downstream service.

## Gateway Routes & Properties Configuration

There are two ways to configure Rate Limits in Gateway

1. Default Rate Limiting
2. Service Level Rate Limiting

### Default Rate Limiting

Default rate limiting sets a standard limit on the number of requests that can be made to the gateway within a specified time frame. This limit applies to all services unless specific rate limits are configured at the service level.

Add these properties in **Values.YAML** of Gateway helm file and then configure the values as per the use case. Read [Configuring Gateway Rate Limiting](configuring-gateway-rate-limiting.md) for more information about these properties.

```yaml
  - name: SPRING_DATA_REDIS_DEFAULT_REPLENISHRATE
    value: "10"
  - name: SPRING_DATA_REDIS_DEFAULT_BURSTCAPACITY
    value: "10"
```

### Service Level Rate Limiting

Service level rate limiting allows you to set specific rate limits for individual services. This means each service can have its request limits, tailored to its unique needs and usage patterns, providing more granular control over traffic management.

If you want to define rate limiting for each service differently you can do so by defining these properties in the **Values.YAML** of the respective service. Read [Configuring Gateway Rate Limiting](configuring-gateway-rate-limiting.md) for more information about these properties.

**Note**: We currently provide two options for keyResolver and if none of them is specified the spring cloud will take a default go `PrincipalNameKeyResolver` which retrieves the `Principal` from the `ServerWebExchange` and calls `Principal.getName()`.

1. `ipKeyResolver :  Resolves key based on ip address of the request`
2. `userKeyResolver : Resolves key based on use UUID of the request`

```yaml
service:
  additionalAnnotations: |
    gateway-burstCapacity: "1"
    gateway-keyResolver: "ipKeyResolver"
    gateway-replenishRate: "2"
```

To enable gateway routes, a service must activate the gateway flag in the Helm chart. Based on this flag, a Go script runs in the Init container, automatically generating the necessary properties for all services using the gateway.

```yaml
ingress:
  enabled: true
  zuul: true
  context: "egov-location"
```

**NOTE**: Restart the Gateway after making changes in service **Values.YAML** so that it can pick up the changes.
