# Add MDMS Configuration

## Overview

MDMS data is the master data used by the application. New modules with master data need to be configured inside the `/data/<tenant>/` folder of the MDMS repo. Each tenant should have a unique ID and sub-tenants can be configured in the format state.cityA, state.cityB etc..Further hierarchies are also possible with tenancy.&#x20;

{% hint style="info" %}
If you've configured the DIGIT environment with a tenant and CITIZEN/EMPLOYEE roles, you have sufficient data to run this module locally. Configuring role-action mapping is only necessary during app deployment in the DIGIT environment and won't be needed for local application execution.
{% endhint %}

{% hint style="info" %}
Refer to [MDMS](../../../../platform/core-services/mdms-v2-master-data-management-service/mdms-master-data-management-service/) docs for more information. To learn about how to design the MDMS, refer to the [design guide](../../../design-guide/design-services.md#identify-reference-data).
{% endhint %}

In the birth registration use case, we use the following master data:

1. tenantId = "pb"
2. User roles - CITIZEN and EMPLOYEE roles configured in roles.json (see below section for more info)
3. Actions - URIs to be exposed via Zuul (see below section for more info)
4. Role-action mapping - for access control (see below section for more info)

{% hint style="info" %}
Ensure that you add data to the appropriate branch of the MDMS repository. For example, if you've set up CD/CI to deploy the DEV branch of the repository to the development environment (default), add the information to the DEV branch. If you're testing in staging or another environment, make sure to add the master data to the corresponding branch of MDMS.
{% endhint %}

## Steps

1. Create a folder called "pb" in the data folder of the MDMS repository "DEV" branch. You will have a new folder path as follows:

`<MDMS repo URL path>/data/pb`

2. Restart the MDMS service in the development environment where DIGIT is running once data is added to the MDMS repository. This loads the newly added/updated MDMS configs.&#x20;

A sample MDMS config file can be viewed here - [Sample MDMS data file](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/common-masters/Department.json).

### API Access Control Configuration

URIs (actions), roles and URI-role mapping will be defined in MDMS. These will apply when the module is deployed into an environment  where Zuul is involved (not while locally running the app). In this sample app, we have used "pb" as a tenantId. In your environment, you can choose to define a new one or work with an existing one.&#x20;

All folders mentioned below need to be created under the `data/pb` folder in MDMS.

{% hint style="info" %}
You can choose to use some other tenantId. Make sure to change the tenant ID everywhere.
{% endhint %}

### Actions

Actions need to be defined inside the /`data/pb/ACCESS-CONTROL-ACTIONS/actions.json` file.  Below are the actions for the birth registration module. Append this to the bottom of the actions.json file. Make sure the "id" field in the JSON is incremented. It needs to be unique in your environment.

```json
// Some code
 {
      "id": 2382,
      "name": "Birth registration module create",
      "url": "/birth-registration/birth-services/v1/registration/_create",
      "parentModule": "",
      "displayName": "Birth registration",
      "orderNumber": 0,
      "enabled": true,
      "serviceCode": "BTR",
      "code": "null",
      "path": ""
    },
  {
    "id": 2383,
    "name": "Birth registration module update",
    "url": "/birth-registration/birth-services/v1/registration/_update",
    "parentModule": "",
    "displayName": "Birth registration",
    "orderNumber": 0,
    "enabled": true,
    "serviceCode": "BTR",
    "code": "null",
    "path": ""
  },
  {
    "id": 2384,
    "name": "Birth registration module search",
    "url": "/birth-registration/birth-services/v1/registration/_search",
    "parentModule": "",
    "displayName": "Birth registration",
    "orderNumber": 0,
    "enabled": true,
    "serviceCode": "BTR",
    "code": "null",
    "path": ""
  }
```

Note that the IDs in the actions.json config are generated manually.

### Roles Configuration

Roles config happens at a state level. For birth registration, we need only CITIZEN and EMPLOYEE roles in the /`data/pb/ACCESSCONTROL-ROLES/roles.json` file.Here are some [sample roles ](https://github.com/egovernments/egov-mdms-data/tree/UAT/data/pg/ACCESSCONTROL-ROLES) that can be defined in an environment. If these roles are already present in the file, then there is no need to add them in again.

### Role-action Mapping

Append the below code to the "roleactions" key in the /`data/pb/ACCESSCONTROL-ROLEACTIONS/`**`roleactions.json.`** Note that other role-action mappings may already be defined in your DIGIT environment. So please make sure to append the below. The `actionid` refers to the URI ID defined in the actions.json file.&#x20;

```json
    {
      "rolecode": "CITIZEN",
      "actionid": 2382,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2383,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2384,
      "actioncode": "",
      "tenantId": "pb"
    }
```
