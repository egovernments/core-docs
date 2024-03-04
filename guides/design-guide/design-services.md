---
description: Steps to identify registries and services
---

# Design Services

## **Overview**

This document provides the steps to identify the registries and other services. One needs to identify the common nouns and verbs. Broadly, nouns translate to registries/services and verbs translate to operations or APIs.

## **Steps - Identify Registries & Services**&#x20;

List the activities in a table and separate the nouns and the verbs as illustrated in the table below. The activities are generalized e.g. in verify application the word application refers to "Birth Certificate Application" hence generalize this to Verify Birth Certificate (we have dropped the term Application for brevity). Knowing the list of services available in DIGIT also helps - as you may call the activity "Pay Charges" instead of "Make Payment". This process may require a few iterations.&#x20;

<table><thead><tr><th width="188">Activity</th><th width="167">Generalized Activity</th><th width="167.1914893617021">Verb</th><th>Noun</th></tr></thead><tbody><tr><td>Apply for Birth Certificate</td><td>Create Birth Certificate </td><td>Create</td><td>Birth Certificate</td></tr><tr><td>Make Payment</td><td>Make Payment</td><td>Make</td><td>Payment</td></tr><tr><td>Verify Application</td><td>Verify Birth Certificate</td><td>Verify</td><td>Birth Certificate</td></tr><tr><td>Approve Application</td><td>Approve Birth Certificate</td><td>Approve</td><td>Birth Certificate</td></tr><tr><td>Send Notification</td><td>Send Notification</td><td>Send</td><td>Notification</td></tr><tr><td>Update Application</td><td>Update Birth Certificate</td><td>Update</td><td>Birth Certificate</td></tr><tr><td>Download Certificate</td><td>Download Birth Certificate</td><td>Download</td><td>Birth Certificate</td></tr></tbody></table>

Now transform the above verb and noun columns to the table below to identify the first set of services and their operations.

<table><thead><tr><th width="281">Service</th><th>Operation</th></tr></thead><tbody><tr><td>Birth Certificate</td><td>Create</td></tr><tr><td></td><td>Update</td></tr><tr><td></td><td>Verify</td></tr><tr><td></td><td>Approve</td></tr><tr><td></td><td>Download</td></tr><tr><td>Notification</td><td>Send</td></tr></tbody></table>

So we have now identified 2 services Birth Certificate and Notification. When we get into detailing the sequence diagrams, it is quite possible that a few more services may emerge e.g. Birth Certificate Charge Calculator - assume charge calculation logic varies between different cities hence it makes sense to externalize this outside Birth Certificate Service. &#x20;

### **Extract Workflows**

Workflows can be configured in DIGIT using the Workflow Service. Workflows must be extracted from the swim lane diagrams and converted into a sequence of states and specific activities a specific actor can perform on that state.&#x20;

{% hint style="info" %}
**Workflows** are a series of steps that moves a process from one state to another state through actions performed by different kind of Actors - Humans, Machines, Time-based events etc. to achieve a goal like onboarding an employee, approving an application or granting a resource etc.&#x20;

DIGIT's workflow service is a simple state machine.

The workflow configuration can be used by any module which performs a sequence of operations on an application/Entity. It can be used to simulate and track processes in organisations to make them more efficient too and increase accountability.
{% endhint %}

The below table illustrates the process:

<table><thead><tr><th width="267.73825503355704">What is the state of the application?</th><th width="204">Which role can act?</th><th>What actions can the role take?</th></tr></thead><tbody><tr><td>Null</td><td>Applicant</td><td>Apply</td></tr><tr><td>Awaiting Verification</td><td>Verifier</td><td>Mark Verified<br>Ask for Clarification</td></tr><tr><td>Awaiting Clarification</td><td>Applicant</td><td>Save/Update</td></tr><tr><td>Verified</td><td>Verifier</td><td>Assign Approver</td></tr><tr><td>Awaiting Approval</td><td>Approver</td><td>Approve<br>Reject</td></tr><tr><td>Approved</td><td>-</td><td>-</td></tr><tr><td>Rejected</td><td>-</td><td>-</td></tr></tbody></table>

&#x20;                                                                               **Workflow Table1**

The above table needs to be translated into [Workflow](../../platform/core-services/workflow-service/configuring-workflows-for-an-entity.md) and MDMS service configurations.&#x20;

At a high level, a workflow consists of:

1. States&#x20;
2. Actions that can be taken in each state
3. Roles that can perform these actions.

Below is a sample workflow JSON template that can be customised.

{% file src="../../.gitbook/assets/sample-workflow-json.jsonc" %}
Sample workflow JSON
{% endfile %}

The states in the first column of the table go into the states array in the workflow JSON. Each state has to be enumerated with the right attributes.

The actions in the third column of the table go into an `actions` JSON array inside each state object. These are the actions that can be taken on any given state to move it to another state. Each action object in the array has the following attributes:

* `"action"` - name of the action
* `"nextState"` - the state this action leads to
* `"roles"` -  The roles that can take action on the state. These roles should be a subset of the roles in the second column of the table and need to map to the [roles.json config in MDMS](design-services.md#extract-mdms-configuration).

The workflow service needs to be configured with this JSON through a REST API call. See here for a [hands-on example](../developer-guide/backend-developer-guide/section-3-integrate-microservices/add-workflow-configuration.md) of how this is done. A sample workflow JSON with placeholders is defined in the file below. This can be used as a customisable template.

### Identify Reference Data

DIGIT comes with an MDMS (Master Data Management Service) that holds master data for a module. &#x20;

{% hint style="info" %}
**MDMS** is used to store data that is unchanging or **slow changing**. Examples of MDMS data are administrative hierarchies, revenue hierarchies, property types, trade license types etc.. Data that changes frequently and requires exposing CRUD APIs go into the database as **registries**.&#x20;
{% endhint %}

Reference data is configured in GitHub in the forked [MDMS repository](https://github.com/egovernments/egov-mdms-data/). Each tenant is created as a folder under the `data` folder. It is recommended that each module's reference data be stored under its own folder for easy reference.&#x20;

The master data can be at the state level or city level. State-level configurations are stored in `master-config.json` under the tenant folder. Set the `isStateLevel` flag as true if these values cannot be overridden. Other subtenants can define their own modules and master names inside their sub-tenant folders.

<mark style="color:red;">**Note that MDMS does not follow any inheritance rules between tenants and sub-tenants. i.e. a sub-tenant defining data inside their folders will NOT implicitly inherit master tenant data.**</mark>&#x20;

{% hint style="info" %}
The folder names and the file names for the custom, module-related master data can be defined as per the user's needs. What has to remain the same is the module names and master names that are defined inside the JSON. These have to match with the master-config.json  also where applicable.  If there are mismatches here, MDMS will not find the required data.
{% endhint %}

Example: [https://github.com/egovernments/egov-mdms-data/blob/UAT/master-config.json](https://github.com/egovernments/egov-mdms-data/blob/UAT/master-config.json)

The tenancy is configured under the `tenant` folder. `tenants.json` configures a list of tenants including state-level and city-level tenants. This is used by the front-end login screen to show a list of tenants. Back-end will still work without an explicit tenants.json file. Logos, shape files, lat long coordinates and other tenant information are to be configured here.&#x20;

Sample tenant information can be [referred to here](https://github.com/egovernments/egov-mdms-data/tree/UAT/data/pg/tenant).  &#x20;

### Extract Roles & Access Control MDMS Configuration

A part of the MDMS configuration for access control can be extracted from the [table above](design-services.md#extract-the-workflow). All new services need to provide access control for the URIs they expose via role action mappings. A module needs to define roles, actions (URIs) and role-action mapping.&#x20;

{% hint style="info" %}
Note that this is only a part of the MDMS configuration. Any other configuration that the module requires has to be set up in MDMS separately.&#x20;
{% endhint %}

### Configure Roles

Create a file called `roles.json`. All the unique roles in the second column of the table need to go into the JSON in the following format below. This needs to be copied to the MDMS repository under the following path:

`/{{mdms-repo}}/data/{{tenantId}}/`[`ACCESSCONTROL-ROLES`](https://github.com/egovernments/egov-mdms-data/tree/DEV/data/pb/ACCESSCONTROL-ROLES)

For this sample application, we will have two roles: EMPLOYEE and CITIZEN.

```json
// Roles JSON 
{[
{
      "code": "{{Role1}}", //Example: Employee
      "name": "{{Role1 Display Name}}",//Example: ULB Employee
      "description": "Default role for all employees"
},
{
      "code": "{{Role2}}",
      "name": "{{Role2 Display Name}}",
      "description": "End user citizen"
},
]
}
```

### Configure Actions&#x20;

Add the URIs from the API spec in a file called `actions-test.json` under the following path:

`/{{mdms-repo}}/data/{{tenantId}}/`**`ACCESSCONTROL-ACTIONS-TEST`**`/`

All URIs for the module need to be included here. The ACTION\_ID needs to be unique and manually generated. Pick a unique ID series for your module.

```
{
      "id": {{ACTION_ID}}, //Needs to be a hand generated unique ID
      "name": "Create birth certificate",
      "url": "/birth-services/v1/_create",
      "parentModule": "",
      "displayName": "Create Birth certificate application",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "birth-services",
      "code": "null",
      "path": ""
}
```

### Configure Role-action Mapping &#x20;

Add the role action mapping in a file called `roleactions.json` under the following path:

`/{{mdms-repo}}/data/{{tenantId}}/`**`ACCESSCONTROL-ROLEACTIONS`**`/`

```
{
      "rolecode": "EMPLOYEE",
      "actionid": {{ACTION_ID}},
      "actioncode": "",
      "tenantId": "{{tenantId}}"
    }
```

### **Detailed Design For Registries & Services**&#x20;

The detailed design consists of&#x20;

1. External Service Interface
2. Internal Implementation

External Service Interface is expressed as in Open API Specification using tools like Swagger. You can open the sample Pet Store provided and modify it to your needs. [Here ](https://editor.swagger.io/?\_ga=2.12891634.451111407.1659147601-509029862.1640847544)is a sample API specification in YAML for the above example. This will require identifying the attributes of the Birth Certificate Object - this information will be available in the user stories or use cases. The YAML document thus created can be used to generate the initial service code as well as the service client.&#x20;

Internal Implementation of the services consists of specifying the class diagram and database tables in which the state of the service i.e. Birth Certificate Object with be stored.&#x20;

### **Identify DIGIT Reusable Registries & Services**

To identify the list of services, one way is to go through the list of below questions.

If users need to be authenticated, then **User Service** will be required.

If there is a need to restrict certain functionalities to certain users, then **Role Service** will be required. When adding an **Employee** to the system, roles can be added giving them appropriate access.  &#x20;

If reference data e.g. Gender - Male, Female, Others etc. needs to be configured, then **Master Data Management Service** will be required.

If information needs to be presented to users in multiple languages then **Localization Service** will be required.

All DIGIT services push data into a Kafka queue which is then picked up by the **Persister Service** which then writes it to the database. This shields the database from a large volume of writes and also provides the ability for the **Indexer** to enrich the data and push it to the Elastic Search for **Decision Support Service (DSS)** to display the dashboard.  In addition, all changes to data are signed and logged into an audit log by the **Signed Audit Service.** This ensures non-repudiation. **File Store Service** is used to store files - depending on the private or public cloud - it can be configured to use the appropriate underlying technologies. &#x20;

All workflows can be configured in the **Workflow Service.** &#x20;

Users and Employees can be notified using **SMS**, **Email** and **App Notification Service.**&#x20;

**Telemetry Service** provides the ability to track user activities to identify drop-offs. However, this requires the user interface developer to inject the telemetry instrumentation at appropriate points in code e.g. when a user starts a new application, when a user moves to a new section, when the user saves the application, or when a user makes a payment etc.

### **Develop Sequence Diagrams**

Now that we have identified the list of services, develop the sequence diagrams which show how all the services talk to each other to enact a use case or user story. A sequence diagram is illustrated below.

![Typical Sequence Diagram for DIGIT](<../../.gitbook/assets/image (42).png>)
