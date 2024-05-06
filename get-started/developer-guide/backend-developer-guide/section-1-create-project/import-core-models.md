# Import Core Models

## **Overview**

The pom.xml typically includes most of the dependencies listed below at project generation time. Review and ensure that all of these dependencies are present. Update the pom.xml in case any are missing.

## **Steps**

Models/POJOs of the dependent service can be imported from the digit-core-models library (work on creating the library is ongoing). These models are used to integrate with the dependent services.

{% code lineNumbers="true" %}
```xml
<dependency>
      <groupId>org.egov.services</groupId>
      <artifactId>tracer</artifactId>
      <version>2.9.0-SNAPSHOT</version>
 </dependency>
```
{% endcode %}

These are pre-written libraries which contain tracer support, common models like MDMS, Auth and Auth and the capability to raise custom exceptions.

Once these core models are imported, it is safe to delete the RequestInfo, and ResponseInfo classes from the models folder and use the ones present in the common contract that is imported.

### **Import Core Models**

Before starting development, create/update the following classes as given below.

1.  Delete the following classes which have been generated from codegen  -\
    \
    &#x20;\-Address\
    \-AuditDetails\
    \-Document\
    \-Error\
    \-ErrorResponse\
    \-RequestInfo\
    \-RequestInfoWrapper\
    \-ResponseInfo\
    \-Role\
    \-User\
    \-Workflow\
    \
    After this import the above classes from egov common-service library as follow-\


    ```java
    import org.egov.common.contract.models.Address;
    import org.egov.common.contract.models.AuditDetails;
    import org.egov.common.contract.request.RequestInfo;
    import org.egov.common.contract.models.RequestInfoWrapper;
    import org.egov.common.contract.response.ResponseInfo;
    import org.egov.common.contract.request.Role;
    import org.egov.common.contract.request.User;
    import org.egov.common.contract.workflow.*;
    ```


2. Create the BirthApplicationSearchRequest POJO with the following content -

```java
package digit.web.models;
import com.fasterxml.jackson.annotation.JsonProperty;

import org.egov.common.contract.request.RequestInfo;
import org.springframework.validation.annotation.Validated;
import jakarta.validation.Valid;
import jakarta.validation.constraints.*;
import lombok.AllArgsConstructor;
import lombok.NoArgsConstructor;
import lombok.Data;
import lombok.Builder;

/**
 * BirthApplicationSearchCriteria
 */
@Validated
@Data
@AllArgsConstructor
@NoArgsConstructor
@Builder
public class BirthApplicationSearchRequest {

    @JsonProperty("RequestInfo")
    @Valid
    private RequestInfo requestInfo = null;

    @JsonProperty("BirthApplicationSearchCriteria")
    @Valid
    private BirthApplicationSearchCriteria birthApplicationSearchCriteria = null;

}

```

3. &#x20;Update BirthApplicationAddress pojo

```java
package digit.web.models;

import java.util.Objects;
import com.fasterxml.jackson.annotation.JsonProperty;
import com.fasterxml.jackson.annotation.JsonCreator;
import io.swagger.v3.oas.annotations.media.Schema;
import java.util.UUID;

import org.egov.common.contract.models.Address;
import org.springframework.validation.annotation.Validated;
import jakarta.validation.Valid;
import jakarta.validation.constraints.*;
import lombok.AllArgsConstructor;
import lombok.NoArgsConstructor;
import lombok.Data;
import lombok.Builder;

/**
 * BirthApplicationAddress
 */
@Validated
@jakarta.annotation.Generated(value = "org.egov.codegen.SpringBootCodegen", date = "2024-05-03T11:52:56.302336279+05:30[Asia/Kolkata]")
@Data
@AllArgsConstructor
@NoArgsConstructor
@Builder
public class BirthApplicationAddress   {
        @JsonProperty("id")

          @Valid
                private String id = null;

        @JsonProperty("tenantId")
          @NotNull

        @Size(min=2,max=64)         private String tenantId = null;

        @JsonProperty("applicationNumber")

                private String applicationNumber = null;

        @JsonProperty("applicantAddress")

          @Valid
                private Address applicantAddress = null;


}

```



4. Create the BTRConfiguration class within the configuration package. The MainConfiguration class should already exist inside the config package.

{% code lineNumbers="true" %}
```java
package digit.config;

import com.fasterxml.jackson.databind.ObjectMapper;
import lombok.*;
import org.egov.tracer.config.TracerConfiguration;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Import;
import org.springframework.http.converter.json.MappingJackson2HttpMessageConverter;
import org.springframework.stereotype.Component;

import jakarta.annotation.PostConstruct;
import java.util.TimeZone;

@Component
@Data
@Import({TracerConfiguration.class})
@NoArgsConstructor
@AllArgsConstructor
@Setter
@Getter
public class BTRConfiguration {
    @Value("${app.timezone}")
    private String timeZone;

    @PostConstruct
    public void initialize() {
        TimeZone.setDefault(TimeZone.getTimeZone(timeZone));
    }

    @Bean
    @Autowired
    public MappingJackson2HttpMessageConverter jacksonConverter(ObjectMapper objectMapper) {
        MappingJackson2HttpMessageConverter converter = new MappingJackson2HttpMessageConverter();
        converter.setObjectMapper(objectMapper);
        return converter;
    }

    // User Config
    @Value("${egov.user.host}")
    private String userHost;

    @Value("${egov.user.context.path}")
    private String userContextPath;

    @Value("${egov.user.create.path}")
    private String userCreateEndpoint;

    @Value("${egov.user.search.path}")
    private String userSearchEndpoint;

    @Value("${egov.user.update.path}")
    private String userUpdateEndpoint;

    //Idgen Config
    @Value("${egov.idgen.host}")
    private String idGenHost;

    @Value("${egov.idgen.path}")
    private String idGenPath;

    //Workflow Config
    @Value("${egov.workflow.host}")
    private String wfHost;

    @Value("${egov.workflow.transition.path}")
    private String wfTransitionPath;

    @Value("${egov.workflow.businessservice.search.path}")
    private String wfBusinessServiceSearchPath;

    @Value("${egov.workflow.processinstance.search.path}")
    private String wfProcessInstanceSearchPath;

    @Value("${is.workflow.enabled}")
    private Boolean isWorkflowEnabled;


    // BTR Variables

    @Value("${btr.kafka.create.topic}")
    private String createTopic;

    @Value("${btr.kafka.update.topic}")
    private String updateTopic;

    @Value("${btr.default.offset}")
    private Integer defaultOffset;

    @Value("${btr.default.limit}")
    private Integer defaultLimit;

    @Value("${btr.search.max.limit}")
    private Integer maxLimit;


    //MDMS
    @Value("${egov.mdms.host}")
    private String mdmsHost;

    @Value("${egov.mdms.search.endpoint}")
    private String mdmsEndPoint;

    //HRMS
    @Value("${egov.hrms.host}")
    private String hrmsHost;

    @Value("${egov.hrms.search.endpoint}")
    private String hrmsEndPoint;

    @Value("${egov.url.shortner.host}")
    private String urlShortnerHost;

    @Value("${egov.url.shortner.endpoint}")
    private String urlShortnerEndpoint;

    @Value("${egov.sms.notification.topic}")
    private String smsNotificationTopic;
}

```
{% endcode %}

The core models are imported.
