---
description: Adding data to MDMS-V2
---

# MDMS - V2

## Overview

MDMS v2 exposes APIs for defining schemas, searching schemas and then adding master data against these defined schemas. The data is now stored in PostgreSQL tables rather than in GitHub. MDMS v2 currently also exposes v1 search API which will fetch data from the database in the same format as MDMS v1 search API to maintain backward compatibility.&#x20;

## **Functionalities**

1. **Create schema -** MDMS-v2 allows you to create your schema with all the validations and properties supported by JSON schema draft 07. JSON Schema Draft 07 version of the JSON Schema specification provides a standardized way to validate the data format and content of JSON files.
2. **Search schema -** MDMS v2 contains an API that allows users to search schemas using criteria like the tenantid, schema code, and unique identifiers.
3. **Create data -** MDMS v2 allows users to create data as per the defined schemas.&#x20;
4. **Search data -** MDMS v2 provides two search APIs - v1 and v2.  The v1 search API is fully backwards compatible.
5. **Update data -** MDMS v2 allows users to update the master data fields.
6. **Fallback functionality -** Both search APIs have implemented fallback where if data is not found for a particular tenant, the services fall back to the parent tenant(s) and return the response. If data is not found even for the parent tenant, an empty response is sent to the user.

## Steps

### Steps to create schema and data

1. **Create schema -** below is a sample schema definition for your reference -

```json
  "SchemaDefinition": {
    "tenantId": "pb",
    "code": "TradeLicense.TradeSubType",
    "description": "Trade sub-type which is a child of Trade type",
    "definition": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "properties": {
        "name": {
          "type": "string",
          "pattern": "^[A-Za-z]+$"
        },
        "code": {
          "type": "string"
        },
        "tradeTypeCode": {
          "type": "string"
        }
      },
      "required": [
        "name",
        "code",
        "tradeTypeCode"
      ],
      "x-unique": [
        "name"
      ],
      "x-ref-schema": [
        {
          "fieldPath": "tradeTypeCode",
          "schemaCode": "TradeLicense.TradeType"
        }
      ]
    },
    "isActive": true
  }
```

To create a basic schema definition, define the following keywords:

* **$schema**: specifies which draft of the JSON Schema standard the schema adheres to.
* **title and description**: state the intent of the schema. These keywords don’t add any constraints to the data being validated.
* **type**: defines the first constraint on the JSON data.

**Reference** - [<img src="https://json-schema.org/favicon.ico" alt="" data-size="line">JSON Schema - Creating your first schema](https://json-schema.org/learn/getting-started-step-by-step#create)

Now, properties can be added under the schema definition. In JSON Schema terms, properties is a validation keyword. When you define properties, you create an object where each property represents a key in the JSON data that’s being validated. You can also specify the required properties described in the object.

**Reference** - [<img src="https://json-schema.org/favicon.ico" alt="" data-size="line">JSON Schema - Creating your first schema](https://json-schema.org/learn/getting-started-step-by-step#define)

Additionally, we have two keys which are not part of standard JSON schema attributes -

* **x-unique**: specifies the fields in the schema utilizing which a unique identifier for each master data will be created.
* **x-ref-schema**: specifies referenced data. This is useful in scenarios where the parent-child relationship needs to be established in the master data. For example, Trade Type can be a parent master data to Trade Sub Type. In the example provided, the "field path" indicates the JsonPath of the attribute in the master data that holds the unique identifier of the referenced parent. The "schema code" specifies the schema against which the referenced master data must be validated for existence.

2. **Create data:** MDMS v2 enables users to create data per the defined schemas. Below is an example of data for the specified schema:-

```json
  "Mdms": {
    "tenantId": "pb",
    "schemaCode": "TradeLicense.TradeSubType",
    "data": {
      "name": "Electronics",
      "code": "ELECTRONICS",
      "tradeTypeCode": "GOODS.MANUFACTURE"
    },
    "isActive": true
  }
```

This JSON data adheres to the defined schema structure and can be used as a reference when creating data within MDMS v2.

### Add data to new MDMS

1. Define the schema for the master that you want to promote to MDMS v2.
2. Make sure that the schema includes a unique field. This field can also be made composite if needed, ensuring that the data added against that schema remains unique.
3. If the data does not have the scope for having unique identifiers, for example, complex masters like - [https://github.com/egovernments/health-campaign-mdms/blob/QA/data/default/health/project-task-configuration.json](https://github.com/egovernments/health-campaign-mdms/blob/QA/data/default/health/project-task-configuration.json) - consider adding a redundant field which can serve as the unique identifier.
4. Hit the following API endpoint to create schema in the system - _/mdms-v2/schema/v1/\_create_
5. Verify the created schema by searching for it using the following API endpoint - _/mdms-v2/schema/v1/\_search_
6. Create the data for the specified schema using the following API endpoint - _/mdms-v2/v2/\_create/{schemaCode}_
7. Verify the created data by searching for it using the following API endpoint - _/mdms-v2/v2/\_search_

\
