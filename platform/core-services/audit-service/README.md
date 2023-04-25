# Audit Service

### Overview <a href="#overview" id="overview"></a>

_The objective of audit service is listed as below -_

1. To provide a one-stop framework for signing data i.e. creating an immutable data entry to track activities of an entity. Whenever an entity is created/updated/deleted the operation is captured in the data logs and is digitally signed to protect it from tampering.

### Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

1. Prior Knowledge of Java/J2EE.
2. Prior Knowledge of SpringBoot.
3. Prior Knowledge of PostgresSQL.
4. Prior Knowledge of REST APIs and related concepts like path parameters, headers, JSON etc.

### Setup And Key Functionalities <a href="#setup-and-key-functionalities" id="setup-and-key-functionalities"></a>

Audit service will be parsing all the persister configs so that it can process data received by the persister and create audit logs out of it.

**Setup:**

1. Step 1: Add the following metrics to the existing persister configs -

{% code lineNumbers="true" %}
```
isAuditEnabled: true
module: PGR
objecIdJsonPath: $.id
tenantIdJsonPath: $.tenantId
transactionCodeJsonPath: $.transactionCode
auditAttributeBasePath: $.service
```
{% endcode %}

2\. Step 2: If a custom implementation of `ConfigurableSignAndVerify` interface is present, provide the signing algorithm implementation name as a part of `audit.log.signing.algorithm` property. For example, if the signing algorithm is HMAC, the property will be set as follows -

{% code lineNumbers="true" %}
```
audit.log.signing.algorithm=HMAC
```
{% endcode %}

3\. Step 3: Set `egov.persist.yml.repo.path` this property to the location of persister configs.

4\. Step 4: Run the audit-service application along with persister service.

**Definitions:**

1. Config file - A YAML (xyz.yml) file which contains persister configuration for running audit service.
2. API - A REST endpoint to post audit logs data.

**Functionality:**

1. When audit-service create API is hit, it will validate request size, keyValueMap and operationType.
2. Upon successful validation, it will choose the configured signer and sign entity data.
3. Once audit logs are signed and ready, it will send it to `audit-create` topic.
4. Persister will listen on this topic and persist the audit logs.

### Deployment Details <a href="#deployment-details" id="deployment-details"></a>

1. Add the required keys for enabling audit service in persister configs.
2. Deploy the latest version of Audit service and Persister service.
3. Add Role-Action mapping for API’s.

### Integration <a href="#integration" id="integration"></a>

#### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

The audit service is used to push signed data for tracking each and every create/modify/delete operation done on database entities.

#### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

* Can be used to have tamper proof audit logs for all database transactions.
* Replaying events in chronological order will lead to current state of entity in the database.

#### Steps to Integration <a href="#steps-to-integration" id="steps-to-integration"></a>

1. To integrate, host of audit-service module should be overwritten in helm chart.
2. `audit-service/log/v1/_create` should be added as the create endpoint for the config added.
3. `audit-service/log/v1/_search` should be added as the search endpoint for the config added.

### API Details <a href="#api-details" id="api-details"></a>

**1. URI**: The format of the API to be used to create audit logs using audit-service is as follows:  `audit-service/log/v1/_create`

**Body**: Body consists of 2 parts: RequestInfo and AuditLogs.

Sample Request Body -

{% code lineNumbers="true" %}
```
{
    "RequestInfo": {
        "apiId": "asset-services",
        "ver": null,
        "ts": null,
        "action": null,
        "did": null,
        "key": null,
        "msgId": "search with from and to values",
        "authToken": "83a1cfb3-6fde-4406-9ee1-622b3ecc7dab"
    },
    "AuditLogs": [
        {
            "userUUID": "11b0e02b-0145-4de2-bc42-c97b96264807",
            "module": "PGR",
            "tenantId": "pb.amritsar",
            "transactionCode": "PGR.CREATE",
            "changeDate": 1657104693726,
            "entityName": "eg_pgr_service",
            "objectId": "c8c901da-61e9-4cd5-89f7-7560997922b7",
            "keyValueMap": {
                "id": "89651651-841a-4b8c-a503-f5d4bb10f4d5",
                "tenantId": "pb.amritsar",
                "assemblyConstituency": "AMC",
                "applicationNumber": "c8c901da-61e9-4cd5-89f7-7560997922b7",
                "applicantId": null,
                "dateSinceResidence": 1590825279,
                "createdBy": "11b0e02b-0145-4de2-bc42-c97b96264807",
                "lastModifiedBy": "11b0e02b-0145-4de2-bc42-c97b96264807",
                "createdTime": 1657104693312,
                "lastModifiedTime": 1657104693312
            },
            "operationType": "CREATE"
        },
        {
            "userUUID": "11b0e02b-0145-4de2-bc42-c97b96264807",
            "module": "PGR",
            "tenantId": "pb.amritsar",
            "transactionCode": "PGR.CREATE",
            "changeDate": 1657104693732,
            "entityName": "eg_pgr_address",
            "objectId": "c8c901da-61e9-4cd5-89f7-7560997922b7",
            "keyValueMap": {
                "id": "84cbe5d1-6ee8-4379-a0c4-0e2a5c94689d",
                "tenantId": "pb.amritsar",
                "doorNo": "1010",
                "latitude": null,
                "longitude": null,
                "buildingName": "Avigna Residence",
                "addressId": null,
                "addressNumber": "34 GA",
                "type": "RESIDENTIAL",
                "addressLine1": "KP Layout",
                "addressLine2": "",
                "landmark": "Petrol pump",
                "street": "12th Main",
                "city": "Amritsar",
                "locality": "New Amritsar Locality",
                "pincode": "143501",
                "detail": "",
                "registrationId": "89651651-841a-4b8c-a503-f5d4bb10f4d5"
            },
            "operationType": "CREATE"
        }
    ]
}
```
{% endcode %}



**2.** **URI**: The format of the API to be used to search audit logs using audit-service is as follows:  `audit-service/log/v1/_search`

**Body**: Body consists RequestInfo and search criteria is passed as query params.

Sample curl for search -

```
curl --location --request POST 'https://dev.digit.org/audit-service/log/v1/_search?offset=0&limit=10&tenantId=pb.amritsar&objectId=c8c901da-61e9-4cd5-89f7-7560997922b7' \
--header 'Content-Type: application/json' \
--data-raw '{
    "RequestInfo": {
        "apiId": "asset-services",
        "ver": null,
        "ts": null,
        "action": null,
        "did": null,
        "key": null,
        "msgId": "search with from and to values",
        "authToken": "83a1cfb3-6fde-4406-9ee1-622b3ecc7dab"
    }
}'
```



&#x20;

### Postman Collection - [Audit Service Postman Collection](https://www.getpostman.com/collections/27d92894fa32f72b83f5) <a href="#postman-collection-audit-service-postman-collection" id="postman-collection-audit-service-postman-collection"></a>
