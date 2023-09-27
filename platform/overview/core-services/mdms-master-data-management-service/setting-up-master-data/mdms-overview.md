# MDMS Overview

## Overview

MDMS stands for Master Data Management Service. MDMS is one of the applications in the eGov DIGIT core group of services. This service aims to reduce the time spent by developers on writing codes to store and fetch master data (primary data needed for module functionality ) which doesn’t have any business logic associated with them.

## Pre-requisites

Before you proceed with the configuration, make sure the following pre-requisites are met -

* Prior knowledge of Java/J2EE.
* Prior knowledge of Spring Boot.
* Prior knowledge of REST APIs and related concepts like path parameters, headers, JSON, etc.
* Prior knowledge of Git.
* Advanced knowledge of how to operate JSON data would be an added advantage to understanding the service.

## Key Functionalities

* The MDMS service reads the data from a set of JSON files from a pre-specified location.
* It can either be an online location (readable JSON files from online) or offline (JSON files stored in local memory).
* The JSON files are in a prescribed format and store the data on a map. The **tenantID** of the file serves as a key and a map of master data details as values.
* Once the data is stored in the map the same can be retrieved by making an API request to the MDMS service. Filters can be applied in the request to retrieve data based on the existing fields of JSON.

## Deployment Details

* For deploying the changes in MDMS data, the service needs to be restarted.
* The changes in MDMS data could be adding new data, updating existing data, or deleting it.

## Configuration Details

The config JSON files to be written should follow the listed rules

* The config files should have JSON extension
* The file should mention the tenantId, module name, and master name first before defining the data

{% code lineNumbers="true" %}
```
{
  "tenantId": "uk",
  "moduleName": "BillingService",
  "{$MasterName}":[ ]
}
```
{% endcode %}



| Title      | Description                                                                                                                      |
| ---------- | -------------------------------------------------------------------------------------------------------------------------------- |
| tenantId   | Serves as a Key                                                                                                                  |
| moduleName | Name of the module to which the master data belongs                                                                              |
| MasterName | The Master Name will be substituted by the actual name of the master data. The array succeeding it will contain the actual data. |

Example config JSON for “Billing Service”

{% code lineNumbers="true" %}
```
{
  "tenantId": "pb",
  "moduleName": "BillingService",
 "BusinessService": 
 [
    {
      "businessService": "PropertyTax",
      "code": "PT",
      "collectionModesNotAllowed": [ "DD" ],
      "partPaymentAllowed": true,
      "isAdvanceAllowed": true,
      "isVoucherCreationEnabled": true
    }
]
}
```
{% endcode %}

## Reference Docs

### Doc Links

| Description                         |
| ----------------------------------- |
| [MDMS Service](../)                 |
| [MDMS Rewritten](mdms-rewritten.md) |

### API List

| Description                                                                                                                 |
| --------------------------------------------------------------------------------------------------------------------------- |
| [API Contract Reference](https://raw.githubusercontent.com/egovernments/egov-services/master/docs/mdms/contract/v1-0-0.yml) |
