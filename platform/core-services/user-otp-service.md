# User OTP Service

## Overview <a href="#overview" id="overview"></a>

User-OTP service handles the OTP for user registration, user log in and password reset for a particular user.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before you proceed with the documentation, make sure the following pre-requisites are met -

* _Java 17_
* [egov-user](user/) service is running
* [egov-localization](localization-service/) service is running
* [egov-otp](../api-specifications/otp.md) service is running

## Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

The User-OTP service sends the OTP to the user on login request, on password change request and during new user registration.

## Deployment Details <a href="#deployment-details" id="deployment-details"></a>

1. Deploy the latest version of user-otp.
2. Make sure egov-otp is running.
3. Add Role-Action mapping for APIs.

## Integration Details <a href="#integration" id="integration"></a>

### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

User-OTP service handles the OTP for user registration, user login and password reset for a particular user.

### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

* Can perform user registration, login, and password reset.
* In the future, if we want to expose the application to citizens then it can be done easily.

### Integration Steps <a href="#steps-to-integration" id="steps-to-integration"></a>

1. To integrate, the host of user-otp module should be overwritten in the helm chart.
2. `/user-otp/v1/_send` should be added as the endpoint for sending OTP to the user via sms or email

## Reference Docs <a href="#reference-docs" id="reference-docs"></a>

## Play around with the API's : [DIGIT-Playground](https://digit-api.apidog.io/doc-507201)&#x20;

### Doc Links <a href="#doc-links" id="doc-links"></a>

<table><thead><tr><th width="256">Title </th><th>Link</th></tr></thead><tbody><tr><td>API Postman Collection</td><td><a href="https://www.getpostman.com/collections/5a7475c3ec5ad9b06927">Postman Collection</a></td></tr></tbody></table>

### API Details

`BasePath` /user-otp/v1/\[API endpoint]

**Method**

a) `POST /_send`

This method sends the OTP to a user via sms or email based on the below parameters -

<table><thead><tr><th width="172">Input Field</th><th width="184">Description</th><th width="158">Mandatory</th><th width="227">Data Type</th></tr></thead><tbody><tr><td><code>tenantId</code></td><td>Unique id for a tenant.</td><td>Yes</td><td>String</td></tr><tr><td><code>mobileNumber</code></td><td>Mobile number of the user</td><td>Yes</td><td>String</td></tr><tr><td><code>type</code></td><td>OTP type ex: login/register/password reset</td><td>Yes</td><td>String</td></tr><tr><td><code>userType</code></td><td>Type of user ex: Citizen/Employee</td><td>No</td><td>String</td></tr></tbody></table>

#### Producers <a href="#producers" id="producers"></a>

* Following are the Producer topic.
  * `egov.core.notification.sms.otp` :- This topic is used to send OTP to user mobile number.
  * `org.egov.core.notification.email` :- This topic is used to send OTP to user email id.

\
