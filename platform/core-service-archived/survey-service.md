# Survey Service

## Overview <a href="#overview" id="overview"></a>

Surveys are an important way to close the feedback loop on the services that are delivered by ULBs. Without proper surveys, ULB employees will never know how happy the citizens are, about the services they consume and what the areas of improvement are.

The surveys section will be used by ULB employees to create citizen surveys to make better-informed decisions while issuing new policies/ feedback on existing services.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

1. Prior knowledge of Java/J2EE.
2. Prior knowledge of SpringBoot.
3. Prior knowledge of PostgresSQL.
4. Prior knowledge of REST APIs and related concepts like path parameters, headers, JSON etc.
5. Prior knowledge of JSONQuery in Postgres. (Similar to PostgresSQL with a few aggregate functions.)

## Key Functionalities  <a href="#key-functionalities-and-configurations" id="key-functionalities-and-configurations"></a>

This service allows -

* Employees - to create, edit, and delete surveys
* Employees - to share survey results with other employees/citizens
* Citizens - to fill out surveys

Each survey entity will have questions associated with it. Questions can be of -

1. short answer type
2. long answer type
3. multiple answers type
4. checkbox answer type
5. date answer type
6. time answer type

## Configuration Details

Survey entities will have a collectCitizenInfo flag associated with them, if that flag is set to true, the mobile number and email address of the citizens responding to the survey will be captured. If it is set to false, responding to the survey will be completely anonymous.

Surveys will have a startDate and endDate associated with them. Within that period, those surveys will be shown in the active section. However, in case the survey has been manually marked inactive by the employee during its active period, that survey will be shown under the inactive surveys section. Citizens can look at active survey entities and submit their responses for that survey.

Once a survey is created, it can be searched with the following parameters -&#x20;

1. tenantIds - To search surveys based on multiple ULBs
2. title - To search surveys based on survey names
3. postedBy - To search surveys based on the employee who created the survey
4. status - To search surveys based on status

Also, if any created survey needs to be updated -

1. Before the survey becomes active, users can edit all the fields.
2. Once the survey becomes Live user can only change&#x20;
   * Survey Description
   * End date and time of the survey

In case of deletion of a survey, the survey will be soft deleted i.e. the ‘active’ boolean field will be set to false and it will not appear in search results.

### API Details <a href="#api-details" id="api-details"></a>

APIs for interacting with survey service are available in the [collection here](https://www.getpostman.com/collections/76c0ee0703fab656835d).
