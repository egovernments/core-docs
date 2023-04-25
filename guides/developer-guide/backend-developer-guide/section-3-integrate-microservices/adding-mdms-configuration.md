# Adding MDMS Configuration

{% hint style="info" %}
If you already have a DIGIT environment configured with a tenant and CITIZEN/EMPLOYEE roles, that is sufficient data to get this module running locally. Configuring role-action mapping is necessary during deployment of the app in the DIGIT environment. It will not be needed to run the application locally.
{% endhint %}

MDMS data is the master data used by the application. New modules with master data need to be configured inside the `/data/<tenant>/` folder of the MDMS repo. Each tenant should have a unique ID and sub-tenants can be configured in the format state.cityA, state.cityB etc..Further hierarchies are also possible with tenancy.&#x20;

{% hint style="info" %}
For more information on [MDMS](../../../../platform/core-services/mdms-master-data-management-service/) see here. To read about how to design for MDMS, please see the [design guide](../../../design-guide/design-services.md#identify-reference-data).
{% endhint %}

In the birth registration use case, we will use the following master data:

1\. tenantId = "pb"

2\. User roles - CITIZEN and EMPLOYEE roles configured in roles.json (see below section for more info)

3\. Actions - URIs to be exposed via Zuul (see below section for more info)

4\. Role-action mapping - for access control (see below section for more info)

{% hint style="info" %}
Make sure to add data to the **correct branch** of the MDMS repository. i.e. if you have setup CD CI to deploy the **DEV** branch of the repository to the dev environment (default), then make sure to add the information in the DEV branch. If you are testing in staging or some other environment, make sure to add the master data to the corresponding branch of MDMS.&#x20;
{% endhint %}

Create a folder called "pb" in the data folder of the MDMS repository "DEV" branch. You will have a new folder path as follows:

`<MDMS repo URL path>/data/pb`

Once data is added to MDMS repository, MDMS service in the dev environment where DIGIT is running has to be restarted which will then load the newly added/updated MDMS configs. A sample MDMS config file can be viewed here - [Sample MDMS data file](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/common-masters/Department.json).

### API Access Control Configuration

URIs (actions), roles and URI-role mapping will be defined in MDMS. These will apply when the module is deployed into an environment  where Zuul is involved (not while locally running the app). In this sample app, we have used "pb" as a tenantId. In your environment, you can choose to define a new one or work with an existing one.&#x20;

All folders mentioned below need to be created under the `data/pb` folder in MDMS.

{% hint style="info" %}
You can choose to use some other tenantId. Make sure to change the tenant ID everywhere.
{% endhint %}

#### Actions

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

Note that the IDs in the actions.json config are manually generated

#### Roles configuration

Roles config happens at a state level. For birth registration, we need only CITIZEN and EMPLOYEE roles in the /`data/pb/ACCESSCONTROL-ROLES/roles.json` file.Here are some [sample roles ](https://github.com/egovernments/egov-mdms-data/tree/UAT/data/pg/ACCESSCONTROL-ROLES) that can be defined in an environment. If these roles are already present in the file, then there is no need to add them in again.

#### Role-action mapping

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

_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
