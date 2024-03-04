# Guidelines for supporting User Privacy in a module

## Overview <a href="#overview" id="overview"></a>

This documents highlights the changes need to be done in a module to support the user privacy feature.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

* Prior Knowledge of Java/J2EE.
* Prior Knowledge of Spring Boot.
* MDMS Service
* Encryption Service
* Prior Knowledge of React Js / Javascript

### Backend service changes <a href="#backend-service-changes" id="backend-service-changes"></a>

#### Update the pom.xml file. <a href="#update-the-pom.xml-file." id="update-the-pom.xml-file."></a>

* Upgrade services-common library version.

```java
<dependency>
    <groupId>org.egov.services</groupId>
    <artifactId>services-common</artifactId>
    <version>1.1.1-SNAPSHOT</version>
</dependency>


```

* Upgrade tracer library version.

```
<dependency>
    <groupId>org.egov.services</groupId>
    <artifactId>tracer</artifactId>
    <version>2.1.2-SNAPSHOT</version>
</dependency>
```

{% hint style="info" %}
After upgrading the above library version, there might be chance that an issue occur for RequestInfo creation because of change in variable type, please go through all java files including JUnit test cases before pushing the changes.
{% endhint %}

{% hint style="info" %}
The above library version need to be upgraded in the dependant module also.\
**For Example:** If water service call the property service and property service is calling user service for owner details then the version of above library need to be upgraded in property service pom file also.
{% endhint %}

### Demand generation changes: <a href="#demand-generation-changes" id="demand-generation-changes"></a>

At service level or calculator service level where demand generation process take place, there payer details value must be pass in plain form. And these user details must get through SYSTEM user.

Create a system user in the particular environment and make sure that system user has role `INTERNAL_MICROSERVICE_ROLE`. Use the curl mentioned below:

```
curl --location --request POST 'http://localhost:8081/user/users/_createnovalidate' \
--header 'Content-Type: application/json' \
--data-raw '{
    "RequestInfo": {
  "apiId": "Rainmaker",
  "authToken": "81a67bd9-3ff6-402c-ae59-d9209c9dfb3d",
  "userInfo": {
    "id": 29836,
    "uuid": "d8854322-a078-41f8-90b5-6f3a1aee9454",
    "userName": "qeroo",
    "name": "QARoo",
    "mobileNumber": "8339358368",
    "emailId": "",
    "locale": null,
    "type": "EMPLOYEE",
    "roles": [
      
      {
        "name": "Employee",
        "code": "EMPLOYEE",
        "tenantId": "pb.amritsar"
      },
      {
        "name": "Super User",
        "code": "SUPERUSER",
        "tenantId": "pb.amritsar"
      }
    ],
    "active": true,
    "tenantId": "pb.amritsar",
    "permanentCity": null
  },
  "msgId": "1653559822522|en_IN"
},
    "user": {
        "userName": "INTERNAL_MICROSERVICE_USER",
        "password": "eGov@123",
        "salutation": null,
        "name": "Internal Microservice User",
        "gender": null,
        "mobileNumber": "8888888880",
        "emailId": null,
        "altContactNumber": "",
        "pan": null,
        "aadhaarNumber": null,
        "permanentAddress": null,
        "permanentCity": null,
        "permanentPincode": null,
        "correspondenceCity": null,
        "correspondencePincode": null,
        "correspondenceAddress": null,
        "active": true,
        "dob": null,
        "pwdExpiryDate": null,
        "locale": "string",
        "type": "SYSTEM",
        "signature": null,
        "accountLocked": false,
        "fatherOrHusbandName": "null",
        "bloodGroup": null,
        "identificationMark": null,
        "photo": null,
        "otpReference": null,
        "tenantId": "pb",
        "roles": [
           {
                    "code": "INTERNAL_MICROSERVICE_ROLE",
                    "name": "Internal Microservice Role",
                    "tenantId": "pb"
            }
        ]
    }
}'
```

{% hint style="info" %}
Do not create the system user with `INTERNAL_MICROSERVICE_ROLE` if it is already existed. Use the UUID of that user, to get plain result data.
{% endhint %}

\
Mention the uuid of the system user in the environment file and in the application.properties file of service\
example:

Environment file:

`egov-internal-microservice-user-uuid: b5b2ac70-d347-4339-98f0-5349ce25f99f`

Application properties file:

`egov.internal.microservice.user.uuid=b5b2ac70-d347-4339-98f0-5349ce25f99f`

&#x20;

Create a method/ function which call the user search API to get the user details in plain form, in that call pass the userInfo of the user with `INTERNAL_MICROSERVICE_ROLE`

For reference follow the below code snippet

```
private User getPlainOwnerDetails(RequestInfo requestInfo, String uuid, String tenantId){
		User userInfoCopy = requestInfo.getUserInfo();
		StringBuilder uri = new StringBuilder();
		uri.append(configs.getUserHost()).append(configs.getUserSearchEndpoint()); // URL for user search call
		Map<String, Object> userSearchRequest = new HashMap<>();
		tenantId = tenantId.split("\\.")[0];

		//Creating role with INTERNAL_MICROSERVICE_ROLE
		Role role = Role.builder()
				.name("Internal Microservice Role").code("INTERNAL_MICROSERVICE_ROLE")
				.tenantId(tenantId).build();

        //Creating userinfo with uuid and role of internal micro service role
		User userInfo = User.builder()
				.uuid(configs.getEgovInternalMicroserviceUserUuid())
				.type("SYSTEM")
				.roles(Collections.singletonList(role)).id(0L).build();

		requestInfo.setUserInfo(userInfo);

        // Setting user search criteria
		userSearchRequest.put("RequestInfo", requestInfo);
		userSearchRequest.put("tenantId", tenantId);
		userSearchRequest.put("uuid",Collections.singletonList(uuid));
		User user = null;
		try {
			LinkedHashMap<String, Object> responseMap = (LinkedHashMap<String, Object>) serviceRequestRepository.fetchResult(uri, userSearchRequest);

			List<LinkedHashMap<String, Object>> users = (List<LinkedHashMap<String, Object>>) responseMap.get("user");
			String dobFormat = "yyyy-MM-dd";
			
			// parsing the user response and coverting object into User.class pojo
			notificationUtil.parseResponse(responseMap,dobFormat);
			user = 	mapper.convertValue(users.get(0), User.class);

		} catch (Exception e) {
			throw new CustomException("EG_USER_SEARCH_ERROR", "Service returned null while fetching user");
		}
		requestInfo.setUserInfo(userInfoCopy);
		return user;
	}
```

#### Report Configuration Changes: <a href="#report-configuration-changes" id="report-configuration-changes"></a>

For the report where PII data is present and decryption is required, such report definition must have UUID values from user table in the query result.\
And the Source column section of the report definition must have mention of the UUID column and for that entry, `showColumn` flag should be set as **false**.

```
 - name: uuid
    label: reports.{moduleName}.uuid
    type: string
    source: eg_user
    showColumn: false
```

And the base sql query in the report config should be written in such a way that in the query it must have the user uuid.

{% hint style="info" %}
In the config, for **name: uuid**\
Here replace uuid with the name of the column containing the user’s uuid in the query’s output.
{% endhint %}

\
**Example:**

```
SELECT emp_data.id as id,
      emp_data.name as name,
      emp_data.uuid as uuid,
      desigmap_def.code as designation,
      deptmap_def.code as department,
      emp_data.employeestatus as status
    FROM emp_data ehe
    inner join eg_user eu ON ehe.uuid = eu.uuid
```

\
In the report config where PII data is present and decryption is required, add this new filed in the report config `decryptionPathId`. And in the Security Policy mdms file, must have the model configuration from the particular report. And the value of key `model` in Security Policy mdms file and `decryptionPathId` in a report must be same.\
\


**Example**:-

```json
{
  "model": "EmployeeReport",
  "uniqueIdentifier": {
    "name": "uuid",
    "jsonPath": "uuid"
  },
  "attributes": [
    {
      "name": "name",
      "jsonPath": "name",
      "patternId": "002",
      "defaultVisibility": "PLAIN"
    }
  ],
  "roleBasedDecryptionPolicy": [
    {
      "roles": [
        "CEMP"
      ],
      "attributeAccessList": [
        {
          "attribute": "name",
          "firstLevelVisibility": "MASKED",
          "secondLevelVisibility": "PLAIN"
        }
      ]
    }
  ]
}
```

#### Searcher Configuration changes: <a href="#searcher-configuration-changes" id="searcher-configuration-changes"></a>

For the searcher result where PII data is present and decryption is required, such searcher definition must have UUID values from user table in the query result. The base sql query in the searcher config should be written in such a way that in the query it must have the user uuid.

I searcher result, where data are coming from user table and to get those value in decrypted form, then in searcher config these following filed `decryptionPathId`must be present. And the Security Policy mdms file, must have the model configuration from the particular searcher config. And the value of key `model` in Security Policy mdms file and `decryptionPathId` in searcher config must be same.\


For details information on Security Policy MDMS file refer this [document](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/2144862213).

### Frontend Changes: <a href="#frontend-changes" id="frontend-changes"></a>

To Do
