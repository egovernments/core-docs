# Zuul

### Overview <a href="#overview" id="overview"></a>

An API Gateway provides a unified interface for a set of microservices so that clients do not need to know about all the details of microservice internals.

DIGIT uses Zuul as an edge service that proxies request to multiple back-end services. It provides a unified “front door” to our ecosystem. This allows any browser, mobile app or other user interface to consume underlying services.

### Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before you proceed with the documentation, make sure the following pre-requisites are met -

* _Java 8_
* egov-user service is running
* egov-accesscontrol service is running

#### Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

* Provides easier API interface to clients
* Can be used to prevent exposing the internal micro-services structure to the outside world.
* Allows to refactor microservices without forcing the clients to refactor consuming logic
* Can centralize cross-cutting concerns like security, monitoring, rate limiting etc

#### Components <a href="#zuul-components" id="zuul-components"></a>

Zuul has mainly four types of filters that enable us to intercept the traffic in the different timelines of the request processing for any particular transaction. We can add any number of filters for a particular URL pattern.

* pre-filters – are invoked before the request is routed.
* post filters – are invoked after the request has been routed.
* route filters – are used to route the request.
* error filters – are invoked when an error occurs while handling the request.

#### Features <a href="#zuul-features" id="zuul-features"></a>

* Microservice authentication and security
* Authorization
* API Routing
* Open APIs using Whitelisting
* RBAC filter
* Logout filter for the finance module
* Property module tax calculation filter for firecess
* Request enrichment filter:
* Addition of co-relation id
* Addition of authenticated user (userinfo) to requestInfo.
* Error filter:
  * Error response formatting
* Validation Filter to check if a tenant of a particular module is enabled or not.
* Multitenancy Validation Filter. Take the tenant id from the Req body or Query Param and validate against the additional tenant role or primary tenant role.
* DevOps efficiency: API response time for logging and sending notifications if it is taking more time.
* Rate Throttling

### Configuration Details <a href="#configuration" id="configuration"></a>

**Routing Property**

For each service, below mentioned property has to be add-in `routes.properties`

Copy

```
-zuul.routes.{serviceName}.path = /{context path of service}/**
-zuul.routes.{serviceName}.stripPrefix = {true/false}
-zuul.routes.{serviceName}.url = {service host name}
```

**Rate Limiting Property**

For endpoints which require rate throttling, below mentioned property has to be added in `limiter.properties`

Copy

```
-zuul.ratelimit.policy-list.{serviceName}[0].limit={request number limit per refresh interval window} 
-zuul.ratelimit.policy-list.{serviceName}[0].quota={request time limit per refresh interval window (in seconds)} 
-zuul.ratelimit.policy-list.{serviceName}[0].refresh-interval={refresh interval in seconds} 
-zuul.ratelimit.policy-list.{serviceName}[0].type[0]=url={url of API endpoint
-zuul.ratelimit.policy-list.{serviceName}[0].type[1]={type of throttling eg: user, origin etc.}
```

### Deployment Details <a href="#deployment-details" id="deployment-details"></a>

1. Deploy the latest version of the Zuul service.
2. Add Zuul routing context paths and service hostname in the configuration.

### Integration Details <a href="#integration" id="integration"></a>

#### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

The Zuul service is used to act as an API gateway for services which citizens avail from ULBs.

#### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

* Can perform service-specific business logic without impacting the other module.
* Provides the capability of routing and authorizing users for accessing resources.

#### Integration Steps <a href="#steps-to-integration" id="steps-to-integration"></a>

1. To integrate, the host of the Zuul module should be overwritten in the helm chart.
