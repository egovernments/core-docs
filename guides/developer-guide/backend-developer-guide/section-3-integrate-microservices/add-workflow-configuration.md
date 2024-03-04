# Add Workflow Configuration

## Overview

Workflow configuration should be created based on the business requirements. More details on [extracting workflow in the design guide](../../../design-guide/model-requirements.md).

## Steps

For our guide, we will configure the following workflow which was the output of the design phase:

![Workflow states, actions and actors](<../../../../.gitbook/assets/image (21) (1).png>)

We will re-use the workflow service which is deployed in the development/sandbox environment.&#x20;

{% hint style="info" %}
This guide assumes you can call the development environment workflow service directly with a **valid auth token**. &#x20;

A sample curl is posted below. Make sure to replace the server hostname and the username and password in the below statement:

```bash
curl --location --request POST 'https://yourserver.digit.org/user/oauth/token' \
--header 'Authorization: Basic ZWdvdi11c2VyLWNsaWVudDo=' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=password' \
--data-urlencode 'scope=read' \
--data-urlencode 'username=<mobile_no_of user>' \
--data-urlencode 'password=<pwd_you_created>' \
--data-urlencode 'tenantId=<your_tenant_id>' \
--data-urlencode 'userType=CITIZEN'
```
{% endhint %}

1. In POSTMan, create a new POST request and paste the below content in the body. The URL for the request is `http://yourserver.digit.org/egov-workflow-v2/egov-wf/businessservice/_create` to create the workflow.

{% hint style="info" %}
Make sure to replace the authToken field in the body with appropriate auth token in your environment. Login to the server as a CITIZEN or EMPLOYEE user (depending on which one you've created) and obtain the authToken from the response body.
{% endhint %}

{% hint style="info" %}
In DIGIT, the API Gateway (Zuul) enriches user information based on the auth token for all requests that go via the gateway. Port forwarding by-passes the API gateway. In this case, when accessing a service directly, for a request to be valid, a user has to send the userInfo JSON **inside the RequestInfo** object. This is true not just for Workflow but for any service. Sample:

`"userInfo": {`

`"id": 24226,`&#x20;

`"uuid": "11b0e02b-0145-4de2-bc42-c97b96264807",`&#x20;

`"userName": "sample_user",`&#x20;

`"roles": [`&#x20;

`{`"name": "Citizen", "code": "CITIZEN"}

]

}

**Note that UUID and roles can be dummy place-holder entities in this case for local testing.**
{% endhint %}

2. Below is the URL and POST body for the business service creation request.&#x20;

```
http://yourserver.digit.org/egov-workflow-v2/egov-wf/businessservice/_create
```

```json
{
   "RequestInfo": {
       "apiId": "Rainmaker",
       "action": "",
       "did": 1,
       "key": "",
       "msgId": "20170310130900|en_IN",
       "requesterId": "",
       "ts": 1513579888683,
       "ver": ".01",
       "authToken": "{{devAuth}}"
   },
   "BusinessServices": [
       {
           "tenantId": "pb",
           "businessService": "BTR",
           "business": "birth-registration",
           "businessServiceSla": 432000000,
           "states": [
               {
                   "sla": null,
                   "state": null,
                   "applicationStatus": null,
                   "docUploadRequired": true,
                   "isStartState": true,
                   "isTerminateState": false,
                   "isStateUpdatable": true,
                   "actions": [
                       {
                           "action": "APPLY",
                           "nextState": "APPLIED",
                           "roles": [
                               "CITIZEN",
                               "EMPLOYEE"
                           ]
                       }
                   ]
               },
               {
                   "sla": null,
                   "state": "APPLIED",
                   "applicationStatus": "APPLIED",
                   "docUploadRequired": false,
                   "isStartState": false,
                   "isTerminateState": true,
                   "isStateUpdatable": false,
                   "actions": [
                       {
                           "action": "APPROVE",
                           "nextState": "APPROVED",
                           "roles": [
                               "EMPLOYEE"
                           ]
                       },
                       {
                           "action": "REJECT",
                           "nextState": "REJECTED",
                           "roles": [
                               "EMPLOYEE"
                           ]
                       }
                   ]
               },
               {
                   "sla": null,
                   "state": "APPROVED",
                   "applicationStatus": "APPROVED",
                   "docUploadRequired": false,
                   "isStartState": false,
                   "isTerminateState": false,
                   "isStateUpdatable": false,
                   "actions": [
                       {
                           "action": "PAY",
                           "nextState": "REGISTRATIONCOMPLETED",
                           "roles": [
                               "SYSTEM_PAYMENT",
                               "CITIZEN",
                               "EMPLOYEE"
                           ]
                       }
                   ]
               },
               {
                   "sla": null,
                   "state": "REJECTED",
                   "applicationStatus": "REJECTED",
                   "docUploadRequired": false,
                   "isStartState": false,
                   "isTerminateState": true,
                   "isStateUpdatable": false,
                   "actions": null
               },
               {
                   "sla": null,
                   "state": "REGISTRATIONCOMPLETED",
                   "applicationStatus": "REGISTRATIONCOMPLETED",
                   "docUploadRequired": false,
                   "isStartState": false,
                   "isTerminateState": true,
                   "isStateUpdatable": false,
                   "actions": null
               }
           ]
       }
   ]
}
```
