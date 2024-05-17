# Internal Gateway

## Overview <a href="#overview" id="overview"></a>

The Internal Gateway is a simplified Zuul service which provides an easy integration of services running different namespaces of a multistate instance, the clients need not know about all the details of microservices and their namespace in the K8s setup.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before you proceed with the documentation, make sure the following pre-requisites are met -

* _Java 17_
* API Gateway

## Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

* Provides an easier API interface between services running in different tenants(namespaces) where direct access between microservices is blocked by default.
* Allows refactoring microservices independently without forcing the clients to refactor integrating logic with other tenants.

### Zuul Components <a href="#zuul-components" id="zuul-components"></a>

Route filter - a single route filter enables the routing based on tenatId from the HTTP header of the incoming requests.

## Configuration Details <a href="#configuration" id="configuration"></a>

### **Routing Property**

For each service, the below-mentioned property has to be added in `internal-gateway.json`

```json
{
  "/egov-mdms-service/.*": {
    "in.statea": "http://egov-mdms-service.statea:8080",
    "in.stateb": "http://egov-mdms-service.stateb:8080",
    "in": "http://egov-mdms-service:8080"
  },
  "/pt-calculator-v2/.*": {
    "in.statea": "http://pt-calculator-v2.statea:8080",
    "in.stateb": "http://pt-calculator-v2.stateb:8080",
    "in": "http://pt-calculator-v2.digit:8080"
  },
  "/property-services/.*": {
    "in.stateb": "http://property-services.digit:8080",
    "in.statea": "http://property-services.digit:8080"
  },
  "/billing-service/.*": {
    "in.stateb": "http://billing-service.digit:8080",
    "in.statea": "http://billing-service.digit:8080"
  },
  "/egov-searcher/.*": {
    "in.statea": "http://egov-searcher.statea:8080",
    "in.stateb": "http://egov-searcher.stateb:8080"
  },
  "/dashboard-analytics/.*": {
    "in.statea": "http://dashboard-analytics.statea:8080",
    "in.stateb": "http://dashboard-analytics.stateb:8080"
  }
}
```

### Sequence Diagram  <a href="#sequence-diagram" id="sequence-diagram"></a>

Open&#x20;



&#x20;
