---
description: Steps to migrate MDMS data to enable use of workbench UI v1.0
---

# MDMS Migration

## Overview

Follow the steps below to migrate the MDMS data to enable the use of Workbench UI v1.0.

## Steps

### 1. **Generate Schema**

Follow the steps below to generate the schema for Workbench UI v1.0:

1. **Clone the migration utility:** Start by cloning the migration utility from this [link](https://github.com/egovernments/Digit-Core/tree/core-2.9-lts-mvn-check/utilities/mdms-migration-toolkit).
2. **Clone the MDMS Repository**: Start by cloning the MDMS repository on your local machine.
3. **Configure `application.properties`**: Open the `application.properties` file in the workbench utility and configure it as follows:
   * Add the hostname of the environment.
   * Add the MDMS cloned folder path in the `egov.mdms.conf.path`.
   * Add `master-config.json` in `masters.config.url`.
   * Specify the output folder path for the created schema in `master.schema.files.dir`.
4. **Port-forward MDMSv2 Service**: Port-forward the MDMSv2 service to port 8094.
5.  **Run the Curl Command**:

    ```sh
    shCopy codecurl -L -X POST 'localhost:8080/mdms-migration-toolkit/schema/v1/_generate'
    ```

    This command generates the schema and saves it in the path specified by `master.schema.files.dir`.

### **2. Update Schema**

After generating the schema, you may need to update it with additional attributes:

*   **Add `x-unique` Attribute**: This defines unique fields in the schema.

    ```json
    "x-unique": ["description"]
    ```
*   **Add `x-ref-schema` Attribute**: Use this attribute if a field within MDMS data needs to refer to another schema.

    ```json
    "x-ref-schema": [{"fieldPath": "billingType","schemaCode": "WaterCharges.BillingType"}]
    ```
* **Set Default Value for a Field**: Use the `default` keyword to set default values.

### **3. Migrate Schema**

To migrate the schema, use the following curl command:

```sh
curl -L 'localhost:8080/mdms-migration-toolkit/schema/v1/_migrate' \
-H 'Content-Type: application/json' \
-d '{
  "schemaMigrationCriteria": {
    "moduleName": "PropertyTax",
    "tenantId": "pb"
  },
  "requestInfo": {
    "apiId": "asset-services",
    "ver": null,
    "ts": null,
    "action": null,
    "did": null,
    "key": null,
    "msgId": "search with from and to values",
    "authToken": "7a9fc02a-bd6e-4e42-bd43-519b9e357bae",
    "correlationId": null,
    "userInfo": {
      "id": 878483,
      "uuid": "3059806b-3059-4724-8ae1-d3f4e12686ff",
      "userName": "8080800000",
      "name": "HRMS-ADMIN-TESTING",
      "mobileNumber": "8080800000",
      "emailId": null,
      "locale": null,
      "type": "EMPLOYEE",
      "roles": [
        {
          "name": "MDMS ADMIN",
          "code": "MDMS_ADMIN",
          "tenantId": "pb"
        },
        {
          "name": "Localisation admin",
          "code": "LOC_ADMIN",
          "tenantId": "pb"
        },
        {
          "name": "Employee",
          "code": "EMPLOYEE",
          "tenantId": "pb"
        }
      ],
      "active": true,
      "tenantId": "pb",
      "permanentCity": null
    }
  }
}'
```

### **4. Migrate Data**

To migrate data for a specific master/module name, use the following curl command:

```sh
curl -L 'localhost:8080/mdms-migration-toolkit/data/v1/_migrate' \
-H 'accept: */*' \
-H 'Content-Type: application/json' \
-d '{
  "masterDataMigrationCriteria": {
    "moduleName": "PropertyTax",
    "tenantId": "pb"
  },
  "requestInfo": {
    "apiId": "asset-services",
    "ver": null,
    "ts": null,
    "action": null,
    "did": null,
    "key": null,
    "msgId": "search with from and to values",
    "authToken": "7a9fc02a-bd6e-4e42-bd43-519b9e357bae",
    "correlationId": null,
    "userInfo": {
      "id": 878483,
      "uuid": "3059806b-3059-4724-8ae1-d3f4e12686ff",
      "userName": "8080800000",
      "name": "HRMS-ADMIN-TESTING",
      "mobileNumber": "8080800000",
      "emailId": null,
      "locale": null,
      "type": "EMPLOYEE",
      "roles": [
        {
          "name": "MDMS ADMIN",
          "code": "MDMS_ADMIN",
          "tenantId": "pb"
        },
        {
          "name": "Localisation admin",
          "code": "LOC_ADMIN",
          "tenantId": "pb"
        },
        {
          "name": "Employee",
          "code": "EMPLOYEE",
          "tenantId": "pb"
        }
      ],
      "active": true,
      "tenantId": "pb",
      "permanentCity": null
    }
  }
}'
```

### 5. Schema Sample

Here is an example of a schema:

```json
{
  "id": "060776ef-2eff-4f76-82ba-9b40cfad1c6c",
  "tenantId": "pb",
  "code": "ws-services-calculation.WCBillingSlab",
  "description": "ws-services-calculation WCBillingSlab",
  "definition": {
    "type": "object",
    "allOf": [
      {
        "if": {
          "required": ["connectionType"],
          "properties": {
            "connectionType": {"const": "Metered"}
          }
        },
        "then": {
          "required": ["slabs"],
          "properties": {
            "calculationAttribute": {"enum": ["Water consumption"]}
          }
        }
      },
      {
        "if": {
          "required": ["connectionType"],
          "properties": {
            "connectionType": {"const": "Non_Metered"}
          }
        },
        "then": {
          "properties": {
            "calculationAttribute": {
              "enum": ["Flat", "No. of taps", "Pipe Size"]
            }
          }
        }
      }
    ],
    "title": "Generated schema for Root",
    "$schema": "http://json-schema.org/draft-07/schema#",
    "required": ["buildingType", "calculationAttribute", "connectionType", "minimumCharge"],
    "x-unique": ["buildingType", "connectionType"],
    "properties": {
      "slabs": {
        "type": "array",
        "items": {
          "type": "object",
          "required": ["from", "to", "charge"],
          "properties": {
            "to": {"type": "number"},
            "from": {"type": "number"},
            "charge": {"type": "number"},
            "meterCharge": {"type": "number"}
          }
        }
      },
      "buildingType": {
        "enum": [
          "RESIDENTIAL", "NONRESIDENTIAL", "COMMERCIAL AND GOVERNMENT", 
          "PARTLY COMMERCIAL", "COMMERCIAL", "GOVERNMENT", "MIXED", "PUBLICSECTOR"
        ],
        "type": "string"
      },
      "minimumCharge": {"type": "number"},
      "connectionType": {
        "enum": ["Metered", "Non_Metered"],
        "type": "string"
      },
      "calculationAttribute": {
        "enum": ["Flat", "Water consumption", "No. of taps", "Pipe Size"],
        "type": "string"
      }
    }
  },
  "isActive": true,
  "auditDetails": {
    "createdBy": "3059806b-3059-4724-8ae1-d3f4e12686ff",
    "lastModifiedBy": "3059806b-3059-4724-8ae1-d3f4e12686ff",
    "createdTime": 1701151086754,
    "lastModifiedTime": 1701151086754
  }
}
```

{% hint style="info" %}
**NOTE:** To migrate data for a specific master/module name, use the following code changes in **migrateMasterData**
{% endhint %}

```java
/**
 * This method accepts master data migration requests and triggers
 * creation of MDMS objects
 * @param masterDataMigrationRequest
 */
public void migrateMasterData(@Valid MasterDataMigrationRequest masterDataMigrationRequest) {

    // Get Master Data map
    Map<String, Map<String, JSONArray>> tenantMap = MDMSApplicationRunnerImpl.getTenantMap();

    // Get tenantId from request
    String tenantId = masterDataMigrationRequest.getMasterDataMigrationCriteria().getTenantId();

    // Build audit details for mdms objects creation
    AuditDetails auditDetails = new AuditDetails();
    RequestInfo requestInfo = masterDataMigrationRequest.getRequestInfo();
    AuditDetailsEnrichmentUtil.enrichAuditDetails(auditDetails, requestInfo, Boolean.TRUE);

    List<JSONArray> masterDataList = new ArrayList<>();

    // Check if master data is present for the incoming tenantId.
    if (tenantMap.containsKey(tenantId)) {
        tenantMap.get(tenantId).keySet().forEach(module -> {
            if (module.equals("common-masters")) {
                tenantMap.get(tenantId).get(module).keySet().forEach(master -> {
                    if (master.equals("CancelCurrentBillReasons") || master.equals("CancelReceiptReason") ||
                        master.equals("CronJobAPIConfig") || master.equals("Department") || master.equals("Designation") ||
                        master.equals("IdProof") || master.equals("UsageCategory") || master.equals("OwnerType") ||
                        master.equals("VehicleType") || master.equals("UOM") || master.equals("StructureType") ||
                        master.equals("TablePaginationOptions")) {
                        // Get master data array for current module and master
                        JSONArray masterDataJSONArray = MDMSApplicationRunnerImpl
                                .getJSONArray(tenantMap.get(tenantId)
                                .get(module)
                                .get(master));
                        masterDataList.add(masterDataJSONArray);
                    }
                });
            }
        });
    }
}

```
