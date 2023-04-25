---
description: Calculating costs for a service and raising demand for bill generation
---

# Implementing custom calculation layer

#### **Calculation**&#x20;

The calculation class will contain the calculation logic for given service delivery.  This is very domain specific and cannot be generalised. Based on the application submitted, the calculator class will calculate the tax/charges and call billing service to generate demand.&#x20;

For our guide, we are going to create a sample calculation class with some dummy logic. Demand generation,  billing and payment will be covered in the future. For this, we are going to perform the following steps -

i) Create a class under `service` folder by the name of `CalculationService`

ii) Now, annotate this class with @Service annotation and add the following logic within it -

```java
package digit.service;

import digit.web.models.BirthRegistrationApplication;
import org.springframework.stereotype.Service;

@Service
public class CalculationService {
    public Double calculateLaminationCharges(BirthRegistrationApplication application){
        // Add calculation logic according to business requirement
        return 10.0;
    }
}

```

_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
