# Adding New Master

## Overview

For creating a new master in MDMS, create the JSON file with the master data and configure the newly created master in the master config file.

## Pre-requisites

Before proceeding with the configuration, make sure the following pre-requisites are met -

* User with permission to edit the git repository where MDMS data is configured.

## Deployment Details

After adding the new master, the MDMS service needs to be restarted to read the newly added data.

## Configuration Details

### **Creating Master JSON**

The new JSON file needs to contain 3 keys as shown in the below code snippet.\
The new master can be created either State-wise or ULB-wise. Tenant ID and config in the master config file determine this.

```
{
  "tenantId": "< TENANT ID >",
  "moduleName": "< MODULE NAME >",
  "< MASTER NAME >": []
}
```

### **Configuring Master Config File**

The master config file is structured as below. Each key in the master config is a module and each key in the module is a master.

```
{
  "<module1>":{
    "<master1>":{},
    "<master2>":{},
    ...
  },
  "<module2>":{
    <master3>:{},
    <master4>:{},
    ...
  },
  ...
}
```

Each master contains the following data and the  keys are self-explanatory

```
"master":{
    "masterName": "<>",
    "isStateLevel": true,
    "uniqueKeys": []
}
```

## Reference Docs

### Doc Links

| Description                                                                                                                                               |
| --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Sample master file](https://github.com/egovernments/playground-mdms-data/blob/master/data/pg/PropertyTax/ConstructionType.json)                          |
| [Sample master configuration](https://github.com/egovernments/playground-mdms-data/blob/081a232c26be11a9d803d4490e01d49a7e35985c/master-config.json#L561) |

