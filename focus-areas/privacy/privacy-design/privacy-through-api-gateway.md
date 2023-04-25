---
description: Ensuring privacy through APIs
---

# Privacy through API Gateway

## Overview

One of the approaches to keep data secure is to encrypt the data as soon as it enters the system and decrypt it only when necessary.&#x20;

![Security at Gateway](<../../../.gitbook/assets/Privacy Design-Security at Gateway.drawio.png>)

## Securing Data

This can be enabled by first identifying the PII present in every request body and then encrypting those attributes of the request body at the API gateway.&#x20;

## Plain/Masked Access&#x20;

As any microservice is not decrypting any of the secured values, the response body that reaches the API gateway would have encrypted values. The service owner will have to define a Data Access Policy for every response schema that could contain some secured values. This data access policy will contain role-based attribute-level access rules.&#x20;

As we are encrypting the values even before the request reaches its service, there would be cases where the receiving service or any other service down the pipeline would expect to read the value in plain like when validating the value. The service will have to request to decrypt the value when necessary. For example, when an SMS service wants to send an SMS to a mobile number present in the JSON body, then the SMS service will have to request the plain value of the mobile number. It will be a client(service) requesting decryption, not any user.&#x20;

## Points Of Intervention

As any business service will receive encrypted value in the request body, it will not be able to directly have format validations as part of the Java Model Class. Any unnecessary validations will have to be removed such as the property service would receive a mobile number as part of a search request but if it is not doing any mobile number lookup in its own database then it should not validate if the mobile number is exactly 10-digit long. Property service will have to leave it up to the user service to validate that.&#x20;

Apart from the changes at the gateway, which is the fundamental change to enforce privacy, changes might be required at the following places:

1. The direct format validations present in the Java model classes will have to be removed for the secured values.&#x20;
2. Making an extra decryption API call wherever plain value access is necessary to proceed, like validations and the example of SMS service mentioned above. We will need a detailed analysis of all the places in the system where plain access to PII might be required and add the code there to decrypt the value.&#x20;
