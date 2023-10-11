---
description: TBD
---

# Section 4: Integrating With Billing & Payment

### What is a calculator?

In governments, each region, city or state has custom rates and charges for the same domain. For example, birth certificate registration rates may differ from city to city and the way it is computed can also vary. This cannot be generalised into a platform service. However, billing is a generic platform service.&#x20;

The way DIGIT solves for this is to "unbundle" the problem and separate out billing from calculations. A customisable service called a "calculator" is used for custom calculation. The calculator then calls the billing service to generate the bill. Each service/module ships with a "default" calculator which can then be customised for that city.

Code of developer guide till this stage is available [here.](https://github.com/egovernments/DIGIT-Dev/blob/birth-registration-service/municipal-services/birth-registration/birth-registration-api-spec.yaml)\
Postman collection of btr-calculator is available [here.](https://github.com/egovernments/DIGIT-OSS/blob/master/tutorials/backend-developer-guide/btr-calculator/birth-registration-calculator-stage-4-postman-collection.json)\
Postman collection of btr-services is availble [here.](https://github.com/egovernments/DIGIT-Dev/blob/00a5537fb35a874f5d11530d2f52e3214f4a7608/tutorials/backend-developer-guide/btr-services/birth-registration-service-stage-4-postman-collection.json)
