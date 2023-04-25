---
description: Configure master data management service
---

# MDMS (Master Data Management Service)

## Overview

The MDMS service aims to reduce the time spent by developers on writing codes to store and fetch master data (primary data needed for module functionality) which doesn’t have any business logic associated with them. Instead of writing APIs and creating tables in different services to store and retrieve data that is seldom changed, the MDMS service keeps them in a single location for all modules and provides data on demand with the help of no more than three lines of configuration.

## **Pre-requisites**

1. Prior knowledge of Java/J2EE
2. Prior knowledge of Spring Boot
3. Prior knowledge of REST APIs and related concepts like path parameters, headers, JSON etc.
4. Prior knowledge of Git
5. Advanced knowledge of how to operate JSON data would be an added advantage to understanding the service

## **Key Functionalities**

* Adds master data for usage without the need to create master data APIs in every module.
* Reads data from GIT directly with no dependency on any database services.

| Environment Variables | Description                                                           |
| --------------------- | --------------------------------------------------------------------- |
| egov.mdms.conf.path   | The default value of folder where master data files are stored        |
| masters.config.url    | The default value of the file URL which contains master-config values |

## Deployment Details <a href="#deployment-details" id="deployment-details"></a>

1. Deploy the latest version of the Mdms-service
2. Add conf path for the file location
3. Add master config JSON path

## **Integration Details**

### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

The MDMS service provides ease of access to master data for any service.

### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

* No time spent writing repetitive codes with no business logic.

### Integration Steps <a href="#steps-to-integration" id="steps-to-integration"></a>

1. To integrate, the host of egov-mdms-service should be overwritten in the helm chart
2. _`egov-mdms-service/v1/_search`_ should be added as the search endpoint for searching master data.
3. MDMS client from eGov snapshots should be added as mvn entity in pom.xml for ease of access since it provides MDMS request pojos.

## Reference Docs

### Doc Links

| Title                                                                                                                                                                                              |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| egov-mdms sample data - [https://github.com/egovernments/egov-mdms-data/tree/DEV/data - Connect to preview](https://github.com/egovernments/egov-mdms-data/tree/DEV/data)                          |
| master-config.json - [https://github.com/egovernments/egov-mdms-data/blob/DEV/master-config.json - Connect to preview](https://github.com/egovernments/egov-mdms-data/blob/DEV/master-config.json) |

### API List <a href="#api-list" id="api-list"></a>

| Title                                                                                        |
| -------------------------------------------------------------------------------------------- |
| [egov-mdms-service/v1/\_search](https://www.getpostman.com/collections/fcc9a71375b674de1308) |

