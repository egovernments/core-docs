---
description: Create and modify workflow configuration
---

# Setting Up Workflows

## Overview

Each service integrated with egov-workflow-v2 service needs to first define the workflow configuration which describes the workflow states, the action that can be taken on these states, the user roles that can perform those actions, SLAs etc. This configuration is created using APIs and is stored in the DB. The configuration can be created at either the state level or the tenant level based on the requirements.

## Pre-requisites

Before you proceed with the configuration, make sure the following pre-requisites are met -

* egov-workflow-v2 service is up and running
* Role action mapping is added for the BusinessService APIs

## Key Functionalities

* Create and modify workflow configuration
* Configure state level as well BusinessService level SLA
* Control access to workflow actions from the configuration
* Validates if the flow defined in the configuration is complete during the creation

## Deployment Details

1. Deploy the latest version of egov-workflow-v2 service.
2. Add role action mapping for BusinessService APIs (preferably add \_create and update only for SUPERUSER. Search can be added for CITIZEN and required employee roles like TL\_\_CEMP etc.
3. Overwrite the egov.wf.statelevel flag (_true_ for state level and _false_ for tenant level).
4. Add businessService persister yaml path in persister configuration.

## Configuration Details

Create the businessService JSON based on product requirements. Following is a sample json of a simple 2-step workflow where an application can be applied by a citizen or counter employee and then can be either rejected or approved by the approver.

```json
{
      "tenantId": "pb",
      "businessService": "PGR",
      "business": "pgr-services",
      "businessServiceSla": 432000000,
      "states": [
        {
          "sla": null,
          "state": null,
          "applicationStatus": null,
          "docUploadRequired": false,
          "isStartState": true,
          "isTerminateState": false,
          "isStateUpdatable": true,
          "actions": [
            {
              "action": "APPLY",
              "nextState": "PENDINGFORASSIGNMENT",
              "roles": [
                "CITIZEN",
                "COUNTER_EMPLOYEE"
              ]
            }
          ]
        },
        {
          "sla": null,
          "state": "APPLIED",
          "applicationStatus": "APPLIED",
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": false,
          "isStateUpdatable": false,
          "actions": [
            {
              "action": "APPROVE",
              "nextState": "APPROVED",
              "roles": [
                "APPROVER"
              ]
            },
            {
              "action": "REJECT",
              "nextState": "REJECTED",
              "roles": [
                "APPROVER"
              ]
            }
          ]
        },
        {
          "sla": null,
          "state": "REJECTED",
          "applicationStatus": "REJECTED",
          "isStateUpdatable": false,
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": true
        },
        {
          "sla": null,
          "state": "APPROVED",
          "applicationStatus": "APPROVED",
          "isStateUpdatable": false,
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": true
        }
      ]
    }
```

Once the businessService json is created add it in the request body of _\_create_ API of workflow and call the API to create the workflow.

To update the workflow first search the workflow object using _\_search_ API and then make changes in the businessService object and then call _\_update_ using the modified search result.&#x20;

States cannot be removed using _\_update_ API as it will leave applications in that state in an invalid state. In such cases first, all the applications in that state should be moved forward or backward state and then the state should be disabled through DB directly.

## Integration Details

### Integration Scope

The workflow configuration can be used by any module which performs a sequence of operations on an application/entity. It can be used to simulate and track processes in organisations to make them more efficient and increase accountability.

### Integration Benefits

Integrating with workflow service provides a way to have a dynamic workflow configuration which can be easily modified according to the changing requirements. The modules don’t have to deal with any validations regarding workflow such as authorisation of the user to take an action if documents are required to be uploaded at a certain stage etc. since it will be automatically handled by _egov-workflow-v2_ service based on the defined configuration. It also automatically keeps updating SLAs for all applications which provide a way to track the time taken by an application to get processed.

### Integration Steps

1. To integrate, the host of `egov-workflow-v2` should be overwritten in the helm chart
2. _`/egov-workflow-v2/egov-wf/businessservice/_search`_ should be added as the endpoint for searching workflow configuration. (Other endpoints are not required once workflow configuration is created)
3. The configuration can be fetched by calling  _`_search`_` ``API`

## Reference Docs

### Doc Links

| Title                                                                                  |
| -------------------------------------------------------------------------------------- |
| [Configuring Workflows For New Product/Entity](configuring-workflows-for-an-entity.md) |
| [Workflow Service Documentation](./)                                                   |

### API List

| Title                                                                      |
| -------------------------------------------------------------------------- |
| [_`_create`_](https://www.getpostman.com/collections/8552e3de40c819e34190) |
| [_`_update`_](https://www.getpostman.com/collections/8552e3de40c819e34190) |
| [_`_search`_](https://www.getpostman.com/collections/8552e3de40c819e34190) |

{% hint style="info" %}
**Note:** All the APIs are in the same Postman collection therefore the same link is added in each row
{% endhint %}

