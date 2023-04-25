---
description: Creating users on DIGIT post installation
---

# User Module

## Overview

This doc provides the steps to create and add users on the DIGIT platform post-installation.

## Steps To Create Users

* Run the [kubectl port-forwarding](https://phoenixnap.com/kb/kubectl-port-forward) of the **egov-user** service from the Kubernetes cluster to your local host. This gives you access to egov-user service, bypassing Zuul auth, and you can now interact with the User API directly.

`kubectl port-forward svc/egov-user 8080:8080 -n egov`

You will see below text in the Terminal:

`Forwarding from 127.0.0.1:8080 -> 8080` \
`Forwarding from [::1]:8080 -> 8080`

* Ensure you have installed the Postman utility to run the following scripts. If not, [Install postman](https://www.postman.com/downloads/canary/) on your local machine. Import the [collection](https://www.getpostman.com/collections/b5031f458fc9400c5ade) into Postman. Create an environment variable for “tenantId” and set its value to your tenant.
* The collection creates four types of users and also provides a way to refresh the auth token:
  1. Super User
  2. System User
  3. Citizen
  4. Anonymous User
* Run all the scripts in order.

The refresh auth token script logs into the server and refreshes the token. A sample script is provided for the employee user. Similar scripts can be copied for the citizen/super user etc..for convenience.

#### Sample Json Object

```
{
       "userName": "systemuser",		Can it be changed: Yes
       "name": "systemuser",			Can it be changed: Yes
       "gender": null,			        Can it be changed: Yes
       "mobileNumber": "9999999999",	        Can it be changed: Yes
       "type": "SYSTEM",			Can it be changed: No
       "active": true,				Can it be changed: No
       "password": "eGov@54321",		Can it be changed: Yes
       "roles": [				Can it be changed: No
           {
               "name": "Employee",
               "code": "EMPLOYEE",
               "tenantId": "pg"
           },
           {
               "name": "System user",
               "code": "SYSTEM",
               "tenantId": "pg"
           }
       ],
       "tenantId": "pg"			Can it be changed: No
   }

```
