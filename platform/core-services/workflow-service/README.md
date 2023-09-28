---
description: Configure workflows as per requirements
---

# Workflow Service

## Overview

Workflows are a series of steps that moves a process from one state to another state by actions performed by different kind of Actors - Humans, Machines, Time based events etc. to achieve a goal like onboarding an employee, or approve an application or granting a resource etc. The _egov-workflow-v2_ is a workflow engine which helps in performing these operations seamlessly using a predefined configuration.

## Pre-requisites

Before you proceed with the documentation, make sure the following pre-requisites are met -

* Java 8
* Kafka server is up and running
* egov-persister service is running and has a workflow persister config path added to it
* PSQL server is running and a database is created to store workflow configuration and data

## Key Functionalities

* Always allow anyone with a role in the workflow state machine to view the workflow instances and comment on it
* On the creation of workflow, it will appear in the inbox of all employees that have roles that can perform any state transitioning actions in this state.
* Once an instance is marked to an individual employee it will appear only in that employee's inbox although point 1 will still hold true and all others participating in the workflow can still search it and act if they have the necessary action available to them
* If the instance is marked to a person who cannot perform any state transitioning action, they can still comment/upload and mark to anyone else.
* **Overall SLA:** SLA for the complete processing of the application/Entity
* **State-level SLA:** SLA for a particular state in the workflow

| **Environment Variables**  | **Description**                                                                                                                                                                                                                                                                                                                                      |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| egov.wf.default.offset     | The default value of offset in search                                                                                                                                                                                                                                                                                                                |
| egov.wf.default.limit      | The default value of limit in search                                                                                                                                                                                                                                                                                                                 |
| egov.wf.max.limit          | The maximum number of records that are returned in search response                                                                                                                                                                                                                                                                                   |
| egov.wf.inbox.assignedonly | Boolean flag if set to _true_ default search will return records assigned to the user only, if _false_ it will return all the records based on the user’s role. _(default search is the search call when no query params are sent and based on the RequestInfo of the call, records are returned, it’s used to show applications in employee inbox)_ |
| egov.wf.statelevel         | Boolean flag set to _true_ if a state-level workflow is required                                                                                                                                                                                                                                                                                     |

## Interaction Diagram

<div align="left">

<figure><img src="../../../../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>

</div>



## Deployment Details

1. Deploy the latest version of egov-workflow-v2 service
2. Add businessService persister yaml path in persister configuration
3. Add Role-Action mapping for BusinessService APIs
4. Overwrite the egov.wf.statelevel flag ( _true_ for state level and _false_ for tenant level)
5. Create businessService (workflow configuration) according to product requirements
6. Add Role-Action mapping for _/processInstance/\_search_ API
7. Add workflow persister yaml path in persister configuration

## Configuration Details

For configuration details please refer to the links in Reference Docs.

## Integration Details

### Integration Scope

The workflow configuration can be used by any module which performs a sequence of operations on an application/Entity. It can be used to simulate and track processes in organisations to make it more efficient too and increase accountability.

### Integration Benefits

* Role-based workflow
* An easy way of writing rule
* File movement within workflow roles

### Steps to Integration

1. To integrate, the host of egov-workflow-v2 should be overwritten in the helm chart.
2. /process/\_search should be added as the search endpoint for searching workflow process Instance objects.
3. /process/\_transition should be added to perform an action on an application. _(It’s for internal use in modules and should not be added in Role-Action mapping)._
4. The workflow configuration can be fetched by calling _\_search_ API to check if data can be updated or not in the current state.

## Reference Docs

### Doc Links

| Title                                                                                                              |
| ------------------------------------------------------------------------------------------------------------------ |
| [Configuring Workflows For New Product/Entity](configuring-workflows-for-an-entity.md)                             |
| [Setting Up Workflows](setting-up-workflows.md)                                                                    |
| [API Swagger Documentation](https://raw.githubusercontent.com/egovernments/core-services/master/docs/worfklow-2.0) |
| [Migration to Workflow 2.0](migration-to-workflow-2.0.md)                                                          |

### API List

| Title                                                                                      |
| ------------------------------------------------------------------------------------------ |
| [_/businessservice/\_create_](https://www.getpostman.com/collections/8552e3de40c819e34190) |
| [_/businessservice/\_update_](https://www.getpostman.com/collections/8552e3de40c819e34190) |
| [_/businessservice/\_search_](https://www.getpostman.com/collections/8552e3de40c819e34190) |
| [_/process/\_transition_](https://www.getpostman.com/collections/8552e3de40c819e34190)     |
| [_/process/\_search_](https://www.getpostman.com/collections/8552e3de40c819e34190)         |

{% hint style="info" %}
**Note:** All the APIs are in the same Postman collection therefore the same link is added in each row
{% endhint %}

