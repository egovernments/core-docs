# Create Validation & Enrichment Layers

### Validation Layer

All business validation logic should be added to this class. For example, verifying the values against the master data, ensuring non-duplication of data etc.

**Steps:** Follow the steps below to create the validation layer.

a. Create a package called validators. This ensures the validation logic is separate so that the code is easy to navigate through and readable.

b. Create a class by the name of BirthApplicationValidator

c. Annotate the class with @Component annotation and insert the following content in the class -

```java
package digit.validators;

import digit.repository.BirthRegistrationRepository;
import digit.web.models.BirthApplicationSearchCriteria;
import digit.web.models.BirthRegistrationApplication;
import digit.web.models.BirthRegistrationRequest;
import org.egov.tracer.model.CustomException;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;
import org.springframework.util.ObjectUtils;

@Component
public class BirthApplicationValidator {

    @Autowired
    private BirthRegistrationRepository repository;

    public void validateBirthApplication(BirthRegistrationRequest birthRegistrationRequest) {
        birthRegistrationRequest.getBirthRegistrationApplications().forEach(application -> {
            if(ObjectUtils.isEmpty(application.getTenantId()))
                throw new CustomException("EG_BT_APP_ERR", "tenantId is mandatory for creating birth registration applications");
        });
    }

    public BirthRegistrationApplication validateApplicationExistence(BirthRegistrationApplication birthRegistrationApplication) {
        return repository.getApplications(BirthApplicationSearchCriteria.builder().applicationNumber(birthRegistrationApplication.getApplicationNumber()).build()).get(0);
    }
}
```

{% hint style="info" %}
**NOTE:** For the sake of simplicity the above**-**mentioned validations are implemented. Required validations will vary on a case-to-case basis.
{% endhint %}

### **Enrichment Layer**

This layer enriches the request. System-generated values like id, auditDetails etc. are generated and added to the request. In the case of this module, since the applicant is the parent of a baby and a child cannot be a user of the system directly, both the parents' details are captured in the User table. The user ids of the parents are then enriched in the application.&#x20;

**Steps:** Follow the steps below to create the enrichment layer.

a. Create a package under DIGIT by the name of enrichment. This ensures the enrichment code is separate from business logic so that the codebase is easy to navigate through and readable.

b. Create a class by the name of BirthApplicationEnrichment

c. Annotate the class with @Component and add the following methods to the class -

```java
package digit.enrichment;

import digit.service.UserService;
import digit.utils.IdgenUtil;
import digit.utils.UserUtil;
import digit.web.models.*;
import lombok.extern.slf4j.Slf4j;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

import java.util.List;
import java.util.UUID;
@Component
@Slf4j
public class BirthApplicationEnrichment {

    @Autowired
    private IdgenUtil idgenUtil;

    @Autowired
    private UserService userService;

    @Autowired
    private UserUtil userUtils;

    public void enrichBirthApplication(BirthRegistrationRequest birthRegistrationRequest) {
        List<String> birthRegistrationIdList = idgenUtil.getIdList(birthRegistrationRequest.getRequestInfo(), birthRegistrationRequest.getBirthRegistrationApplications().get(0).getTenantId(), "btr.registrationid", "", birthRegistrationRequest.getBirthRegistrationApplications().size());
        Integer index = 0;
        for(BirthRegistrationApplication application : birthRegistrationRequest.getBirthRegistrationApplications()){
            // Enrich audit details
            AuditDetails auditDetails = AuditDetails.builder().createdBy(birthRegistrationRequest.getRequestInfo().getUserInfo().getUuid()).createdTime(System.currentTimeMillis()).lastModifiedBy(birthRegistrationRequest.getRequestInfo().getUserInfo().getUuid()).lastModifiedTime(System.currentTimeMillis()).build();
            application.setAuditDetails(auditDetails);

            // Enrich UUID
            application.setId(UUID.randomUUID().toString());

//            application.getFather().setId(application.getId());
//            application.getMother().setId(application.getId());

            // Enrich registration Id
            application.getAddress().setRegistrationId(application.getId());

            // Enrich address UUID
            application.getAddress().setId(UUID.randomUUID().toString());

            //Enrich application number from IDgen
            application.setApplicationNumber(birthRegistrationIdList.get(index++));

        }
    }

    public void enrichBirthApplicationUponUpdate(BirthRegistrationRequest birthRegistrationRequest) {
        // Enrich lastModifiedTime and lastModifiedBy in case of update
        birthRegistrationRequest.getBirthRegistrationApplications().get(0).getAuditDetails().setLastModifiedTime(System.currentTimeMillis());
        birthRegistrationRequest.getBirthRegistrationApplications().get(0).getAuditDetails().setLastModifiedBy(birthRegistrationRequest.getRequestInfo().getUserInfo().getUuid());
    }

    public void enrichFatherApplicantOnSearch(BirthRegistrationApplication application) {
        UserDetailResponse fatherUserResponse = userService.searchUser(userUtils.getStateLevelTenant(application.getTenantId()),application.getFather().getId(),null);
        User fatherUser = fatherUserResponse.getUser().get(0);
        log.info(fatherUser.toString());
        FatherApplicant fatherApplicant = FatherApplicant.builder().aadhaarNumber(fatherUser.getAadhaarNumber())
                                                                    .accountLocked(fatherUser.getAccountLocked())
                                                                    .active(fatherUser.getActive())
                                                                    .altContactNumber(fatherUser.getAltContactNumber())
                                                                    .bloodGroup(fatherUser.getBloodGroup())
                                                                    .correspondenceAddress(fatherUser.getCorrespondenceAddress())
                                                                    .correspondenceCity(fatherUser.getCorrespondenceCity())
                                                                    .correspondencePincode(fatherUser.getCorrespondencePincode())
                                                                    .gender(fatherUser.getGender())
                                                                    .id(fatherUser.getUuid())
                                                                    .name(fatherUser.getName())
                                                                    .type(fatherUser.getType())
                                                                    .roles(fatherUser.getRoles()).build();
        application.setFather(fatherApplicant);
    }

    public void enrichMotherApplicantOnSearch(BirthRegistrationApplication application) {
        UserDetailResponse motherUserResponse = userService.searchUser(userUtils.getStateLevelTenant(application.getTenantId()),application.getFather().getId(),null);
        User motherUser = motherUserResponse.getUser().get(0);
        log.info(motherUser.toString());
        MotherApplicant motherApplicant = MotherApplicant.builder().aadhaarNumber(motherUser.getAadhaarNumber())
                .accountLocked(motherUser.getAccountLocked())
                .active(motherUser.getActive())
                .altContactNumber(motherUser.getAltContactNumber())
                .bloodGroup(motherUser.getBloodGroup())
                .correspondenceAddress(motherUser.getCorrespondenceAddress())
                .correspondenceCity(motherUser.getCorrespondenceCity())
                .correspondencePincode(motherUser.getCorrespondencePincode())
                .gender(motherUser.getGender())
                .id(motherUser.getUuid())
                .name(motherUser.getName())
                .type(motherUser.getType())
                .roles(motherUser.getRoles()).build();
        application.setMother(motherApplicant);
    }
}
```

{% hint style="info" %}
**NOTE:** For the sake of simplicity the above-mentioned enrichment methods are implemented. Required enrichment will vary on a case-to-case basis.
{% endhint %}



