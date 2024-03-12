---
description: Integration with other DIGIT services
---

# Section 3: Integrate Microservices

## Overview

A separate class should be created for integrating with each dependent microservice. Only one method from that class should be called from the main service class for integration.

This guide showcases the steps to integrate our microservices with other microservices like

1. [IdGen Service](integrate-idgen-service.md)
2. [User Service](integrate-user-service.md)
3. [MDMS Service](integrate-mdms-service.md)
4. [Workflow Service](integrate-workflow-service.md)
5. [URL Shortening Service](integrate-url-shortener-service.md)

## Common Resources

For interacting with other microservices, we can create and implement the following `ServiceRequestRepository` class under `repository` package -

```java
package digit.repository;


import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.SerializationFeature;
import lombok.extern.slf4j.Slf4j;
import org.egov.tracer.model.ServiceCallException;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Repository;
import org.springframework.web.client.HttpClientErrorException;
import org.springframework.web.client.RestTemplate;

import java.util.Map;


@Repository
@Slf4j
public class ServiceRequestRepository {

    private ObjectMapper mapper;

    private RestTemplate restTemplate;


    @Autowired
    public ServiceRequestRepository(ObjectMapper mapper, RestTemplate restTemplate) {
        this.mapper = mapper;
        this.restTemplate = restTemplate;
    }


    public Object fetchResult(StringBuilder uri, Object request) {
        mapper.configure(SerializationFeature.FAIL_ON_EMPTY_BEANS, false);
        Object response = null;
        try {
            response = restTemplate.postForObject(uri.toString(), request, Map.class);
        }catch(HttpClientErrorException e) {
            log.error("External Service threw an Exception: ",e);
            throw new ServiceCallException(e.getResponseBodyAsString());
        }catch(Exception e) {
            log.error("Exception while fetching from searcher: ",e);
        }

        return response;
    }
}
```

