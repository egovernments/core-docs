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
  <version>2.0.0-SNAPSHOT</version>
</dependency>
<dependency>
  <groupId>org.egov.services</groupId>
  <artifactId>services-common</artifactId>
  <version>1.0.1-SNAPSHOT</version>
</dependency>
<repositories>
  <repository>
    <id>repo.egovernments.org</id>
    <name>eGov ERP Releases Repository</name>
    <url>https://nexus-repo.egovernments.org/nexus/content/repositories/releases/</url>
  </repository>
  <repository>
    <id>repo.egovernments.org.snapshots</id>
    <name>eGov ERP Releases Repository</name>
    <url>https://nexus-repo.egovernments.org/nexus/content/repositories/snapshots/</url>
  </repository>
  <repository>
    <id>repo.egovernments.org.public</id>
    <name>eGov Public Repository Group</name>
    <url>https://nexus-repo.egovernments.org/nexus/content/groups/public/</url>
  </repository>
</repositories>
```
{% endcode %}

These are pre-written libraries which contain tracer support, common models like MDMS, Auth and Auth and the capability to raise custom exceptions.

Once these core models are imported, it is safe to delete the RequestInfo, and ResponseInfo classes from the models folder and use the ones present in the common contract that is imported.

### **Import Core Models**

Before starting development, create/update the following classes as given below.

1. Create RequestInfoWrapper POJO within the Models package -

{% code lineNumbers="true" %}
```java
package digit.web.models;

import com.fasterxml.jackson.annotation.JsonProperty;
import lombok.*;
import org.egov.common.contract.request.RequestInfo;


@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
@Builder
public class RequestInfoWrapper {

    @JsonProperty("RequestInfo")
    private RequestInfo requestInfo;
}

```
{% endcode %}

2. Update the Applicant POJO with the following content -

{% code lineNumbers="true" %}
```java
package digit.web.models;

import java.util.Objects;
import com.fasterxml.jackson.annotation.JsonProperty;
import com.fasterxml.jackson.annotation.JsonCreator;
import digit.web.models.Role;
import digit.web.models.User;
import io.swagger.annotations.ApiModel;
import io.swagger.annotations.ApiModelProperty;
import java.time.LocalDate;
import java.util.ArrayList;
import java.util.List;
import org.springframework.validation.annotation.Validated;
import javax.validation.Valid;
import javax.validation.constraints.*;
import lombok.AllArgsConstructor;
import lombok.Getter;
import lombok.NoArgsConstructor;
import lombok.Setter;
import lombok.Builder;

/**
 * Details of the user applying for birth registration
 */
@ApiModel(description = "Details of the user applying for birth registration")
@Validated
@javax.annotation.Generated(value = "org.egov.codegen.SpringBootCodegen", date = "2022-08-16T15:34:24.436+05:30")

@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
@Builder
public class javaApplicant   {
        @JsonProperty("id")
        private String id = null;

        @JsonProperty("userName")
        private String userName = null;

        @JsonProperty("password")
        private String password = null;

        @JsonProperty("salutation")
        private String salutation = null;

        @JsonProperty("name")
        private String name = null;

        @JsonProperty("gender")
        private String gender = null;

        @JsonProperty("mobileNumber")
        private String mobileNumber = null;

        @JsonProperty("emailId")
        private String emailId = null;

        @JsonProperty("altContactNumber")
        private String altContactNumber = null;

        @JsonProperty("pan")
        private String pan = null;

        @JsonProperty("aadhaarNumber")
        private String aadhaarNumber = null;

        @JsonProperty("permanentAddress")
        private String permanentAddress = null;

        @JsonProperty("permanentCity")
        private String permanentCity = null;

        @JsonProperty("permanentPincode")
        private String permanentPincode = null;

        @JsonProperty("correspondenceCity")
        private String correspondenceCity = null;

        @JsonProperty("correspondencePincode")
        private String correspondencePincode = null;

        @JsonProperty("correspondenceAddress")
        private String correspondenceAddress = null;

        @JsonProperty("active")
        private Boolean active = null;

        @JsonProperty("dob")
        private LocalDate dob = null;

        @JsonProperty("pwdExpiryDate")
        private LocalDate pwdExpiryDate = null;

        @JsonProperty("locale")
        private String locale = null;

        @JsonProperty("type")
        private String type = null;

        @JsonProperty("signature")
        private String signature = null;

        @JsonProperty("accountLocked")
        private Boolean accountLocked = null;

        @JsonProperty("roles")
        @Valid
        private List<Role> roles = null;

        @JsonProperty("fatherOrHusbandName")
        private String fatherOrHusbandName = null;

        @JsonProperty("bloodGroup")
        private String bloodGroup = null;

        @JsonProperty("identificationMark")
        private String identificationMark = null;

        @JsonProperty("photo")
        private String photo = null;

        @JsonProperty("createdBy")
        private Long createdBy = null;

        @JsonProperty("createdDate")
        private LocalDate createdDate = null;

        @JsonProperty("lastModifiedBy")
        private Long lastModifiedBy = null;

        @JsonProperty("lastModifiedDate")
        private LocalDate lastModifiedDate = null;

        @JsonProperty("otpReference")
        private String otpReference = null;

        @JsonProperty("tenantId")
        private String tenantId = null;


        public Applicant addRolesItem(Role rolesItem) {
            if (this.roles == null) {
            this.roles = new ArrayList<>();
            }
        this.roles.add(rolesItem);
        return this;
        }

}
```
{% endcode %}

3. Create the BTRConfiguration class within the configuration package. The MainConfiguration class should already exist inside the config package.

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

import javax.annotation.PostConstruct;
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
