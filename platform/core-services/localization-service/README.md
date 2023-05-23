# Localization Service

### Overview <a href="#overview" id="overview"></a>

An eGov core application which provides locale-specific components and translating text for the eGov group of applications.

### Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

1. Prior knowledge of Java/J2EE.
2. Prior knowledge of Spring Boot.
3. Prior knowledge of REST APIs and related concepts like path parameters, headers, JSON etc.
4. Prior knowledge of Redis and Postgres.

## Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

The localization application stores the locale data in the format of key and value along with the module, tenantid and locale. The module defines which application of eGov owns the locale data and tenantId does the same for the tenant, locale is the specific locale for which data is being added. &#x20;

The request can be posted through the post API with the above-mentioned variables in the request body.

Once posted the same data can be searched based on the module, locale and tenantId as keys.

The data posted to the localization service is permanently stored in the database and loaded into the Redis cache for easy access and every time new data is added to the application the Redis cache will be refreshed.

## Deployment Details <a href="#deployment-details" id="deployment-details"></a>

1. Deploy the latest version of the Localization Service.
2. Add role-action mapping for APIs.

## Integration Details <a href="#integration" id="integration"></a>

### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

The localization service is used to store **key-value pairs** of metadata in different languages for all miscellaneous/ad-hoc services which citizens avail from ULBs.

### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

* Can perform service-specific business logic without impacting the other module.
* Provides the capability of having multiple languages in the module.

### Integration Steps <a href="#steps-to-integration" id="steps-to-integration"></a>

1. To integrate, the host of the localization-services module should be overwritten in the helm chart.
2. `/localization/messages/v1/_upsert` should be added as the create endpoint for creating localization key-value pairs in the system
3. `/localization/messages/v1/_search` should be added as the search endpoint. This method handles all requests to search existing records depending on different search criteria

### Postman Collection <a href="#postman-collection" id="postman-collection"></a>

[https://www.getpostman.com/collections/a140e7426ab4419ed5b5](https://www.getpostman.com/collections/a140e7426ab4419ed5b5)

### Swagger Contract <a href="#swagger-contract" id="swagger-contract"></a>

[https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/DIGIT-OSS/master/core-services/docs/localisation-contract.yml](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/DIGIT-OSS/master/core-services/docs/localisation-contract.yml)\
