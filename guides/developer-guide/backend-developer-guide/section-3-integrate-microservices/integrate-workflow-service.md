# Integrate Workflow Service

## **Overview**

The birth registration module follows a simple workflow derived from the swimlane diagrams. Please check the [design inputs](../section-0-prep/design-inputs/high-level-design.md#process-workflow-diagram) section for correlation as well as the [design guide](../../../design-guide/design-services.md#extract-the-workflow) for info on how the workflow configuration is derived.&#x20;

## Steps

Integration with workflow service requires the following steps -

1. Create Workflow service - Create a class to transition the workflow object across its states. For this, create a class by the name of WorkflowService.java under the service directory and annotate it with @Service annotation.&#x20;
2. Add the below content to this class -

```java
package digit.service;

import com.fasterxml.jackson.databind.ObjectMapper;
import digit.config.BTRConfiguration;
import digit.repository.ServiceRequestRepository;
import digit.web.models.*;
import lombok.extern.slf4j.Slf4j;
import org.egov.common.contract.models.Workflow;
import org.egov.common.contract.request.RequestInfo;
import org.egov.common.contract.models.RequestInfoWrapper;
import org.egov.common.contract.request.User;
import org.egov.common.contract.workflow.*;
import org.egov.tracer.model.CustomException;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;
import org.springframework.util.CollectionUtils;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.List;

@Component
@Slf4j
public class WorkflowService {

    @Autowired
    private ObjectMapper mapper;

    @Autowired
    private ServiceRequestRepository repository;

    @Autowired
    private BTRConfiguration config;

    public void updateWorkflowStatus(BirthRegistrationRequest birthRegistrationRequest) {
        birthRegistrationRequest.getBirthRegistrationApplications().forEach(application -> {
            ProcessInstance processInstance = getProcessInstanceForBTR(application, birthRegistrationRequest.getRequestInfo());
            ProcessInstanceRequest workflowRequest = new ProcessInstanceRequest(birthRegistrationRequest.getRequestInfo(), Collections.singletonList(processInstance));
            callWorkFlow(workflowRequest);
        });
    }

    public State callWorkFlow(ProcessInstanceRequest workflowReq) {

        ProcessInstanceResponse response = null;
        StringBuilder url = new StringBuilder(config.getWfHost().concat(config.getWfTransitionPath()));
        Object optional = repository.fetchResult(url, workflowReq);
        response = mapper.convertValue(optional, ProcessInstanceResponse.class);
        return response.getProcessInstances().get(0).getState();
    }

    private ProcessInstance getProcessInstanceForBTR(BirthRegistrationApplication application, RequestInfo requestInfo) {
        Workflow workflow = application.getWorkflow();

        ProcessInstance processInstance = new ProcessInstance();
        processInstance.setBusinessId(application.getApplicationNumber());
        processInstance.setAction(workflow.getAction());
        processInstance.setModuleName("birth-services");
        processInstance.setTenantId(application.getTenantId());
        processInstance.setBusinessService("BTR");
        processInstance.setDocuments(workflow.getDocuments());
        processInstance.setComment(workflow.getComments());

        if(!CollectionUtils.isEmpty(workflow.getAssignes())){
            List<User> users = new ArrayList<>();

            workflow.getAssignes().forEach(uuid -> {
                User user = new User();
                user.setUuid(uuid);
                users.add(user);
            });

            processInstance.setAssignes(users);
        }

        return processInstance;

    }

    public ProcessInstance getCurrentWorkflow(RequestInfo requestInfo, String tenantId, String businessId) {

        RequestInfoWrapper requestInfoWrapper = RequestInfoWrapper.builder().requestInfo(requestInfo).build();

        StringBuilder url = getSearchURLWithParams(tenantId, businessId);

        Object res = repository.fetchResult(url, requestInfoWrapper);
        ProcessInstanceResponse response = null;

        try{
            response = mapper.convertValue(res, ProcessInstanceResponse.class);
        }
        catch (Exception e){
            throw new CustomException("PARSING_ERROR","Failed to parse workflow search response");
        }

        if(response!=null && !CollectionUtils.isEmpty(response.getProcessInstances()) && response.getProcessInstances().get(0)!=null)
            return response.getProcessInstances().get(0);

        return null;
    }

    private BusinessService getBusinessService(BirthRegistrationApplication application, RequestInfo requestInfo) {
        String tenantId = application.getTenantId();
        StringBuilder url = getSearchURLWithParams(tenantId, "BTR");
        RequestInfoWrapper requestInfoWrapper = RequestInfoWrapper.builder().requestInfo(requestInfo).build();
        Object result = repository.fetchResult(url, requestInfoWrapper);
        BusinessServiceResponse response = null;
        try {
            response = mapper.convertValue(result, BusinessServiceResponse.class);
        } catch (IllegalArgumentException e) {
            throw new CustomException("PARSING ERROR", "Failed to parse response of workflow business service search");
        }

        if (CollectionUtils.isEmpty(response.getBusinessServices()))
            throw new CustomException("BUSINESSSERVICE_NOT_FOUND", "The businessService " + "BTR" + " is not found");

        return response.getBusinessServices().get(0);
    }

    private StringBuilder getSearchURLWithParams(String tenantId, String businessService) {

        StringBuilder url = new StringBuilder(config.getWfHost());
        url.append(config.getWfBusinessServiceSearchPath());
        url.append("?tenantId=");
        url.append(tenantId);
        url.append("&businessServices=");
        url.append(businessService);
        return url;
    }

    public ProcessInstanceRequest getProcessInstanceForBirthRegistrationPayment(BirthRegistrationRequest updateRequest) {

        BirthRegistrationApplication application = updateRequest.getBirthRegistrationApplications().get(0);

        ProcessInstance process = ProcessInstance.builder()
                .businessService("BTR")
                .businessId(application.getApplicationNumber())
                .comment("Payment for birth registration processed")
                .moduleName("birth-services")
                .tenantId(application.getTenantId())
                .action("PAY")
                .build();

        return ProcessInstanceRequest.builder()
                .requestInfo(updateRequest.getRequestInfo())
                .processInstances(Arrays.asList(process))
                .build();

    }
}
```

5. Add workflow to BirthRegistrationService.
6. Add the below field to BirthRegistrationService.java

```java
 @Autowired
 private WorkflowService workflowService;
```

6. Transition the workflow - Modify the following methods in BirthRegistrationService.java as follows. Note that we are adding calls into the workflow service in each of these methods.

<details>

<summary>registerBtRequest</summary>

```java
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
```



</details>

<details>

<summary>updateBtApplication</summary>

```java
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
```



</details>

<details>

<summary>searchBtApplications</summary>

```java
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
```



</details>

7. Configure application.properties - Add the following properties to application.properties file of the birth registration module. Depending on whether you are port forwarding or using the service directly on the host, please update the host name.

```properties
#Workflow config
is.workflow.enabled=true
egov.workflow.host=http://localhost:8282
egov.workflow.transition.path=/egov-workflow-v2/egov-wf/process/_transition
egov.workflow.businessservice.search.path=/egov-workflow-v2/egov-wf/businessservice/_search
egov.workflow.processinstance.search.path=/egov-workflow-v2/egov-wf/process/_search
```

8. Run the workflow service locally - the application will call into it to create the necessary tables in the DB and effect the workflow transitions.&#x20;
