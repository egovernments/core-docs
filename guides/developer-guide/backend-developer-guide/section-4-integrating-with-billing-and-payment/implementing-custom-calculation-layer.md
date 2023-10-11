---
description: Calculating costs for a service and raising demand for bill generation
---

# Implementing Custom Calculation Layer

## **Calculation**&#x20;

The calculation class will contain the calculation logic for given service delivery.  This is very domain specific and cannot be generalised. Based on the application submitted, the calculator class will calculate the tax/charges and call billing service to generate the demand.&#x20;

For our guide, we are going to create a sample calculation class with some dummy logic. Demand generation,  billing and payment will be covered in the future. For this, we are going to perform the following steps -

i) Create a class under `service` folder by the name of `CalculationService`

ii) Now, annotate this class with @Service annotation and add the following logic within it -

```java
package digit.service;

import com.fasterxml.jackson.databind.ObjectMapper;
import digit.config.BTRConfiguration;
import digit.repository.ServiceRequestRepository;
import digit.web.models.*;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.ArrayList;
import java.util.List;

@Service
public class CalculationService {

    @Autowired
    private BTRConfiguration btrConfiguration;

    @Autowired
    private ObjectMapper mapper;

    @Autowired
    private ServiceRequestRepository serviceRequestRepository;

    public CalculationRes getCalculation(BirthRegistrationRequest request){

        List<CalculationCriteria> calculationCriteriaList = new ArrayList<>();
        for(BirthRegistrationApplication application : request.getBirthRegistrationApplications()) {
            CalculationCriteria calculationCriteria = CalculationCriteria.builder()
                    .birthregistrationapplication(application)
                    .tenantId(application.getTenantId())
                    .applicationNumber(application.getApplicationNumber())
                    .build();
            calculationCriteriaList.add(calculationCriteria);
        }

        CalculationReq calculationReq = CalculationReq.builder()
                .requestInfo(request.getRequestInfo())
                .calculationCriteria(calculationCriteriaList)
                .build();

        StringBuilder url = new StringBuilder().append(btrConfiguration.getBtrCalculatorHost())
                .append(btrConfiguration.getBtrCalculatorCalculateEndpoint());

        Object response = serviceRequestRepository.fetchResult(url, calculationReq);
        CalculationRes calculationRes = mapper.convertValue(response, CalculationRes.class);

        return calculationRes;
    }
}

```
