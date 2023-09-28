# Service Request

## Overview

Service request allows users to define a service and then create a service against service definitions. A service definition can be a survey or a checklist which the users might want to define and a service against the service definition can be a response against the survey or a filled-out checklist.

## Pre-requisites

1. Prior knowledge of Java/J2EE
2. Prior knowledge of SpringBoot
3. Prior knowledge of PostgreSQL
4. Prior knowledge of REST APIs and related concepts like path parameters, headers, JSON etc.

## Key Functionalities

Users can -

1. Create and search service definitions.
2. Create and search services.

## API Details

1. /service-request/service/definition/v1/\_create - Takes RequestInfo and ServiceDefinition in request body. ServiceDefinition has all the parameters related to the service definition being created.\

2. /service-request/service/definition/v1/\_search - Allows searching of existing service definitions. Takes RequestInfo, ServiceDefinitionCriteria and Pagination objects in the request body.\

3. /service-request/service/v1/\_create - Takes RequestInfo and Service in the request body. Service has all the parameters related to the service being created against a particular ServiceDefinition.\

4. /service-request/service/v1/\_search - Allows searching of existing services created against service definitions. Takes RequestInfo, ServiceCriteria and Pagination objects in the request body.

Detailed API payloads for interacting with Service Request for all four endpoints can be found in the following collection - [Service Request Collection](https://api.postman.com/collections/12892142-f7bf3d00-6eed-4efc-8cbe-66dd22833f8e?access\_key=PMAT-01GST3SNZDFX2CZ5GW0A69M91K)

### Swagger Documentation

The link to the swagger documentation can be found below - [Service Request Contract](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/DIGIT-OSS/health-checklist-final/core-services/service-request/src/main/resources/service-request-contract.yaml)
