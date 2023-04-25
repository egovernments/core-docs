# OTP Service

### Overview <a href="#overview" id="overview"></a>

OTP Service is a core service that is available on the DIGIT platform. The service is used to authenticate the user in the platform. The functionality is exposed via REST API.

### Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before you proceed with the documentation, make sure the following pre-requisites are met -

* _Java 8_

### Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

egov-otp is being called internally by user-otp service which fetches mobileNumber and feeds to egov-otp to generate 'n' digit OTP.

### Deployment Details <a href="#deployment-details" id="deployment-details"></a>

1. Deploy the latest version of egov-otp service.
2. Add Role-Action mapping for API’s.

### Integration <a href="#integration" id="integration"></a>

#### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

The egov-otp service is used to authenticate the user in the platform.

#### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

* Can perform user authentication without impacting the other module.
* In the future, this application can be used in a standalone manner in any other platforms that require a user authentication system.

#### Steps to Integration <a href="#steps-to-integration" id="steps-to-integration"></a>

1. To integrate, host of egov-otp module should be overwritten in helm chart.
2. `/otp/v1/_create` should be added as the create endpoint. Create OTP Configuration this API is internal call from v1/\_send end point, this end point present in user-otp service no need of explicity call
3. `/otp/v1/_validate` should be added as the validate endpoint. OTP Configuration this end point is validate the otp respect to mobilenumber
4. `/otp/v1/_search` should be added as the search endpoint. This API searches the mobile number and otp using uuid ,uuid nothing but otp reference number

### Reference Docs <a href="#reference-docs" id="reference-docs"></a>

#### Doc Links <a href="#doc-links" id="doc-links"></a>

| Title                     | Link                                                                                                                                                                  |
| ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| API Swagger Documentation | [Swagger Documentation](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/DIGIT-OSS/doc-patch/core-services/docs/egov-otp-contract.yml#!) |

### API Details <a href="#api-details" id="api-details"></a>

`BasePath` /egov-otp/v1

Egov-otp service APIs - contains create, validate and search end point

a) `POST /otp/v1/_create` - create OTP Configuration this API is internal call from v1/\_send end point, this end point present in user-otp service no need of explicity call

b) `POST /otp/v1/_validate` - validate OTP Configuration this end point is validate the otp respect to mobilenumber

c) `POST /otp/v1/_search` - search the mobile number and otp using uuid ,uuid nothing but otp reference number

### Configuration <a href="#configuration" id="configuration"></a>

Below properties define the OTP configurations

a) `egov.otp.length` : Number of digits in the OTP

b) `egov.otp.ttl` : Controls the validity time frame of the otp. Default value is 900 seconds. Another OTP generated within this time frame is also allowed.

c) `egov.otp.encrypt` : Controls if the otp is encrypted and stored in the table.
