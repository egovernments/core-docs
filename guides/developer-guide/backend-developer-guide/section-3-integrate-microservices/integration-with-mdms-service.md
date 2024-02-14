# Integration with MDMS Service

## **Overview**

We will call into MDMS deployed in the sandbox environment. All MDMS config data needs to be uploaded into the MDMS repository (DEV branch if you are deploying/testing in your dev environment).&#x20;

## Steps

Integration with MDMS requires the following steps to be followed:

1. Add a new MDMS file in MDMS repo. For this guide, a sample MDMS file has already been added [available here](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/DIGIT-DEVELOPER-TUTORIAL/BtrCharges.json). Copy this file into your repository.&#x20;
2. Restart MDMS service after adding the new file via Jenkins build UI.&#x20;
3. Once restarted, hit the curl mentioned below to verify that the new file has been properly added .

```bash
curl --location --request POST 'https://yourserver.digit.org/egov-mdms-service/v1/_search' \
--header 'Content-Type: application/json' \
--data-raw '{
    "RequestInfo": {
        "apiId": "asset-services",
        "ver": null,
        "ts": null,
        "action": null,
        "did": null,
        "key": null,
        "msgId": "search with from and to values",
        "authToken": "{{devAuth}}"
    },
    "MdmsCriteria": {
        "tenantId": "pb",
        "moduleDetails": [
            {
                "moduleName": "BTR",
                "masterDetails": [
                    {
                        "name": "RegistrationCharges"
                    }
                ]
            }
        ]
    }
}' 
```

4. Call the MDMS service post verification from within our application and fetch the required master data. For this, create a Java class by the name of MdmsUtil under utils folder. Annotate this class with @Component and put the following content in the class -

```java
package digit.utils;

import com.jayway.jsonpath.JsonPath;
import org.egov.common.contract.request.RequestInfo;
import org.egov.mdms.model.MasterDetail;
import org.egov.mdms.model.MdmsCriteria;
import org.egov.mdms.model.MdmsCriteriaReq;
import org.egov.mdms.model.ModuleDetail;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;
import org.springframework.web.client.RestTemplate;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;


@Component
public class MdmsUtil {
    @Autowired
    private RestTemplate restTemplate;

    @Value("${egov.mdms.host}")
    private String mdmsHost;

    @Value("${egov.mdms.search.endpoint}")
    private String mdmsUrl;


    public Integer fetchRegistrationChargesFromMdms(RequestInfo requestInfo, String tenantId) {
        StringBuilder uri = new StringBuilder();
        uri.append(mdmsHost).append(mdmsUrl);
        MdmsCriteriaReq mdmsCriteriaReq = getMdmsRequestForCategoryList(requestInfo, tenantId);
        Object response = new HashMap<>();
        Integer rate = 0;
        try {
            response = restTemplate.postForObject(uri.toString(), mdmsCriteriaReq, Map.class);
            rate = JsonPath.read(response, "$.MdmsRes.BTR.RegistrationCharges.[0].amount");
        }catch(Exception e) {
            return  null;
        }
        return rate;
    }

    private MdmsCriteriaReq getMdmsRequestForCategoryList(RequestInfo requestInfo, String tenantId) {
        MasterDetail masterDetail = new MasterDetail();
        masterDetail.setName("RegistrationCharges");
        List<MasterDetail> masterDetailList = new ArrayList<>();
        masterDetailList.add(masterDetail);

        ModuleDetail moduleDetail = new ModuleDetail();
        moduleDetail.setMasterDetails(masterDetailList);
        moduleDetail.setModuleName("BTR");
        List<ModuleDetail> moduleDetailList = new ArrayList<>();
        moduleDetailList.add(moduleDetail);

        MdmsCriteria mdmsCriteria = new MdmsCriteria();
        mdmsCriteria.setTenantId(tenantId.split("\\.")[0]);
        mdmsCriteria.setModuleDetails(moduleDetailList);

        MdmsCriteriaReq mdmsCriteriaReq = new MdmsCriteriaReq();
        mdmsCriteriaReq.setMdmsCriteria(mdmsCriteria);
        mdmsCriteriaReq.setRequestInfo(requestInfo);

        return mdmsCriteriaReq;
    }
}


```

5. Add the following properties in application.properties file -

```properties
#mdms urls
egov.mdms.host=https://dev.digit.org # REPLACE with your environment name
egov.mdms.search.endpoint=/egov-mdms-service/v1/_search
```
