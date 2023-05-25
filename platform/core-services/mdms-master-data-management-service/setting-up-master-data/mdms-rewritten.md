# MDMS Rewritten

## Overview

Master Data Management Service is a core service made available on the DIGIT platform. It encapsulates the functionality surrounding Master Data Management. The service creates, updates and fetches Master Data pertaining to different modules. This eliminates the overhead of embedding the storage and retrieval logic of Master Data into other modules. The functionality is exposed via REST API.

## Pre-requisites <a href="#prerequisites" id="prerequisites"></a>

Prior Knowledge of Java/J2EE, Spring Boot, and advanced knowledge of operating JSON data would be an added advantage to understanding the service.

## Functionality

The MDM service reads the data from a set of JSON files from a pre-specified location. It can either be an online location (readable JSON files from online) or offline (JSON files stored in local memory). The JSON files should conform to a prescribed format. The data is stored in a map and **tenantID** of the file serves as the key.

Once the data is stored in the map the same can be retrieved by making an API request to the MDM service. Filters can be applied in the request to retrieve data based on the existing fields of JSON.

## Setup and Usage

The spring boot application needs **lombok** extension added to your IDE to load it. Once the application is up and running API requests can be posted to the URL.

## Configuration & Structure <a href="#configuration-and-structure" id="configuration-and-structure"></a>

The config JSON files to be written should follow the listed rules

* The config files should have JSON extension.
* The file should mention the tenantId, module name, and master name first before defining the data.

{% code lineNumbers="true" %}
```
{
  "tenantId": "pb",
  "moduleName": "BillingService",
  "{$MasterName}":[ ]
}
```
{% endcode %}

The Master Name in the above sample will be substituted by the actual name of the master data. The array succeeding it will contain the actual data.

Example config JSON for “Billing Service”

{% code lineNumbers="true" %}
```
{
  "tenantId": "pb",
  "moduleName": "BillingService",
 "BusinessService": 
 [
    {
      "businessService": "PropertyTax",
      "code": "PT",
      "collectionModesNotAllowed": [ "DD" ],
      "partPaymentAllowed": true,
      "isAdvanceAllowed": true,
      "isVoucherCreationEnabled": true
    }
]
}
```
{% endcode %}

## API Reference Documentation

APIs are available to create, update and fetch master data pertaining to different modules. Refer to the segment below for quick details.

**BasePath**:/mdms/v1/\[API endpoint]\
**Method**

`POST /_create`

Creates or Updates Master Data on GitHub as JSON files

`MDMSCreateRequest` _Request Info + MasterDetail_ — Details of the master data to be created or updated on GitHub.

**MasterDetail**

<table><thead><tr><th width="153">Input Field</th><th width="440">Description</th><th width="116">Mandatory</th><th>Data Type</th></tr></thead><tbody><tr><td><strong>tenantId</strong></td><td>Unique id for a tenant.</td><td>Yes</td><td>String</td></tr><tr><td><strong>filePath</strong></td><td>file-path on git where master data is to be created or updated</td><td>Yes</td><td>String</td></tr><tr><td><strong>masterName</strong></td><td>Master Data name to be created or updated</td><td>Yes</td><td>String</td></tr><tr><td><strong>masterData</strong></td><td>content to be written on to the Config file</td><td>Yes</td><td>Object</td></tr></tbody></table>

`MdmsCreateResponse` _Response Info_

**Method**

`POST /_search`

This method fetches a list of masters for a specified module and tenantId.

`MDMSCriteriaReq (mdms request) -` _Request Info + MdmsCriteria_ — Details of module and master which need to be searched using MDMS.

**MdmsCriteria**

| Input Field       | Description                              | Mandatory | Data Type |
| ----------------- | ---------------------------------------- | --------- | --------- |
| **tenantId**      | Unique id for a tenant                   | Yes       | String    |
| **moduleDetails** | module for which master data is required | Yes       | Array     |

`MdmsResponse` _Response Info_ + Mdms

**MDMS**

| Input Field | Description      | Mandatory | Data Type |
| ----------- | ---------------- | --------- | --------- |
| **mdms**    | Array of modules | Yes       | Array     |

**Common Request/Response/Error Structures:**

**RequestInfo** should be used to carry meta information about the requests to the server as described in the fields below. All DIGIT APIs will use requestinfo as a part of the request body to carry this meta information. Some of this information will be returned back from the server as part of the ResponseInfo in the response body to ensure correlation.

<table><thead><tr><th width="133">Input Field</th><th width="369">Description</th><th>Mandatory</th><th>Data Type</th></tr></thead><tbody><tr><td><strong>apiId</strong></td><td>unique API ID</td><td>Yes</td><td>String</td></tr><tr><td><strong>ver</strong></td><td>API version - for HTTP based request this will be same as used in path</td><td>Yes</td><td>String</td></tr><tr><td><strong>ts</strong></td><td>time in epoch format: int64</td><td>Yes</td><td>Long</td></tr><tr><td><strong>action</strong></td><td>API action to be performed like _create, _update, _search (denoting POST, PUT, GET) or _oauth etc</td><td>Yes</td><td>String</td></tr><tr><td><strong>DID</strong></td><td>Device ID from which the API is called</td><td>No</td><td>String</td></tr><tr><td><strong>Key</strong></td><td>API key (API key provided to the caller in case of server to server communication)</td><td>No</td><td>String</td></tr><tr><td><strong>msgId</strong></td><td> Unique request message id from the caller</td><td>Yes</td><td>String</td></tr><tr><td><strong>requestorId</strong></td><td>UserId of the user calling</td><td>No</td><td>String</td></tr><tr><td><strong>authToken</strong></td><td>//session/jwt/saml token/oauth token - the usual value that would go into HTTP bearer token</td><td>Yes</td><td>String</td></tr></tbody></table>

**ResponseInfo** should be used to carry metadata information about the response from the server. apiId, ver, and msgId in ResponseInfo should always correspond to the same values in the respective request's RequestInfo.

<table><thead><tr><th width="148">Output Field</th><th width="400">Description</th><th>Mandatory</th><th>Data Type</th></tr></thead><tbody><tr><td><strong>apiId</strong></td><td>unique API ID</td><td>Yes</td><td>String</td></tr><tr><td><strong>ver</strong></td><td>API version</td><td>Yes</td><td>String</td></tr><tr><td><strong>ts</strong></td><td>response time in epoch format: int64</td><td>Yes</td><td>Long</td></tr><tr><td><strong>resMsgId</strong></td><td>unique response message-id (UUID) - will usually be the correlation id from the server</td><td>No</td><td>String</td></tr><tr><td><strong>msgId</strong></td><td>message-id of the request</td><td>No</td><td>String</td></tr><tr><td><strong>status</strong></td><td><p>status of request processing -</p><p><strong>Enum:</strong> <em>SUCCESSFUL (HTTP 201) or FAILED (HTTP 400)</em></p></td><td>Yes</td><td>String</td></tr></tbody></table>

**ErrorRes**

All DIGIT APIs will return ErrorRes in case of failure which will carry ResponseInfo as metadata and Error object as an actual representation of the error. When the request processing status in the ResponseInfo is ‘FAILED’ the HTTP status code 400 is returned.

<table><thead><tr><th width="148">Output Field</th><th width="486">Description</th><th width="139">Mandatory</th><th>Data Type</th></tr></thead><tbody><tr><td><strong>code</strong></td><td>Error Code will be a module-specific error label/code to identify the error. All modules should also publish the Error codes with their specific localized values in localization service to ensure clients can print locale-specific error messages. An example of an error code would be UserNotFound to indicate User Not Found by User/Authentication service. All services must declare their possible Error Codes with a brief description in the error response section of their API path.</td><td>Yes</td><td>String</td></tr><tr><td><strong>message</strong></td><td>English locale message of the error code. Clients should make a separate call to get the other locale description if configured with the service. Clients may choose to cache these locale-specific messages to enhance performance with a reasonable TTL (May be defined by the localization service based on tenant + module combination).</td><td>Yes</td><td>String</td></tr><tr><td><strong>description</strong></td><td>Optional long description of the error to help clients take remedial action. This will not be available as part of the localization service.</td><td>No</td><td>String</td></tr><tr><td><strong>params</strong></td><td>Some error messages may carry replaceable fields (say $1, $2) to provide more context to the message. E.g. Format related errors may want to indicate the actual field for which the format is invalid. Client's should use the values in the param array to replace those fields.</td><td>No</td><td>Array</td></tr></tbody></table>

