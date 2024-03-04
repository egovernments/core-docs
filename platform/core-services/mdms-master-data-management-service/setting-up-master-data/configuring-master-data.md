# Configuring Master Data

## Overview

Configuring master data for a new module requires creating a new module in the master config file and adding master data. For better organizing, create all the master data files belonging to the module in the same folder. Organizing in the same folder is not mandatory it is based on the moduleName in the master data file.

## Pre-requisites

Before you proceed with the configuration, make sure the following pre-requisites are met -

* User with permission to edit the git repository where MDMS data is configured.

## Key Functionalities

These data can be used to validate the incoming data.

## Deployment Details

After adding the new module data, the MDMS service needs to be restarted to read the newly added data.

## Configuration Details

### **Add New Module**

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

The new module can be added below the existing modules in the master config file.

### **Create Masters Data**

Please check the link to create a new master[ Adding New Master](adding-new-master.md)

## Reference Docs

### Doc Links

| Description                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------- |
| [Sample master config file](https://github.com/egovernments/playground-mdms-data/blob/master/master-config.json) |
| [Sample module folder](https://github.com/egovernments/playground-mdms-data/tree/master/data/pg/TradeLicense)    |
