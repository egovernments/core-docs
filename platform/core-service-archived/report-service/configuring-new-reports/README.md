# Configuring New Reports

## Overview <a href="#overview" id="overview"></a>

Through report service, useful data get shown for a specific module based on some given criteria like date, locality, financial year, etc.

For example, PT dump report of property tax service you have to select from date to date, financial year etc and based on the criteria we can see all the data fulfilling the criteria. In the response, we see all the details of a property which is paid between the given from date and to date. In case we select the financial year, the property which is paid for that specific financial year is visible.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before you proceed with the configuration, make sure the following pre-requisites are met -

* User with permission to edit the git repository where Reports are configured and knowledge on YAML.
* Prior Knowledge of YAML.
* Prior Knowledge of SQL queries.
* Prior Knowledge of the relation between the tables for which module you are going to write a report.

## Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

* Users can write queries (like SQL queries) for fetching real-time data to display in a UI application.
* Users can apply filters like from date, to date, financial year, etc based on the report configuration.
* Users can download the result in PDF and XLS format.
* User can select or deselect the columns user wants to see.
* User can choose the number of records he/she wants to see on a page.

## Deployment Details <a href="#deployment-details" id="deployment-details"></a>

Once the changes have been done in the report configuration file we have to restart the report service so the report service will read the new configuration.

## Configuration Details <a href="#configuration-details" id="configuration-details"></a>

* To add a new report first add the file path in the [reportFileLocationsv1](https://raw.githubusercontent.com/egovernments/configs/DEV/reports/reportFileLocationsv1.txt). (In this file, the path of the report configuration files gets stored).
  * \<Module Name>=file:///work-dir/configs/reports/config/\<report file name>.yml
  * ex: pgr=file:///work-dir/configs/reports/config/pgr-reports.yml
* Once the file path is added in the file reportFileLocationsv1, go to the folder [/configs/reports/config](https://github.com/egovernments/configs/tree/DEV/reports/config).
* Create a new file and name the file that you have given in the file reportFileLocationsv1.
* Write the report configuration. Once it is done commit those changes.
* Add the role and actions for the new report.
* Restart the MDMS and report service.

## Reference Docs <a href="#reference-docs" id="reference-docs"></a>

### Doc Links <a href="#doc-links" id="doc-links"></a>

| Title                                                                                                           |
| --------------------------------------------------------------------------------------------------------------- |
| [ file-locations](https://raw.githubusercontent.com/egovernments/configs/DEV/reports/reportFileLocationsv1.txt) |
| [report config folder](https://github.com/egovernments/configs/tree/DEV/reports/config)                         |
