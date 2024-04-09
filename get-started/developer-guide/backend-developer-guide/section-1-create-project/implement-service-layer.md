# Implement Service Layer

## **Overview**

The service layer performs business logic on the RequestData and prepares the Response to be returned back to the client.

## **Steps**

Follow the steps below to create the service layer.

1. Create a new package called Service.
2. Create a new class in this folder by the name BirthRegistrationService.
3. Annotate the class with @Service annotation.
4.  Add the following content to the class -

    ```java
    package digit.service;


    import digit.enrichment.BirthApplicationEnrichment;
    import digit.kafka.Producer;
    import digit.repository.BirthRegistrationRepository;
    import digit.validators.BirthApplicationValidator;
    import digit.web.models.BirthApplicationSearchCriteria;
    import digit.web.models.BirthRegistrationApplication;
    import digit.web.models.BirthRegistrationRequest;
    import lombok.extern.slf4j.Slf4j;
    import org.egov.common.contract.request.RequestInfo;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.stereotype.Service;
    import org.springframework.util.CollectionUtils;

    import java.util.ArrayList;
    import java.util.Collections;
    import java.util.List;

    @Service
    @Slf4j
    public class BirthRegistrationService {

        @Autowired
        private BirthApplicationValidator validator;

        @Autowired
        private BirthApplicationEnrichment enrichmentUtil;

        @Autowired
        private UserService userService;

        @Autowired
        private WorkflowService workflowService;

        @Autowired
        private BirthRegistrationRepository birthRegistrationRepository;

        @Autowired
        private Producer producer;

        public List<BirthRegistrationApplication> registerBtRequest(BirthRegistrationRequest birthRegistrationRequest) {
            // Validate applications
            validator.validateBirthApplication(birthRegistrationRequest);

            // Enrich applications
            enrichmentUtil.enrichBirthApplication(birthRegistrationRequest);

    //         Enrich/Upsert user in upon birth registration
            userService.callUserService(birthRegistrationRequest);
    //
            // Initiate workflow for the new application
            workflowService.updateWorkflowStatus(birthRegistrationRequest);

            // Push the application to the topic for persister to listen and persist
            producer.push("save-bt-application", birthRegistrationRequest);

            // Return the response back to user
            return birthRegistrationRequest.getBirthRegistrationApplications();
        }

        public List<BirthRegistrationApplication> searchBtApplications(RequestInfo requestInfo, BirthApplicationSearchCriteria birthApplicationSearchCriteria) {
            // Fetch applications from database according to the given search criteria
            List<BirthRegistrationApplication> applications = birthRegistrationRepository.getApplications(birthApplicationSearchCriteria);

            // If no applications are found matching the given criteria, return an empty list
            if(CollectionUtils.isEmpty(applications))
                return new ArrayList<>();

            // Enrich mother and father of applicant objects
            applications.forEach(application -> {
                enrichmentUtil.enrichFatherApplicantOnSearch(application);
                enrichmentUtil.enrichMotherApplicantOnSearch(application);
            });

            // Otherwise return the found applications
            return applications;
        }

        public BirthRegistrationApplication updateBtApplication(BirthRegistrationRequest birthRegistrationRequest) {
            // Validate whether the application that is being requested for update indeed exists
            BirthRegistrationApplication existingApplication = validator.validateApplicationExistence(birthRegistrationRequest.getBirthRegistrationApplications().get(0));
            existingApplication.setWorkflow(birthRegistrationRequest.getBirthRegistrationApplications().get(0).getWorkflow());
            log.info(existingApplication.toString());
            birthRegistrationRequest.setBirthRegistrationApplications(Collections.singletonList(existingApplication));

            // Enrich application upon update
            enrichmentUtil.enrichBirthApplicationUponUpdate(birthRegistrationRequest);

            workflowService.updateWorkflowStatus(birthRegistrationRequest);

            // Just like create request, update request will be handled asynchronously by the persister
            producer.push("update-bt-application", birthRegistrationRequest);

            return birthRegistrationRequest.getBirthRegistrationApplications().get(0);
        }
    }
    ```

```java
```

{% hint style="info" %}
**NOTE:** At this point, your IDE must be showing a lot of errors but do not worry we will add all dependent layers as we progress through this guide and the errors will go away.
{% endhint %}

