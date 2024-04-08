---
description: Implementing the controller layer in Spring
---

# Build The Web Layer

## **Overview**

The web/controller layer handles all the incoming REST requests to a service.

### **Setup Request Handler In The Controller Layer**

Follow the steps below to set up the request handler in the controller layer.

1. Make a call to the method in the Service Layer and get the response back from it.
2. Build the responseInfo.
3. Build the final response to be returned to the client.

![Sample request handler in controller layer](<../../../../.gitbook/assets/image (122).png>)

The controller class reflects the below content -

{% code lineNumbers="true" %}
```java
package digit.web.controllers;


import digit.service.BirthRegistrationService;
import digit.util.ResponseInfoFactory;
import digit.web.models.*;
import com.fasterxml.jackson.databind.ObjectMapper;
import io.swagger.annotations.ApiParam;
import io.swagger.v3.oas.annotations.Parameter;
import io.swagger.v3.oas.annotations.enums.ParameterIn;
import io.swagger.v3.oas.annotations.media.Schema;
import org.egov.common.contract.response.ResponseInfo;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RequestMapping;
import java.io.IOException;
import java.util.Collections;
import java.util.List;

import jakarta.validation.Valid;
import jakarta.servlet.http.HttpServletRequest;


@jakarta.annotation.Generated(value = "org.egov.codegen.SpringBootCodegen", date = "2024-03-07T11:10:12.732364039+05:30[Asia/Kolkata]")
@Controller
    @RequestMapping("")
    public class BirthApiController{

    private final ObjectMapper objectMapper;

    private final HttpServletRequest request;

    private BirthRegistrationService birthRegistrationService;

    @Autowired
    private ResponseInfoFactory responseInfoFactory;

    @Autowired
    public BirthApiController(ObjectMapper objectMapper, HttpServletRequest request, BirthRegistrationService birthRegistrationService) {
        this.objectMapper = objectMapper;
        this.request = request;
        this.birthRegistrationService = birthRegistrationService;
    }

    @RequestMapping(value="/registration/v1/_create", method = RequestMethod.POST)
    public ResponseEntity<BirthRegistrationResponse> v1RegistrationCreatePost(@ApiParam(value = "Details for the new Birth Registration Application(s) + RequestInfo meta data." ,required=true )  @Valid @RequestBody BirthRegistrationRequest birthRegistrationRequest) {
        List<BirthRegistrationApplication> applications = birthRegistrationService.registerBtRequest(birthRegistrationRequest);
        ResponseInfo responseInfo = responseInfoFactory.createResponseInfoFromRequestInfo(birthRegistrationRequest.getRequestInfo(), true);
        BirthRegistrationResponse response = BirthRegistrationResponse.builder().birthRegistrationApplications(applications).responseInfo(responseInfo).build();
        return new ResponseEntity<>(response, HttpStatus.OK);
    }

    @RequestMapping(value="/v1/registration/_search", method = RequestMethod.POST)
    public ResponseEntity<BirthRegistrationResponse> v1RegistrationSearchPost(@ApiParam(value = "Details for the new Birth Registration Application(s) + RequestInfo meta data." ,required=true )  @Valid @RequestBody BirthApplicationSearchRequest birthApplicationSearchRequest) {
        List<BirthRegistrationApplication> applications = birthRegistrationService.searchBtApplications(birthApplicationSearchRequest.getRequestInfo(), birthApplicationSearchRequest.getBirthApplicationSearchCriteria());
        ResponseInfo responseInfo = responseInfoFactory.createResponseInfoFromRequestInfo(birthApplicationSearchRequest.getRequestInfo(), true);
        BirthRegistrationResponse response = BirthRegistrationResponse.builder().birthRegistrationApplications(applications).responseInfo(responseInfo).build();
        return new ResponseEntity<>(response,HttpStatus.OK);
    }

    @RequestMapping(value="/registration/v1/_update", method = RequestMethod.POST)
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

The web layer is now setup.
