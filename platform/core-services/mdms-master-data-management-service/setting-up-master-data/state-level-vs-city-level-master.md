# State Level Vs City Level Master

## Overview <a href="#overview" id="overview"></a>

MDMS supports the configuration of data at different levels. While we enable a state there can be data that is common to all the ULBs of the state and data specific to each ULB. The data further can be configured at each module level as state-specific or ULB’s specific.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before you proceed with the configuration, make sure the following pre-requisites are met -

* Prior Knowledge of Java/J2EE.
* Prior Knowledge of Spring Boot.
* Prior Knowledge of REST APIs and related concepts like path parameters, headers, JSON, etc.
* Prior knowledge of Git.
* Advanced knowledge of operating JSON data would be an added advantage to understanding the service.

## Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

* State Level Masters are maintained in a common folder.
* ULB Level Masters are maintained in separate folders named after the ULB.
* Module Specific State Level Masters are maintained by a folder named after the specific module that is placed outside the common folder.

## Deployment Details <a href="#deployment-details" id="deployment-details"></a>

* For deploying the changes(adding new data, updating existing data or deletion) in MDMS, the MDMS service needs to be restarted.

## Configuration Details <a href="#configuration-details" id="configuration-details"></a>

### **State Level Master Configuration**

* The common master data across all ULBs and modules like department, designation, etc are placed under the **common-masters** folder which is under the tenant folder of the MDMS repository.

ex: [**egov-mdms-data**](https://github.com/egovernments/egov-mdms-data)**/**[**data**](https://github.com/egovernments/egov-mdms-data/tree/DEV/data)**/**[**pb**](https://github.com/egovernments/egov-mdms-data/tree/DEV/data/pb)**/common-masters/** Here “**pb**” is the tenant folder name.

* The common master data across all ULBs and are module-specific are placed in a folder named after each module. These folders are placed directly under the tenant folder.

ex: [**egov-mdms-data**](https://github.com/egovernments/egov-mdms-data)**/**[**data**](https://github.com/egovernments/egov-mdms-data/tree/DEV/data)**/**[**pb**](https://github.com/egovernments/egov-mdms-data/tree/DEV/data/pb)**/TradeLicense/** Here “**pb**” is the tenant folder name and “**TradeLicense**“ is the module name.

### **ULB Level Master Configuration**

* Module data that are specific to each ULB like boundary data, interest, penalty, etc are configured at the ULB level. There will be a folder per ULB under the tenant folder and all the ULB’s module-specific data are placed under this folder.

ex: [**egov-mdms-data**](https://github.com/egovernments/egov-mdms-data)**/**[**data**](https://github.com/egovernments/egov-mdms-data/tree/DEV/data)**/**[**pb**](https://github.com/egovernments/egov-mdms-data/tree/DEV/data/pb)**/**[**amritsar**](https://github.com/egovernments/egov-mdms-data/tree/DEV/data/pb/amritsar)**/TradeLicense/** Here “**amritsar**“ is the ULB name and “**TradeLicense**“ is the module name. All the data specific to this module for the ULB are configured inside this folder.

## Reference Docs <a href="#reference-docs" id="reference-docs"></a>

### Doc Links <a href="#doc-links" id="doc-links"></a>

| Description                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------ |
| [State-Level Common-Master Data](https://github.com/egovernments/egov-mdms-data/tree/DEV/data/pb/common-masters)​              |
| [State-Level Module-Specific Common-Master Data](https://github.com/egovernments/egov-mdms-data/tree/DEV/data/pb/TradeLicense) |
| [ULB Specific Data](https://github.com/egovernments/egov-mdms-data/tree/DEV/data/pb/amritsar)                                  |

### API List <a href="#api-list" id="api-list"></a>

| Description                                                                                                                 |
| --------------------------------------------------------------------------------------------------------------------------- |
| [API Contract Reference](https://raw.githubusercontent.com/egovernments/egov-services/master/docs/mdms/contract/v1-0-0.yml) |

