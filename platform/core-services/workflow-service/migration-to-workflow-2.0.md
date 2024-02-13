---
description: Deploy workflow 2.0 in an environment where workflow is already running
---

# Migration To Workflow 2.0

## Overview

In workflow 2.0 assignee is changed from an object to a list of objects.&#x20;

## Deployment Details

To accommodate this change a new table named 'eg\_wf\_assignee\_v2' is added that maps the processInstaceIds to assignee UUIDs. To deploy workflow 2.0 in an environment where workflow is already running assignee column needs to be migrated to the eg\_wf\_assignee\_v2 table.&#x20;

The following query does this migration:

{% code lineNumbers="true" %}
```
INSERT INTO eg_wf_assignee_v2(processinstanceid, tenantid, assignee, createdBy, lastModifiedBy, createdTime, lastModifiedTime) SELECT id, tenantid,
         assignee, createdBy, lastModifiedBy ,createdTime,lastModifiedTime FROM eg_wf_processinstance_v2 WHERE assignee IS NOT NULL;
```
{% endcode %}

## Configuration Details

### Persister Configuration

Persister config for egov-workflow-v2 is updated. Insert query for the table eg\_wf\_assignee\_v2 is added in egov-workflow-v2-persister.yml.&#x20;

The latest updated config can be referred to from the below link:&#x20;

{% embed url="https://github.com/egovernments/configs/blob/master/egov-persister/egov-workflow-v2-persister.yml" %}

### Searcher Configuration

The employee inbox has an added column to display the locality of the applications. This mapping of the application number to locality is fetched by calling the searcher API for the respective module. If a new module is integrated with workflow its searcher config should be added in the locality searcher yaml with module code as a name in the definition. All the search URLs and role action mapping details must be added to the MDMS.&#x20;

The format of the URL is given below:

{% code lineNumbers="true" %}
```
        /egov-searcher/locality/{MODULENAME}/_get
```
{% endcode %}

Sample request for TL:

{% code lineNumbers="true" %}
```
  curl -X POST \
        https://egov-micro-dev.egovernments.org/egov-searcher/locality/TL/_get \
        -H 'Content-Type: application/json' \
        -H 'Postman-Token: 1c2adbb9-004f-42ce-8aab-a29a2b0df7a7' \
        -H 'cache-control: no-cache' \
        -d '{
        "RequestInfo": {
            "apiId": "Rainmaker",
            "ver": ".01",
            "ts": 0,
            "action": "_create",
            "did": "1",
            "key": "",
            "msgId": "20170310130900|en_IN",
            "authToken": "5cb9019c-f690-4c88-850d-d15cbc2c6e54",
            "correlationId": "a2e4642e-8cb5-483b-8ea2-827cbe822c5f"
        },
        "searchCriteria": {
            "referenceNumber":[ "PB-TL-2019-04-24-001768","PB-TL-2019-04-22-001764"]
        }Migration
        }' 
```
{% endcode %}

The searcher yaml can be referred from the below link:

{% embed url="https://github.com/egovernments/configs/blob/master/egov-searcher/localitySearcher.yml" %}

### Business Service Configuration <a href="#businessservice" id="businessservice"></a>

For sending back the application to citizens, the action with the key 'SENDBACKTOCITIZEN' must be added. The exact key should be used. The resultant state of the action should be a new state. If pointing to an existing state the action in that state will be visible to the CITIZEN even when the application reaches the state without Send Back as the workflow is role-based.&#x20;

To update the businessService for Send Back feature, add the following state and action in the search response at required places and add call businessService update API. This assigns the UUID to the new state and action and creates the required references. The Resubmit action is added as optional action for counter employees to take action on behalf of the citizen.

State json:

{% code lineNumbers="true" %}
```
{
              "sla": null,
              "state": "CITIZENACTIONREQUIRED",
              "applicationStatus": "CITIZENACTIONREQUIRED",
              "docUploadRequired": false,
              "isStartState": false,
              "isTerminateState": false,
              "isStateUpdatable": true,
              "actions": [
                  {
                      "action": "FORWARD",
                      "nextState": "FIELDINSPECTION",
                      "roles": [
                          "CITIZEN"
                      ]
                  },
                  {
                      "action": "RESUBMIT",
                      "nextState": "FIELDINSPECTION",
                      "roles": [
                          "TL_CEMP"
                      ]
                  }
              ]
}
```
{% endcode %}

Action json:

{% code lineNumbers="true" %}
```
{
          "action": "SENDBACKTOCITIZEN",
          "nextState": "CITIZENACTIONREQUIRED",
          "roles": [
              "TL_FIELD_INSPECTOR"
          ]
}
```
{% endcode %}

### UI Configuration

Each item in the above dropdown is displayed by adding an object in the link below -

{% embed url="https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/ACCESSCONTROL-ACTIONS-TEST/actions-test.json" %}

<div align="left">

<figure><img src="../../../.gitbook/assets/image (167).png" alt=""><figcaption></figcaption></figure>

</div>

For example:

&#x20;{

&#x20;   "id": 1928,

&#x20;   "name": "rainmaker-common-tradelicence",

&#x20;   "url": "quickAction",

&#x20;   "displayName": "Search TL",

&#x20;   "orderNumber": 2,

&#x20;   "parentModule": "",

&#x20;   "enabled": true,

&#x20;   "serviceCode": "",

&#x20;   "code": "",

&#x20;   "path": "",

&#x20;   "navigationURL": "tradelicence/search",

&#x20;   "leftIcon": "places:business-center",

&#x20;   "rightIcon": "",

&#x20;   "queryParams": ""

&#x20; }

* **id , url, displayName, navigationURL**
  * Mandatory properties.
* The value of the URL property should be “**quickAction**” as shown above.

Accordingly, add the role-actions:

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/roleactions.json at master · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/ACCESSCONTROL-ROLEACTIONS/roleactions.json)

{

&#x20;   "rolecode": "TL\_CEMP",

&#x20;   "actionid": 1928,

&#x20;   "actioncode": "",

&#x20;   "tenantId": "pb"

&#x20; }

### **SLA Configuration**

<figure><img src="../../../.gitbook/assets/image (189).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (195).png" alt=""><figcaption></figcaption></figure>

SLA slots and the background colour of the SLA days remaining on the Inbox page are defined in the MDMS configuration as shown above.

For example: If the maximum SLA is 30 then, it has 3 slots

1. 30 - 30\*(1/3) => 20 - 30: will have green colour defined
2. 0 - 20: will have yellow colour defined
3. <0: will have red colour defined

The colours are also configured in the MDMS.

## Integration Details

* For API _/egov-workflow-v2/egov-wf/process/\_transition_:\
  The field assignee of type User in ProcessInstance object is changed to a list of 'User' called assignees.\
  User assignee --> List\<User> assignees
* For Citizen Sendback:\
  When the action SENDBACKTOCITIZEN is called on the entity the module has to enrich the assignees with the UUIDs of the owners and creator of the entity.
