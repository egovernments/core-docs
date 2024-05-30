---
description: Configure role based user access and map actions to roles
---

# Access Control Services

## Overview

DIGIT is an API-based platform where each API denotes a DIGIT resource. The primary job of Access Control Service (ACS) is to authorise end-user based on their roles and provide access to the DIGIT platform resources. Access control functionality is essentially based on below points:

**Actions:** Actions are events which are performed by a user. This can be an API end-point or front-end event. This is the MDMS master.

**Roles:** Roles are assigned to users. A single user can hold multiple roles. Roles are defined in MDMS masters.

**Role-Action:** Role actions are mapped between Actions and Roles. Based on roles, the action mapping access control service identifies applicable actions for the role.

## Pre-requisites

Before you proceed with the configuration, make sure the following pre-requisites are met -

* Java 17
* [MDMS](mdms-v2-master-data-management-service/mdms-master-data-management-service/) service is up and running

## Key Functionalities

* Serve the applicable actions for a user based on user roles .
* On each action performed by a user, access control looks at the roles for the user and validates actions mapping with the role.
* Support tenant-level role action - For instance, an employee from Amritsar can have the role of APPROVER for other ULBs like Jalandhar and hence will be authorised to act as APPROVER in Jalandhar.

## Play around with the API's : [DIGIT-Playground](https://digit-api.apidog.io/doc-507201)&#x20;

## Deployment Details

1. [Deploy](../../accelerators/concepts/deployment-key-concepts/deploying-digit-services.md)  the latest version of the Access Control Service
   * **Note**: This video will give you an idea of how to deploy any Digit-service. Further you can find the latest builds for each service in out latest [release document](../releases/digit-2.9-lts/service-build-updates.md) here.
2. [Deploy](../../accelerators/concepts/deployment-key-concepts/deploying-digit-services.md)  service to fetch the Role Action Mappings
   * **Note**: This video will give you an idea of how to deploy any Digit-service. Further you can find the latest builds for each service in out latest [release document](../releases/digit-2.9-lts/service-build-updates.md) here.

## Configuration Details

Define the roles:

{% code lineNumbers="true" %}
```json
{
      "code": "EMPLOYEE",
      "name": "Employee",
      "description": "Default role for all employees"
}
```
{% endcode %}

Add the actions (URL)

{% code lineNumbers="true" %}
```json
{
      "id": {{ACTION_ID}},
      "name": "Create TradeLicense",
      "url": "/tl-services/v1/_create",
      "parentModule": "",
      "displayName": "Create TradeLicense",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "tl-services",
      "code": "null",
      "path": ""
}
```
{% endcode %}

Add the role action mapping

{% code lineNumbers="true" %}
```json
{
      "rolecode": "EMPLOYEE",
      "actionid": {{ACTION_ID}},
      "actioncode": "",
      "tenantId": "pb"
    }
```
{% endcode %}

{% hint style="info" %}
The details about the fields in the configuration can be found in the [Swagger contract](https://raw.githubusercontent.com/egovernments/egov-services/master/docs/egov-accesscontrol/contracts/v1-0-1.yml)
{% endhint %}

## Integration Details

### Integration Scope

Any Service which requires **authorisation** can leverage the functionalities provided by the access control service.

### Integration Benefits

Any new service that is to be added to the platform will not have to worry about authorisation. It can just add its role action mapping in the master data and the Access Control Service will perform authorisation whenever the API for the microservice is called.

### Integration Steps

1. To integrate with Access Control Service the [role action mapping](https://github.com/egovernments/playground-mdms-data/blob/master/data/pg/ACCESSCONTROL-ROLEACTIONS/roleactions.json) has to be configured (added) in the MDMS service.
2. The service needs to call `/actions/_authorize` API of Access Control Service to check for authorisation of any request.

## Interaction Diagram

<figure><img src="../../.gitbook/assets/acccessControl.png" alt=""><figcaption></figcaption></figure>

## Reference Docs

### Doc Links

| Title                                                                                                                            |
| -------------------------------------------------------------------------------------------------------------------------------- |
| [API Contract](https://raw.githubusercontent.com/egovernments/egov-services/master/docs/egov-accesscontrol/contracts/v1-0-1.yml) |

### API List

| Title                  | Link                                                              |
| ---------------------- | ----------------------------------------------------------------- |
|  `/actions/_authorize` | [\[LINK TO BE UPDATED\]](https://digit-api.apidog.io/api-6828950) |

