# Localization Service

### Overview <a href="#overview" id="overview"></a>

An eGov core application which provides locale-specific components and translating text for the eGov group of applications.

### Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

1. Prior Knowledge of Java/J2EE.
2. Prior Knowledge of Spring Boot.
3. Prior Knowledge of REST APIs and related concepts like path parameters, headers, JSON etc.
4. Prior knowledge of Redis and postgres.

### Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

The localization application stores the locale data in the format of key and value along with the module, tenantid and locale. Module defines which application of eGov owns the locale data and tenantId does the same for the tenant, locale is the specific locale for which data is being added. &#x20;



The request can be posted through the post API with the above mentioned variables in the request body.



Once posted the same data can be searched based on the module, locale and tenantId as keys.



The Data posted to localization service will be permanently stored in the database and will be loaded in to redis cache for easy access and every time new data is added in to the application the redis cache will be refreshed.

### Deployment Details <a href="#deployment-details" id="deployment-details"></a>

1. Deploy the latest version of Localization Service.
2. Add Role-Action mapping for API’s.

### Integration <a href="#integration" id="integration"></a>

#### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

The Localization service is used to store **key-value pairs** of meta data in different languages for all miscellaneous / adhoc services which citizens avail from ULBs.

#### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

* Can perform service-specific business logic without impacting the other module.
* Provides the capability of having multiple languages in module.

#### Steps to Integration <a href="#steps-to-integration" id="steps-to-integration"></a>

1. To integrate, host of localization-services module should be overwritten in helm chart.
2. `/localization/messages/v1/_upsert` should be added as the create endpoint for creating localization key value pairs in the system
3. `/localization/messages/v1/_search` should be added as the search endpoint .This method handles all requests to search existing records depending on different search criteria

&#x20;

#### Postman Collection <a href="#postman-collection" id="postman-collection"></a>

[https://www.getpostman.com/collections/a140e7426ab4419ed5b5](https://www.getpostman.com/collections/a140e7426ab4419ed5b5)

#### Swagger Contract <a href="#swagger-contract" id="swagger-contract"></a>

[https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/DIGIT-OSS/master/core-services/docs/localisation-contract.yml](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/DIGIT-OSS/master/core-services/docs/localisation-contract.yml)

\
