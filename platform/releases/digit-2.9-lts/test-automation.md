# Test Automation

### Overview

A comprehensive guide on running automated test scripts for various core services.

### Pre-requisites

Before you begin automating DIGIT- LTS's core services, please ensure the Postman tool is installed.

{% hint style="info" %}
_**Note**:- It is mandatory to run the automated script for user services, As User collection includes requests to create users, a crucial step as access to all resources requires a user._
{% endhint %}

### Steps&#x20;

Follow the steps below to run the egov-User service automation scripts.\


**1. Import User Collection:** To import the User Collection into Postman, follow the steps outlined in the [User Collection Document](https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit?usp=sharing). Access the Google document to proceed.

**2. Port Forward to Digit-LTS Environment:** Replace `[userPod]` with the relevant user pod name.

```shell
kubectl port-forward [userPod] 8081:8080 -n egov
```

Port-forward to the Digit-LTS environment to create the first user using the command above.

**3. Run the User Collection:** To download the CSV file, please follow this link: [Download CSV](https://docs.google.com/spreadsheets/d/10UxoY9FaIn5iLiQKQvt458TEwqTAx8EQsR0BmdQKkBE/edit?usp=sharing). Make sure to download the file before proceeding with the User collection.

In the CSV file, each cell in the first row UserFIRST, UserName2, and UserName3  represents a unique user and each cell in the second row represents a name given to a specific user.

For example: The first cell in the first row that is UserFIRST represents the first user and USERDemoM1 represents the name given to user UserFIRST.

| UserFIRST  | UserName2  | UserName3  |
| ---------- | ---------- | ---------- |
| USERDemoM1 | EGOvDemoM2 | EGOvDemoM3 |

* Open the User collection in Postman and click the "Run" button.

<figure><img src="https://lh7-us.googleusercontent.com/_6-JwZSB3nddFUyYe8L2d5xwkz-eNwoAQkP7m4IZW2XQwQJWDgz5i0L8KRazKs97gReDu7lKE-tOtDM_zOBvuBIDc0TlkBZw10_Jnvw-vvaZ7QA4TvPlW4zZeNegIvs4o1mPlhCwbB9z0SdO2h_37g" alt=""><figcaption></figcaption></figure>

* Select the downloaded CSV file by clicking on the "Select File" button

<figure><img src="https://lh7-us.googleusercontent.com/v6VBtYJ0VHl8S7osw3_ggUMdLuVHjyREtRNSijJZjs5Qx5RjD51ctUG4jajGqr9Y0kMG_B9O_RSubI0ZFmAd9ocmHgjOwIiPbMOilmRWQEgRVVwTWDudCk-D9m1eJS3t034T-m_HsYCbI5fxXEoaTg" alt=""><figcaption></figcaption></figure>

* Click on the "Run User" button to execute the collection.

{% hint style="info" %}
_Due to the uniqueness constraint on usernames, you cannot create duplicate users with the same username._&#x20;

**IMPORTANT**: To avoid errors when executing the User collection multiple times in the same environment, remember to modify the username in the CSV file for each execution.\

{% endhint %}

### **Additional Notes**

* The provided steps automate the creation of users in the DIGIT-LTS environment, which is essential for accessing all resources.
* Make sure to review and modify the CSV file as needed to include accurate user data.
* For further assistance or troubleshooting, refer to the Postman documentation or reach out to the relevant support channels.
* By following these steps, you can effectively automate the core services of Digit-LTS, starting with the User service, using Postman.

### Test Automation - Localization service

1. Import Localization Collection into Postman: &#x20;

Copy the Localization collection link from the provided document link: [https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit?usp=sharing). Open Postman and import the collection.

2. Prepare CSV File:

Download the CSV file from the provided link: [https://docs.google.com/spreadsheets/d/1swMoCCVHpNnohmVp\_HbbfeykP1t0ZXy9ugQAii7UOWA/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1swMoCCVHpNnohmVp\_HbbfeykP1t0ZXy9ugQAii7UOWA/edit?usp=sharing).

Make sure the CSV file is in the correct format.

3. Run localization Collection in Postman:

Open the localization collection in Postman by clicking on localization collection.

Click on the "Run" button to execute the collection.

4. Select CSV File:

When prompted, select the downloaded CSV file by clicking on the "Select File" button.

5. &#x20;Run Collection:

After selecting the CSV file, click on the "Run Collection" button to execute the collection.

{% hint style="info" %}
_**Note**: Ensure that if running the Localization collection multiple times within the same environment, you change the locale and code within the CSV file each time._
{% endhint %}

The "locale" column in the CSV file represents the place/area where you are creating the message (mandatory).

The "code" column represents the unique code associated with the message.

By following these steps, you can automate the localization services using Postman.

### Test Automation -  Egov-OTP Services

1\. Import Egov OTP Collection into Postman:

* Copy the Egov OTP collection link from the provided document link: [https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit?usp=sharing).
* Open Postman and import the collection.

2\. To Run Egov OTP Collection in Postman:

* Open the Egov OTP collection in Postman by clicking on Egov OTP collection.
* Click on the "Run" button to execute the collection.
* Click on the "Run Collection" button to execute the collection.

### Test Automation - MDMS Service

1\. Import MDMS Collection into Postman:

* Copy the MDMS collection link from the provided document link: [https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit?usp=sharing.](https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit?usp=sharing)
* Open Postman and import the collection.

2\. To Run MDMS Collection in Postman:

* Open the MDMS collection in Postman by clicking on MDMS collection.
* Click on the "Run" button to execute the collection.
* Click on the "Run Collection" button to execute the collection.

### Test Automation - URL Shortening Service

1\. Import Url shortening Collection into Postman:

* Copy the Url shortening collection link from the provided document link: [https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit?usp=sharing).
* Open Postman and import the collection.\


2\. To Run URL - shortening Collection in Postman:

* Open the URL shortening collection in Postman by clicking on the URL shortening collection.
* Click on the "Run" button to execute the collection.
* Click on the "Run Collection" button to execute the collection.\


### Test Automation -  egov-location Service

1\. Import Location Collection into Postman:

* Copy the Location collection link from the provided document link: [https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit?usp=sharing).
* Open Postman and import the collection.

2\. To Run Location Collection in Postman:

* Open the Location collection in Postman by clicking on Location collection.
* Click on the "Run" button to execute the collection.
* Click on the "Run Collection" button to execute the collection.

### Test Automation - access-control Service

1\. Import Access control Collection into Postman:

* Copy the Access control collection link from the provided document link: [https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit?usp=sharing).
* Open Postman and import the collection.

2\. To Run Access control Collection in Postman:

* Open the Access control collection in Postman by clicking on Access control collection.
* Click on the "Run" button to execute the collection.
* Click on the "Run Collection" button to execute the collection.

### Test Automation - Filestore Service

1\. Import Filestore Collection into Postman:

* Copy the Filestore collection link from the provided document link: [https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit?usp=sharing).
* Open Postman and import the collection.

2\. To Run Filestore Collection in Postman:

* Open the Filestore collection in Postman by clicking on Filestore collection.
* Click on the "Run" button to execute the collection.
* Click on the "Run Collection" button to execute the collection.

### Test Automation - egov- Idgen Service

1\. Import Id gen Collection into Postman:

* Copy the Id gen collection link from the provided document link: [https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit?usp=sharing).
* Open Postman and import the collection.

2\. To Run Id gen Collection in Postman:

* Open the Id gen collection in Postman by clicking on Id gen collection.
* Click on the "Run" button to execute the collection.
* Click on the "Run Collection" button to execute the collection.

### Test Automation - Workflow Service

1\. Importing WorkFlow Collection:

* Access the Google document [https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit?usp=sharing) copy WorkFlow collection link and import the WorkFlow collection into Postman.

2\. Running the WorkFlow Collection:

* Before executing the WorkFlow collection, download the CSV file from [https://docs.google.com/spreadsheets/d/1bB3R5faJFfRC0cGZbtPBhv1bmKm\_MsH1upnuC3s2hso/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1bB3R5faJFfRC0cGZbtPBhv1bmKm\_MsH1upnuC3s2hso/edit?usp=sharing) in CSV format.
* Open the WorkFlow collection in Postman and click on the "Run" button.
* Select the downloaded CSV file by clicking on the "Select File" button.
* Click on the "Run Workflow" button to execute the collection.

Additionally, you must update the columns `BusinessIdFirst` and `BusinessIdTwo` in your application for a successful transition.

**IMPORTANT:** If you execute the WorkFlow collection multiple times in the same environment, it's essential to rename the services listed under the columns `BUSINESSSERVICE`, `BUSINESSSERVICETHIRD`, and `BUSINESSSERVICEFOURTH` in the CSV file for each execution to avoid conflicts.

**Additional Notes**: You can also modify other columns but not mandatory.

### Test Automation - Encryption Service

1\. Importing Encryption Collection:

* Access the Google document [https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1xTkC\_IeKjWJOWQcD0kXazoFtEPcSG1civVfEHGmIqMM/edit?usp=sharing) copy Encryption collection link and import the Encryption collection into Postman.

2\. Port Forwarding to Digit-LTS Environment:

* Port-forward to the Digit-LTS environment to decrypt the Encrypted data. Use the following command:
* kubectl port-forward \[Encryption] 8081:8080 -n egov
* Replace \[Encryption] with the relevant Encryption pod name.

3\. Running the Encryption Collection:

* Before executing the Encryption collection, download the CSV file from [https://docs.google.com/spreadsheets/d/1qwtZ2AG60cIgZlMhZ3YN\_j58vMJgx1uovY8nlKThinM/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1qwtZ2AG60cIgZlMhZ3YN\_j58vMJgx1uovY8nlKThinM/edit?usp=sharing) in CSV format.

In CSV file , cell in first row UserFIRST,UserName2,UserName3  represents unique user and each cell in second row represent name given to specific user.

For example: The first cell in the first row that is UserFIRST represents the first user and USERDemoM1 represents the name given to the user UserFIRST.

| UserForEncy |
| ----------- |
| EncUser1    |

* Open the User collection in Postman and click on the "Run" button.
* Select the downloaded CSV file by clicking on the "Select File" button.
* Click on the "Run EncyptionApi" button to execute the collection.

{% hint style="info" %}
**IMPORTANT**: When executing the Encryption collection more than once in the same environment, it's essential to modify the username in the CSV file for every run. This ensures the newly created user has the necessary permissions to encrypt and decrypt data.&#x20;
{% endhint %}

