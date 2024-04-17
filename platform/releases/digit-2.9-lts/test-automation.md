# Test Automation

## Overview

A comprehensive guide on running automated test scripts for various core services.

## Pre-requisites

Before initiating automating DIGIT- LTS core services, ensure the Postman tool is installed.

Create an environment in Postman with a global variable  BaseUrl and set its value per your environment configuration. For example - we have set &#x20;https://digit-lts.digit.org as the base URL.

&#x20;Import all the services you want to automate in the same environment.[](https://digit-lts.digit.org)

{% hint style="info" %}
_**Note**:- It is mandatory to run the automated script for user services, As User collection includes requests to create users, a crucial step as access to all resources requires a user._
{% endhint %}

## Steps&#x20;

Follow the steps below to run the egov-User service automation scripts.

**1. Import user collection:** Copy the User collection link from the provided document link: [ Collection Document](https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit?usp=sharing) and import the collection in Postman.

**2. Port forward to DIGIT-LTS environment:** Replace `[userPod]` with the relevant user pod name.

```shell
kubectl port-forward [userPod] 8081:8080 -n egov
```

Port-forward to the DIGIT-LTS environment to create the first user using the command above.

**3. Run the user collection:** Click on the [Download CSV](https://docs.google.com/spreadsheets/d/10UxoY9FaIn5iLiQKQvt458TEwqTAx8EQsR0BmdQKkBE/edit?usp=sharing) link to download the CSV file.  Make sure to download the file in CSV format before proceeding with the User collection.

In the CSV file, each cell in the first row UserFIRST, UserName2, and UserName3  represents a unique user and each cell in the second row represents a name given to a specific user.

For example: The first cell in the first row that is UserFIRST represents the first user and USERDemoM1 represents the name given to user UserFIRST.

| UserFIRST  | UserName2  | UserName3  |
| ---------- | ---------- | ---------- |
| USERDemoM1 | EGOvDemoM2 | EGOvDemoM3 |

Open the User collection in Postman and click on the **Run** button.

<figure><img src="https://lh7-us.googleusercontent.com/_6-JwZSB3nddFUyYe8L2d5xwkz-eNwoAQkP7m4IZW2XQwQJWDgz5i0L8KRazKs97gReDu7lKE-tOtDM_zOBvuBIDc0TlkBZw10_Jnvw-vvaZ7QA4TvPlW4zZeNegIvs4o1mPlhCwbB9z0SdO2h_37g" alt=""><figcaption></figcaption></figure>

Select CSV file - Select the downloaded CSV file by clicking on the **Select File** button.

<figure><img src="https://lh7-us.googleusercontent.com/v6VBtYJ0VHl8S7osw3_ggUMdLuVHjyREtRNSijJZjs5Qx5RjD51ctUG4jajGqr9Y0kMG_B9O_RSubI0ZFmAd9ocmHgjOwIiPbMOilmRWQEgRVVwTWDudCk-D9m1eJS3t034T-m_HsYCbI5fxXEoaTg" alt=""><figcaption></figcaption></figure>

Click on the **Run User** button to execute the collection.

{% hint style="info" %}
_Due to the uniqueness constraint on usernames, you cannot create duplicate users with the same username._&#x20;

**IMPORTANT**: To avoid errors when executing the User collection multiple times in the same environment, remember to modify the username in the CSV file for each execution.\

{% endhint %}

### **Additional Notes**

* The provided steps automate the creation of users in the DIGIT-LTS environment, which is essential for accessing all resources.
* Review and modify the CSV file as needed to include accurate user data.
* For further assistance or troubleshooting, refer to the Postman documentation or contact the relevant support channels.
* By following these steps, you can effectively automate the core services of DIGIT-LTS, starting with the User service, using Postman.

### Test Automation - Localization Service

1. **Import Localization Collection into Postman:** [Click here](https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit#gid=0) and copy the localization collection link (available in column B of the sheet). Open the Postman and import the collection.
2. **Prepare CSV File:** [Click here ](https://docs.google.com/spreadsheets/d/1swMoCCVHpNnohmVp\_HbbfeykP1t0ZXy9ugQAii7UOWA/edit#gid=0)to download the CSV file. Make sure the CSV file is in the correct format.
3. **Run localization Collection in Postman:** Open the localization collection in Postman by clicking on localization collection. Click on the Run button to execute the collection.
4. **Select CSV File:** When prompted, click on the Select File button to select the downloaded CSV file.
5. **Run Collection:** After selecting the CSV file, click on the Run Collection button to execute the collection.

In the CSV file, code1 represents the specific code for creating the message in the locale1.&#x20;

The message "Punjab water park" is created in the locale/region/mohalla. A unique code "Alpha pgr 1" is associated with the created message.

| code1       | locale1           |
| ----------- | ----------------- |
| Alpha pgr 1 | Punjab water park |

{% hint style="info" %}
_**Note**: Ensure that if running the Localization collection multiple times within the same environment, you change the locale and code within the CSV file each time._
{% endhint %}

The locale column in the CSV file represents the place/area to create the message (mandatory).

The code column represents the unique code associated with the message.

The above steps automate the localization services using Postman.

### Test Automation -  Egov-OTP Services

1\. Import Egov OTP Collection into Postman:

* [Click here ](https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit#gid=0)to open the document and copy the Egov OTP collection link&#x20;
* Open Postman and import the collection.

2\. To Run Egov OTP Collection in Postman:

* Click on the Egov OTP collection in Postman to open the collection.
* Click on the **Run** button to execute the collection.
* Click on the **Run Collection** button to execute the collection.

### Test Automation - MDMS Service

1\. Import MDMS Collection into Postman:

* [Click here](https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit#gid=0) to open the document and copy the MDMS collection link.
* Open Postman and import the collection.

2\. To run the MDMS Collection in Postman:

* Open the MDMS collection in Postman by clicking on MDMS collection.
* Click on the **Run** button to execute the collection.
* Click on the **Run Collection** button to execute the collection.

### Test Automation - URL Shortening Service

1\. Import Url shortening Collection into Postman:

* [Click here](https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit#gid=0) to open the document and copy the URL shortening collection link.
* Open Postman and import the collection.

2\. To run the URL - shortening collection in Postman:

* Open the URL shortening collection in Postman by clicking on the URL shortening collection.
* Click on the **Run** button to execute the collection.
* Click on the **Run Collection** button to execute the collection.\


### Test Automation -  egov-location Service

1\. Import Location Collection into Postman:

* [Click here](https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit#gid=0) to open the document and copy the location collection link.
* Open Postman and import the collection.

2\. To run Location Collection in Postman:

* Open the Location collection in Postman by clicking on Location collection.
* Click on the **Run** button to execute the collection.
* Click on the **Run Collection** button to execute the collection.

### Test Automation - access-control Service

1\. Import Access control Collection into Postman:

* [Click here](https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit#gid=0) to open the document and copy the Access Control collection link.&#x20;
* Open Postman and import the collection.

2\. To run the Access Control collection in Postman:

* Open the Access Control collection in Postman by clicking on Access Control collection.
* Click on the **Run** button to execute the collection.
* Click on the **Run Collection** button to execute the collection.

### Test Automation - Filestore Service

1\. Import Filestore Collection into Postman:

* [Click here](https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit#gid=0) to open the document and copy the Filestore collection link.
* Open Postman and import the collection.

2\. To run Filestore Collection in Postman:

* Open the Filestore collection in Postman by clicking on the Filestore collection.
* Click on the **Run** button to execute the collection.
* Click on the **Run Collection** button to execute the collection.

### Test Automation - egov- Idgen Service

1\. Import the ID gen Collection into Postman:

* [Click here](https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit#gid=0) to open the document and copy the ID-gen collection link.
* Open Postman and import the collection.

2\. To Run Id gen Collection in Postman:

* Before executing the Id gen collection, download the CSV file from [https://docs.google.com/spreadsheets/d/1bB3R5faJFfRC0cGZbtPBhv1bmKm\_MsH1upnuC3s2hso/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1bB3R5faJFfRC0cGZbtPBhv1bmKm\_MsH1upnuC3s2hso/edit?usp=sharing) in CSV format.
* Open the Id gen collection in Postman by clicking on Id gen collection.
* Click on the "Run" button to execute the collection.
* Click on the "Run Collection" button to execute the collection.

### Test Automation - Workflow Service

1\. Importing WorkFlow Collection:

* [Click here](https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit#gid=0) to open the document, copy the Workflow collection link and import the Workflow collection into Postman.

2\. Running the WorkFlow Collection:

* [Click here](https://docs.google.com/spreadsheets/d/1bB3R5faJFfRC0cGZbtPBhv1bmKm\_MsH1upnuC3s2hso/edit#gid=0) to download the CSV file before executing the WorkFlow collection.
* Open the WorkFlow collection in Postman and click on the **Run** button.
* Select the downloaded CSV file by clicking on the **Select File** button.
* Click on the **Run Workflow** button to execute the collection.

Additionally, you must update the columns `BusinessIdFirst` and `BusinessIdTwo` in your application for a successful transition.

{% hint style="info" %}
**IMPORTANT:** If you execute the WorkFlow collection multiple times in the same environment, it's essential to rename the services listed under the columns `BUSINESSSERVICE`, `BUSINESSSERVICETHIRD`, and `BUSINESSSERVICEFOURTH` in the CSV file for each execution to avoid conflicts.

**Additional Notes**: You can also modify other columns but not mandatory.

_**Note**_: if you are getting error in the transition folder of workflow collection, then change CSV file data and run individual folder (don't run whole Workflow  collection) to avoid error.
{% endhint %}

### Test Automation - Encryption Service

1\. Importing Encryption Collection:

* [Click here](https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit#gid=0) to open the document, copy the Encryption collection link and import the collection into Postman.&#x20;

2\. Port Forwarding to Digit-LTS Environment:

* Port-forward to the Digit-LTS environment to decrypt the Encrypted data. Use the following command:
* kubectl port-forward \[Encryption] 8081:8080-n egov
* Replace \[Encryption] with the relevant Encryption pod name.

3\. Running the Encryption Collection:

* [Click here ](https://docs.google.com/spreadsheets/d/1qwtZ2AG60cIgZlMhZ3YN\_j58vMJgx1uovY8nlKThinM/edit#gid=0)to download the CSV file before executing the Encryption collection.

In CSV file , cell in first row "UserForEncy"  represents unique user and  cell in second row  "EncUser1" represent name given to specific user.

| UserForEncy |
| ----------- |
| EncUser1    |

* Open the User collection in Postman and click on the **Run** button.
* Select the downloaded CSV file by clicking on the **Select File** button.
* Click on the **Run EncyptionApi** button to execute the collection.

{% hint style="info" %}
**IMPORTANT**: When executing the Encryption collection more than once in the same environment, it is essential to modify the username in the CSV file for every run. This ensures the newly created user has the necessary permissions to encrypt and decrypt data.&#x20;
{% endhint %}

