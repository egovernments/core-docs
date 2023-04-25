# Integration with Workflow Service

#### **Integration with workflow**

The birth registration module follows a simple workflow derived from the swimlane diagrams. Please check the [design inputs](../section-0-prep/design-inputs/high-level-design.md#process-workflow-diagram) section for correlation as well as the [design guide](../../../design-guide/design-services.md#extract-the-workflow) for info on how the workflow configuration is derived.&#x20;

Integration with workflow service requires the following steps -

i) Add a workflow object to BirthRegistrationApplication POJO (this may already exist. Do not add if it exists already).&#x20;

```java
@Valid
@JsonProperty("workflow")
private Workflow workflow = null; 
```

#### Create POJOs to support workflow

Create the following POJOs under the `digit.web.models` package.

<details>

<summary>ProcessInstance.java</summary>

```java
package digit.web.models;

import com.fasterxml.jackson.annotation.JsonProperty;
import lombok.*;

import javax.validation.Valid;
import javax.validation.constraints.NotNull;
import javax.validation.constraints.Size;
import java.util.ArrayList;
import java.util.List;

@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
@Builder
@EqualsAndHashCode(of = { "id" })
@ToString
public class ProcessInstance {

    @Size(max = 64)
    @JsonProperty("id")
    private String id;

    @NotNull
    @Size(max = 128)
    @JsonProperty("tenantId")
    private String tenantId;

    @NotNull
    @Size(max = 128)
    @JsonProperty("businessService")
    private String businessService;

    @NotNull
    @Size(max = 128)
    @JsonProperty("businessId")
    private String businessId;

    @NotNull
    @Size(max = 128)
    @JsonProperty("action")
    private String action;

    @NotNull
    @Size(max = 64)
    @JsonProperty("moduleName")
    private String moduleName;

    @JsonProperty("state")
    private State state;

    @JsonProperty("comment")
    private String comment;

    @JsonProperty("documents")
    @Valid
    private List<Document> documents;

    @JsonProperty("assignes")
    private List<User> assignes;

    public ProcessInstance addDocumentsItem(Document documentsItem) {
        if (this.documents == null) {
            this.documents = new ArrayList<>();
        }
        if (!this.documents.contains(documentsItem))
            this.documents.add(documentsItem);

        return this;
    }

}
```

</details>

<details>

<summary>State.java</summary>

```java
package digit.web.models;

import com.fasterxml.jackson.annotation.JsonProperty;
import lombok.*;

import javax.validation.Valid;
import javax.validation.constraints.Size;
import java.util.ArrayList;
import java.util.List;

@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
@Builder
@ToString
@EqualsAndHashCode(of = {"tenantId","businessServiceId","state"})
public class State   {

    @Size(max=256)
    @JsonProperty("uuid")
    private String uuid;

    @Size(max=256)
    @JsonProperty("tenantId")
    private String tenantId;

    @Size(max=256)
    @JsonProperty("businessServiceId")
    private String businessServiceId;

    @JsonProperty("sla")
    private Long sla;

    @Size(max=256)
    @JsonProperty("state")
    private String state;

    @Size(max=256)
    @JsonProperty("applicationStatus")
    private String applicationStatus;

    @JsonProperty("docUploadRequired")
    private Boolean docUploadRequired;

    @JsonProperty("isStartState")
    private Boolean isStartState;

    @JsonProperty("isTerminateState")
    private Boolean isTerminateState;

    @JsonProperty("isStateUpdatable")
    private Boolean isStateUpdatable;

    @JsonProperty("actions")
    @Valid
    private List<Action> actions;

    private AuditDetails auditDetails;


    public State addActionsItem(Action actionsItem) {
        if (this.actions == null) {
            this.actions = new ArrayList<>();
        }
        this.actions.add(actionsItem);
        return this;
    }

}
```



</details>

<details>

<summary>Action.java</summary>

```java
package digit.web.models;

import com.fasterxml.jackson.annotation.JsonProperty;
import lombok.*;

import javax.validation.Valid;
import javax.validation.constraints.Size;
import java.util.ArrayList;
import java.util.List;

@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
@Builder
@ToString
@EqualsAndHashCode(of = {"tenantId","currentState","action"})
public class Action {

    @Size(max=256)
    @JsonProperty("uuid")
    private String uuid;

    @Size(max=256)
    @JsonProperty("tenantId")
    private String tenantId;

    @Size(max=256)
    @JsonProperty("currentState")
    private String currentState;

    @Size(max=256)
    @JsonProperty("action")
    private String action;

    @Size(max=256)
    @JsonProperty("nextState")
    private String nextState;

    @Size(max=1024)
    @JsonProperty("roles")
    @Valid
    private List<String> roles;

    private AuditDetails auditDetails;


    public Action addRolesItem(String rolesItem) {
        if (this.roles == null) {
            this.roles = new ArrayList<>();
        }
        this.roles.add(rolesItem);
        return this;
    }

}
```

</details>

<details>

<summary>ProcessInstanceRequest.java</summary>

```java
package digit.web.models;

import com.fasterxml.jackson.annotation.JsonProperty;
import lombok.*;
import org.egov.common.contract.request.RequestInfo;

import javax.validation.Valid;
import javax.validation.constraints.NotNull;
import java.util.ArrayList;
import java.util.List;


@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
@Builder
@ToString
public class ProcessInstanceRequest {
    @JsonProperty("RequestInfo")
    private RequestInfo requestInfo;

    @JsonProperty("ProcessInstances")
    @Valid
    @NotNull
    private List<ProcessInstance> processInstances;


    public ProcessInstanceRequest addProcessInstanceItem(ProcessInstance processInstanceItem) {
        if (this.processInstances == null) {
            this.processInstances = new ArrayList<>();
        }
        this.processInstances.add(processInstanceItem);
        return this;
    }

}
```

</details>

<details>

<summary>ProcessInstanceResponse.java</summary>

```java
package digit.web.models;

import com.fasterxml.jackson.annotation.JsonProperty;
import lombok.*;
import org.egov.common.contract.response.ResponseInfo;

import javax.validation.Valid;
import java.util.ArrayList;
import java.util.List;

@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
@Builder
public class ProcessInstanceResponse {
    @JsonProperty("ResponseInfo")
    private ResponseInfo responseInfo;

    @JsonProperty("ProcessInstances")
    @Valid
    private List<ProcessInstance> processInstances;


    public ProcessInstanceResponse addProceInstanceItem(ProcessInstance proceInstanceItem) {
        if (this.processInstances == null) {
            this.processInstances = new ArrayList<>();
        }
        this.processInstances.add(proceInstanceItem);
        return this;
    }

}
```



</details>

<details>

<summary>BusinessService.java</summary>

```java
package digit.web.models;

import com.fasterxml.jackson.annotation.JsonInclude;
import com.fasterxml.jackson.annotation.JsonProperty;
import lombok.*;

import javax.validation.Valid;
import javax.validation.constraints.NotNull;
import javax.validation.constraints.Size;
import java.util.ArrayList;
import java.util.List;


@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
@Builder
@ToString
@EqualsAndHashCode(of = {"tenantId","businessService"})
@JsonInclude(JsonInclude.Include.NON_NULL)
public class BusinessService   {

    @Size(max=256)
    @JsonProperty("tenantId")
    private String tenantId = null;

    @Size(max=256)
    @JsonProperty("uuid")
    private String uuid = null;

    @Size(max=256)
    @JsonProperty("businessService")
    private String businessService = null;

    @Size(max=256)
    @JsonProperty("business")
    private String business = null;

    @Size(max=1024)
    @JsonProperty("getUri")
    private String getUri = null;

    @Size(max=1024)
    @JsonProperty("postUri")
    private String postUri = null;

    @JsonProperty("businessServiceSla")
    private Long businessServiceSla = null;

    @NotNull
    @Valid
    @JsonProperty("states")
    private List<State> states = null;

    @JsonProperty("auditDetails")
    private AuditDetails auditDetails = null;



    public BusinessService addStatesItem(State statesItem) {
        if (this.states == null) {
            this.states = new ArrayList<>();
        }
        this.states.add(statesItem);
        return this;
    }


    /**
     * Returns the currentState with the given uuid if not present returns null
     * @param uuid the uuid of the currentState to be returned
     * @return
     */
    public State getStateFromUuid(String uuid) {
        State state = null;
        if(this.states!=null){
            for(State s : this.states){
                if(s.getUuid().equalsIgnoreCase(uuid)){
                    state = s;
                    break;
                }
            }
        }
        return state;
    }



}ava
```



</details>

<details>

<summary>BusinessServiceResponse.java</summary>

```java
package digit.web.models;

import com.fasterxml.jackson.annotation.JsonProperty;
import lombok.*;
import org.egov.common.contract.response.ResponseInfo;

import javax.validation.Valid;
import javax.validation.constraints.NotNull;
import java.util.ArrayList;
import java.util.List;



@Data
@NoArgsConstructor
@AllArgsConstructor
@Builder
@ToString
public class BusinessServiceResponse {

    @JsonProperty("ResponseInfo")
    private ResponseInfo responseInfo;

    @JsonProperty("BusinessServices")
    @Valid
    @NotNull
    private List<BusinessService> businessServices;


    public BusinessServiceResponse addBusinessServiceItem(BusinessService businessServiceItem) {
        if (this.businessServices == null) {
            this.businessServices = new ArrayList<>();
        }
        this.businessServices.add(businessServiceItem);
        return this;
    }



}
```

</details>

#### Create Workflow service

Next, we have to create a class to transition the workflow object across its states. For this, create a class by the name of WorkflowService.java under the service directory and annotate it with @Service annotation. Add the following content to this class -

```java
package digit.service;

import com.fasterxml.jackson.databind.ObjectMapper;
import digit.config.BTRConfiguration;
import digit.repository.ServiceRequestRepository;
import digit.web.models.*;
import lombok.extern.slf4j.Slf4j;
import org.egov.common.contract.request.RequestInfo;
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
                digit.web.models.User user = new digit.web.models.User();
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

#### Add workflow to BirthRegistrationService

Add the following field to BirthRegistrationService.java

```java
 @Autowired
 private WorkflowService workflowService;
```

#### Transition the workflow

Modify the following methods in BirthRegistrationService.java as follows. Note that we are adding calls into the workflow service in each of these methods.

<details>

<summary>registerBtRequest</summary>

```java
  public List<BirthRegistrationApplication> registerBtRequest(BirthRegistrationRequest birthRegistrationRequest) {
        birthApplicationValidator.validateBirthApplication(birthRegistrationRequest);
        birthApplicationEnrichment.enrichBirthApplication(birthRegistrationRequest);

        // Enrich/Upsert user in upon birth registration
        userService.callUserService(birthRegistrationRequest);

        // WORKFLOW INTEGRATION HERE: Initiate workflow for the new application
        workflowService.updateWorkflowStatus(birthRegistrationRequest);

        // Push the application to the topic for persister to listen and persist
        producer.push(configuration.getCreateTopic(), birthRegistrationRequest);

        // Return the response back to user
        return birthRegistrationRequest.getBirthRegistrationApplications();
    }Java
```



</details>

<details>

<summary>updateBtApplication</summary>

```java
  public List<BirthRegistrationApplication> updateBtApplication(BirthRegistrationRequest birthRegistrationRequest) {
        // Validate whether the application that is being requested for update indeed exists
        List<BirthRegistrationApplication> existingApplication = birthApplicationValidator.validateApplicationUpdateRequest(birthRegistrationRequest);
        // Enrich application upon update
        birthApplicationEnrichment.enrichBirthApplicationUponUpdate(birthRegistrationRequest);
        //Workflow integration
        workflowService.updateWorkflowStatus(birthRegistrationRequest);
        // Just like create request, update request will be handled asynchronously by the persister
        producer.push(configuration.getUpdateTopic(), birthRegistrationRequest);

        return birthRegistrationRequest.getBirthRegistrationApplications();
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
            birthApplicationEnrichment.enrichFatherApplicantOnSearch(application);
            birthApplicationEnrichment.enrichMotherApplicantOnSearch(application);
        });
        
        //WORKFLOW INTEGRATION
        applications.forEach(application -> {
            application.setWorkflow(Workflow.builder().status(workflowService.getCurrentWorkflow(requestInfo, application.getTenantId(), application.getApplicationNumber()).getState().getState()).build());
        });

        // Otherwise, return the found applications
        return applications;
    }
```



</details>

#### Configure application.properties

Add the following properties to application.properties file of the birth registration module. Depending on whether you are port forwarding or using the service directly on the host, please update the host name.

```properties
#Workflow config
is.workflow.enabled=true
egov.workflow.host=http://localhost:8282
egov.workflow.transition.path=/egov-workflow-v2/egov-wf/process/_transition
egov.workflow.businessservice.search.path=/egov-workflow-v2/egov-wf/businessservice/_search
egov.workflow.processinstance.search.path=/egov-workflow-v2/egov-wf/process/_search
```

Now, when you run workflow service locally, your application will call into it to create the necessary tables in the DB and effect the workflow transitions.&#x20;

_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
