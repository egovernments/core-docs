---
description: Describes how to integrate with DIGIT's ID Gen service
---

# Integration with IDGen Service

Each application needs to have a unique ID. The [IDGen service](../../../../platform/overview/core-services/id-generation-service.md) generates these unique IDs. ID format can be customised via configuration in MDMS.&#x20;

i) Add the ID format that needs to be generated in this file - [Id Format Mdms File](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/common-masters/IdFormat.json). The following config has been added for this module:

```
{
"format": "PB-BTR-[cy:yyyy-MM-dd]-[SEQ_EG_BTR_ID]",
"idname": "btr.registrationid"
}
```

ii) Now, restart IDGen service and MDMS service and port-forward IDGen service to port 8285:

```
kubectl port-forward <IDGEN_SERVICE_POD_NAME> 8285:8080
```

{% hint style="info" %}
Note that you can set the ID format  in the application.properties file of IDGen service and run the service locally if you don't have access to a DIGIT environment.&#x20;
{% endhint %}

iv) Hit the following curl to verify that the format is added properly. The "ID" name needs to match exactly with what was added in MDMS.

```bash
curl --location --request POST 'http://localhost:8285/egov-idgen/id/_generate' \
--header 'Content-Type: application/json' \
--data-raw '{
    "RequestInfo": {
        "apiId": "string",
        "ver": "string",
        "ts": null,
        "action": "string",
        "did": "string",
        "key": "string",
        "msgId": "string",
        "authToken": "6456b2cf-49ca-47c7-b7b6-c179f19614c7",
        "correlationId": "e721639b-c095-40b3-86e2-acecb2cb6efb",
        "userInfo": {
            "id": 23299,
            "uuid": "e721639b-c095-40b3-86e2-acecb2cb6efb",
            "userName": "9337682030",
            "name": "Abhilash Seth",
            "type": "EMPLOYEE",
            "mobileNumber": "9337682030",
            "emailId": "abhilash.seth@gmail.com",
            "roles": [
                {
                    "id": 281,
                    "name": "Employee"
                }
            ]
        }
    },
    "idRequests": [
        {
            "tenantId": "pb.amritsar",
            "idName": "btr.registrationid"
        }
    ]
}'
```

v) Once verified, we can call the ID generation service from within our application and generate the registrationId.&#x20;

Add the following model POJOs under `models` folder:

IdGenerationRequest.java

```java
package digit.web.models;

import com.fasterxml.jackson.annotation.JsonProperty;
import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;
import org.egov.common.contract.request.RequestInfo;

import java.util.List;

@Data
@AllArgsConstructor
@NoArgsConstructor
@Builder
public class IdGenerationRequest {

    @JsonProperty("RequestInfo")
    private RequestInfo requestInfo;

    private List<IdRequest> idRequests;

}
```

IdGenerationResponse.java

```java
package digit.web.models;

import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;
import org.egov.common.contract.response.ResponseInfo;

import java.util.List;


@Data
@AllArgsConstructor
@NoArgsConstructor
@Builder
public class IdGenerationResponse {

    private ResponseInfo responseInfo;

    private List<IdResponse> idResponses;

}

```

IdRequest.java

```java
package digit.web.models;
import com.fasterxml.jackson.annotation.JsonProperty;
import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

import javax.validation.constraints.NotNull;


@Data
@AllArgsConstructor
@NoArgsConstructor
@Builder
public class IdRequest {

    @JsonProperty("idName")
    @NotNull
    private String idName;

    @NotNull
    @JsonProperty("tenantId")
    private String tenantId;

    @JsonProperty("format")
    private String format;

}

```

IdResponse.java

```java
package digit.web.models;

import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;


@Data
@AllArgsConstructor
@NoArgsConstructor
@Builder
public class IdResponse {

    private String id;

}
```

In the BirthApplicationEnrichment class, update the enrichBirthApplication method as shown below:

```java
public void enrichBirthApplication(BirthRegistrationRequest birthRegistrationRequest) {
        //Retrieve list of IDs from IDGen service
        List<String> birthRegistrationIdList = idgenUtil.getIdList(birthRegistrationRequest.getRequestInfo(), birthRegistrationRequest.getBirthRegistrationApplications().get(0).getTenantId(), "btr.registrationid", "", birthRegistrationRequest.getBirthRegistrationApplications().size());
        Integer index = 0;
        for(BirthRegistrationApplication application : birthRegistrationRequest.getBirthRegistrationApplications()) {
            // Enrich audit details
            AuditDetails auditDetails = AuditDetails.builder().createdBy(birthRegistrationRequest.getRequestInfo().getUserInfo().getUuid()).createdTime(System.currentTimeMillis()).lastModifiedBy(birthRegistrationRequest.getRequestInfo().getUserInfo().getUuid()).lastModifiedTime(System.currentTimeMillis()).build();
            application.setAuditDetails(auditDetails);

            // Enrich UUID
            application.setId(UUID.randomUUID().toString());

            // Set application number from IdGen
            application.setApplicationNumber(birthRegistrationIdList.get(index++));
            
            // Enrich registration Id
            application.getAddress().setRegistrationId(application.getId());

            // Enrich address UUID
            application.getAddress().setId(UUID.randomUUID().toString());
        }
    }
```

Make sure below ID generation host configuration is present in the application.properties file. Make sure to fill in the correct values for the host.

```properties
#Idgen Config
egov.idgen.host=http://localhost:8285/ #REPLACE
egov.idgen.path=egov-idgen/id/_generate
```

_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
