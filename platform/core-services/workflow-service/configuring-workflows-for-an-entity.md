---
description: Configure workflows for a new product
---

# Configuring Workflows For An Entity

## Overview

Workflow is defined as a sequence of tasks that has to be performed on an application/Entity to process it. The _`egov-workflow-v2`_ is a workflow engine which helps in performing these operations seamlessly using a predefined configuration. We will discuss how to create this configuration for a new product in this document.

## Pre-requisites

Before you proceed with the configuration, make sure the following pre-requisites are met -

* _`egov-workflow-v2` service is up and running_
* Role action mapping is added for business service APIs

## Key Functionalities

* Create and modify workflow configuration according to the product requirements
* Configure State level as well BusinessService level SLA to efficiently track the progress of the application
* Control access to perform actions through configuration

<table><thead><tr><th width="262">Attributes</th><th>Description</th></tr></thead><tbody><tr><td><code>tenantId</code></td><td>The tenantId (ULB code) for which the workflow configuration is defined</td></tr><tr><td><code>businessService</code></td><td>The name of the workflow</td></tr><tr><td><code>business</code></td><td>The name of the module which uses this workflow configuration</td></tr><tr><td><code>businessServiceSla</code></td><td>The overall SLA to process the application (<em>in milliseconds</em>)</td></tr><tr><td><code>state</code></td><td>Name of the state</td></tr><tr><td><code>applicationStatus</code></td><td>Status of the application when in the given state</td></tr><tr><td><code>docUploadRequired</code></td><td>Boolean flag representing if document are required to enter the state</td></tr><tr><td><code>isStartState</code></td><td>Boolean flag representing if the state can be used as starting state in workflow</td></tr><tr><td><code>isTerminateState</code></td><td>Boolean flag representing if the state is the leaf node or end state in the workflow configuration. <em>(No Actions can be taken on states with this flag as true)</em></td></tr><tr><td><code>isStateUpdatable</code></td><td>Boolean flag representing whether data can be updated in the application when taking action on the state</td></tr><tr><td><code>currentState</code></td><td>The current state on which action can be performed</td></tr><tr><td><code>nextState</code></td><td>The resultant state after action is performed</td></tr><tr><td><code>roles</code></td><td>A list containing the roles which can perform the actions</td></tr><tr><td><code>auditDetails</code></td><td>Contains fields to audit edits on the data. <em>(createdTime, createdBy,lastModifiedTIme,lastModifiedby)</em></td></tr></tbody></table>

## Deployment Details

1. Deploy the latest version of the egov-workflow-v2 service.
2. Add businessService persister yaml path in persister configuration.
3. Add role action mapping for BusinessService APIs.
4. Overwrite the egov.wf.statelevel flag (_true_ for state level and _false_ for tenant level).

## Configuration Details

The Workflow configuration has 3 levels of hierarchy:\
a. BusinessService\
b. State\
c. Action\


The top-level object is BusinessService which contains fields describing the workflow and a list of States that are part of the workflow. The businessService can be defined at the tenant level like pb.amritsar or at the state level like pb. All objects maintain an audit sub-object which keeps track of who is creating and updating and the time of it.

```
{
        "tenantId": "pb.amritsar",
        "businessService": "PGR",
        "business": "pgr-services",
        "businessServiceSla": 432000000,
        "states": [...]
    }
```

Each state object is a valid status for the application. The State object contains information about the state and what actions can be performed on it.

```
{
        "sla": 36000000,
        "state": "PENDINGFORASSIGNMENT",
        "applicationStatus": "PENDINGFORASSIGNMENT",
        "docUploadRequired": false,
        "isStartState": false,
        "isTerminateState": false,
        "isStateUpdatable": false,
        "actions": [...]
    }
```

The action object is the last object in the hierarchy, it defines the name of the action and the roles that can perform the action.

```
      {
          "action": "ASSIGN",
          "roles": [
              "GRO",
              "DGRO"
          ],
          "nextState": "PENDINGATLME",
      }
```

The workflow should always start from the null state as the service treats new applications as having null as the initial state. eg:

```
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
                            "nextState": "APPLIED",
                            "roles": [
                                "CITIZEN",
                                "CSR"
                            ]
                        }
                    ]
                }
```

In the action object whatever nextState is defined, the application will be sent to that state. It can be to another forward state or even some backward state from where the application has already passed\
_(generally, such actions are named SENDBACK)_

SENDBACKTOCITIZEN is a special keyword for an action name. This action sends back the application to the citizen’s inbox for him to take action. A new State should be created on which Citizen can take action and should be the nextState of this action. While calling this action from the module _assignees_ should be enriched by the module with the UUIDs of the owners of the application

## Integration Details

For integration-related steps please refer to the document [**Setting Up Workflows**](setting-up-workflows.md).

## Reference Docs

### Doc Links

| Title                                           |
| ----------------------------------------------- |
| [Workflow Service Documentation](./)            |
| [Setting Up Workflows](setting-up-workflows.md) |

### API List

| Title                                                                      |
| -------------------------------------------------------------------------- |
| [_`_create`_](https://www.getpostman.com/collections/8552e3de40c819e34190) |
| [_`_update`_](https://www.getpostman.com/collections/8552e3de40c819e34190) |
| [_`_search`_](https://www.getpostman.com/collections/8552e3de40c819e34190) |

{% hint style="info" %}
**Note:** All the APIs are in the same Postman collection therefore the same link is added in each row
{% endhint %}

