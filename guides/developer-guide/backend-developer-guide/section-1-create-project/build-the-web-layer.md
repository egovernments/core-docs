---
description: Implementing the controller layer in Spring
---

# Build The Web Layer

## **Overview**

The web/controller layer handles all the incoming REST requests to a service.

## **Process Flow**

The @RequestMapping("/v1") annotation is added on top of the controller class. This contains the version of the API (this becomes a part of the API endpoint URL).

#### **Steps to setup the request handler in the controller layer**

Follow the steps below to set up the request handler in the controller layer.

1. Make a call to the method in the Service layer and get the response back from it.
2. Build the responseInfo.
3. Build the final response to be returned to the client.

![Sample request handler in controller layer](<../../../../.gitbook/assets/image (62).png>)

For this guide, the controller class will contain the following content -

{% code lineNumbers="true" %}
```java
package digit.web.controllers;

import com.fasterxml.jackson.databind.ObjectMapper;
import digit.service.BirthRegistrationService;
import digit.utils.ResponseInfoFactory;
import digit.web.models.*;
import io.swagger.annotations.ApiParam;
import io.swagger.annotations.Tag;
import lombok.ToString;
import lombok.extern.slf4j.Slf4j;
import org.egov.common.contract.response.ResponseInfo;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;

import javax.servlet.http.HttpServletRequest;
import javax.validation.Valid;
import java.util.Collections;
import java.util.List;
@javax.annotation.Generated(value = "org.egov.codegen.SpringBootCodegen", date = "2022-07-26T12:39:05.988+05:30")
@Slf4j
@ToString
@Controller
@RequestMapping("/birth-services")
public class V1ApiController{

    private final ObjectMapper objectMapper;

    private final HttpServletRequest request;

    private BirthRegistrationService birthRegistrationService;

    @Autowired
    private ResponseInfoFactory responseInfoFactory;

    @Autowired
    public V1ApiController(ObjectMapper objectMapper, HttpServletRequest request, BirthRegistrationService birthRegistrationService) {
        this.objectMapper = objectMapper;
        this.request = request;
        this.birthRegistrationService = birthRegistrationService;
    }

    @RequestMapping(value="/v1/registration/_create", method = RequestMethod.POST)
    public ResponseEntity<BirthRegistrationResponse> v1RegistrationCreatePost(@ApiParam(value = "Details for the new Birth Registration Application(s) + RequestInfo meta data." ,required=true )  @Valid @RequestBody BirthRegistrationRequest birthRegistrationRequest) {
        List<BirthRegistrationApplication> applications = birthRegistrationService.registerBtRequest(birthRegistrationRequest);
        ResponseInfo responseInfo = responseInfoFactory.createResponseInfoFromRequestInfo(birthRegistrationRequest.getRequestInfo(), true);
        BirthRegistrationResponse response = BirthRegistrationResponse.builder().birthRegistrationApplications(applications).responseInfo(responseInfo).build();
        return new ResponseEntity<>(response, HttpStatus.OK);
    }

    @RequestMapping(value="/v1/registration/_search", method = RequestMethod.POST)
    public ResponseEntity<BirthRegistrationResponse> v1RegistrationSearchPost(@RequestBody RequestInfoWrapper requestInfoWrapper, @Valid @ModelAttribute BirthApplicationSearchCriteria birthApplicationSearchCriteria) {
        List<BirthRegistrationApplication> applications = birthRegistrationService.searchBtApplications(requestInfoWrapper.getRequestInfo(), birthApplicationSearchCriteria);
        ResponseInfo responseInfo = responseInfoFactory.createResponseInfoFromRequestInfo(requestInfoWrapper.getRequestInfo(), true);
        BirthRegistrationResponse response = BirthRegistrationResponse.builder().birthRegistrationApplications(applications).responseInfo(responseInfo).build();
        return new ResponseEntity<>(response,HttpStatus.OK);
    }

    @RequestMapping(value="/v1/registration/_update", method = RequestMethod.POST)
    public ResponseEntity<BirthRegistrationResponse> v1RegistrationUpdatePost(@ApiParam(value = "Details for the new (s) + RequestInfo meta data." ,required=true )  @Valid @RequestBody BirthRegistrationRequest birthRegistrationRequest) {
        BirthRegistrationApplication application = birthRegistrationService.updateBtApplication(birthRegistrationRequest);

        ResponseInfo responseInfo = responseInfoFactory.createResponseInfoFromRequestInfo(birthRegistrationRequest.getRequestInfo(), true);
        BirthRegistrationResponse response = BirthRegistrationResponse.builder().birthRegistrationApplications(Collections.singletonList(application)).responseInfo(responseInfo).build();
        return new ResponseEntity<>(response, HttpStatus.OK);
    }

}

```
{% endcode %}

{% hint style="info" %}
**NOTE:** At this point, your IDE must be showing a lot of errors but do not worry we will add all dependent layers as we progress through this guide and the errors will go away.
{% endhint %}

4. Since the Codegen jar creates the search API with search parameters annotated with @RequestParam rather than taking request parameters as a POJO. For this, we will create a POJO by the name of BirthApplicationSearchCriteria within the Models package. Insert the following content in the POJO.

{% code lineNumbers="true" %}
```java
package digit.web.models;

import com.fasterxml.jackson.annotation.JsonProperty;
import lombok.*;

import java.util.List;

@Data
@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
@Builder
@ToString
public class BirthApplicationSearchCriteria {

    @JsonProperty("tenantId")
    private String tenantId;

    @JsonProperty("status")
    private String status;

    @JsonProperty("ids")
    private List<String> ids;

    @JsonProperty("applicationNumber")
    private String applicationNumber;

}
```
{% endcode %}

The web layer is now setup.
