# Integration with User Service

#### **Integration with User service**&#x20;

The user service provides the capabilities of creating a user, searching for a user and retrieving the details of a user. This module will search for a user and if not found, create that user with the user service.

{% hint style="info" %}
DIGIT's user service masks PII that gets stored in the database using the encryption service.
{% endhint %}

Create the following POJOs under the `model` directory:

<details>

<summary>CreateUserRequest.java</summary>

```java
package digit.web.models;

import com.fasterxml.jackson.annotation.JsonProperty;
import lombok.AllArgsConstructor;
import lombok.Getter;
import lombok.NoArgsConstructor;
import org.egov.common.contract.request.RequestInfo;

@AllArgsConstructor
@Getter
@NoArgsConstructor
public class CreateUserRequest {

    @JsonProperty("requestInfo")
    private RequestInfo requestInfo;

    @JsonProperty("user")
    private User user;

}
```

</details>

<details>

<summary>UserSearchRequest.java</summary>

```java
package digit.web.models;

import com.fasterxml.jackson.annotation.JsonProperty;
import lombok.Getter;
import lombok.Setter;
import org.egov.common.contract.request.RequestInfo;

import java.util.Collections;
import java.util.List;


@Getter
@Setter
public class UserSearchRequest {

    @JsonProperty("RequestInfo")
    private RequestInfo requestInfo;

    @JsonProperty("uuid")
    private List<String> uuid;

    @JsonProperty("id")
    private List<String> id;

    @JsonProperty("userName")
    private String userName;

    @JsonProperty("name")
    private String name;

    @JsonProperty("mobileNumber")
    private String mobileNumber;

    @JsonProperty("aadhaarNumber")
    private String aadhaarNumber;

    @JsonProperty("pan")
    private String pan;

    @JsonProperty("emailId")
    private String emailId;

    @JsonProperty("fuzzyLogic")
    private boolean fuzzyLogic;

    @JsonProperty("active")
    @Setter
    private Boolean active;

    @JsonProperty("tenantId")
    private String tenantId;

    @JsonProperty("pageSize")
    private int pageSize;

    @JsonProperty("pageNumber")
    private int pageNumber = 0;

    @JsonProperty("sort")
    private List<String> sort = Collections.singletonList("name");

    @JsonProperty("userType")
    private String userType;

    @JsonProperty("roleCodes")
    private List<String> roleCodes;

}
```

</details>

<details>

<summary>UserDetailResponse.java</summary>

```java
package digit.web.models;

import com.fasterxml.jackson.annotation.JsonProperty;
import lombok.AllArgsConstructor;
import lombok.Getter;
import lombok.NoArgsConstructor;
import lombok.ToString;
import org.egov.common.contract.response.ResponseInfo;

import java.util.List;

@AllArgsConstructor
@NoArgsConstructor
@Getter
@ToString
public class UserDetailResponse {
    @JsonProperty("responseInfo")
    ResponseInfo responseInfo;

    @JsonProperty("user")
    List<User> user;
}
```

</details>

Create a class by the name of UserService under service folder and add the following content to it:

<details>

<summary>UserService.java</summary>

{% code overflow="wrap" %}
```java
package digit.service;

import digit.config.BTRConfiguration;
import digit.utils.UserUtil;
import digit.web.models.*;
import lombok.extern.slf4j.Slf4j;
import org.apache.commons.lang.StringUtils;
import org.egov.common.contract.request.RequestInfo;
import org.egov.tracer.model.CustomException;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.util.CollectionUtils;

import java.util.Collections;
import java.util.List;
import java.util.Map;
import java.util.function.Function;
import java.util.stream.Collectors;


@Service
@Slf4j
public class UserService {
    private UserUtil userUtils;

    private BTRConfiguration config;

    @Autowired
    public UserService(UserUtil userUtils, BTRConfiguration config) {
        this.userUtils = userUtils;
        this.config = config;
    }

    /**
     * Calls user service to enrich user from search or upsert user
     * @param request
     */
    public void callUserService(BirthRegistrationRequest request){
        request.getBirthRegistrationApplications().forEach(application -> {
            if(!StringUtils.isEmpty(application.getFather().getId()))
                enrichUser(application, request.getRequestInfo());
            else {
                User user = createFatherUser(application);
                application.getFather().setId(upsertUser(user, request.getRequestInfo()));
            }
        });

        request.getBirthRegistrationApplications().forEach(application -> {
            if(!StringUtils.isEmpty(application.getMother().getId()))
                enrichUser(application, request.getRequestInfo());
            else {
                User user = createMotherUser(application);
                application.getMother().setId(upsertUser(user, request.getRequestInfo()));
            }
        });
    }

    private User createFatherUser(BirthRegistrationApplication application){
        FatherApplicant father = application.getFather();
        User user = User.builder().userName(father.getUserName())
                .name(father.getName())
                .mobileNumber(father.getMobileNumber())
                .emailId(father.getEmailId())
                .altContactNumber(father.getAltContactNumber())
                .tenantId(father.getTenantId())
                .type(father.getType())
                .roles(father.getRoles())
                .build();
//        String tenantId = father.getTenantId();
        return user;
    }

    private User createMotherUser(BirthRegistrationApplication application){
        MotherApplicant mother = application.getMother();
        User user = User.builder().userName(mother.getUserName())
                .name(mother.getName())
                .mobileNumber(mother.getMobileNumber())
                .emailId(mother.getEmailId())
                .altContactNumber(mother.getAltContactNumber())
                .tenantId(mother.getTenantId())
                .type(mother.getType())
                .roles(mother.getRoles())
                .build();
//        String tenantId = father.getTenantId();
        return user;
    }
    private String upsertUser(User user, RequestInfo requestInfo){

        String tenantId = user.getTenantId();
        User userServiceResponse = null;

        // Search on mobile number as user name
        UserDetailResponse userDetailResponse = searchUser(userUtils.getStateLevelTenant(tenantId),null, user.getMobileNumber());
        if (!userDetailResponse.getUser().isEmpty()) {
            User userFromSearch = userDetailResponse.getUser().get(0);
            log.info(userFromSearch.toString());
            if(!user.getUserName().equalsIgnoreCase(userFromSearch.getUserName())){
                userServiceResponse = updateUser(requestInfo,user,userFromSearch);
            }
            else userServiceResponse = userDetailResponse.getUser().get(0);
        }
        else {
            userServiceResponse = createUser(requestInfo,tenantId,user);
        }

        // Enrich the accountId
       // user.setId(userServiceResponse.getUuid());
        return userServiceResponse.getUuid();
    }


    private void enrichUser(BirthRegistrationApplication application, RequestInfo requestInfo){
        String accountIdFather = application.getFather().getId();
        String accountIdMother = application.getMother().getId();
        String tenantId = application.getTenantId();

        UserDetailResponse userDetailResponseFather = searchUser(userUtils.getStateLevelTenant(tenantId),accountIdFather,null);
        UserDetailResponse userDetailResponseMother = searchUser(userUtils.getStateLevelTenant(tenantId),accountIdMother,null);
        if(userDetailResponseFather.getUser().isEmpty())
            throw new CustomException("INVALID_ACCOUNTID","No user exist for the given accountId");

        else application.getFather().setId(userDetailResponseFather.getUser().get(0).getUuid());

        if(userDetailResponseMother.getUser().isEmpty())
            throw new CustomException("INVALID_ACCOUNTID","No user exist for the given accountId");

        else application.getMother().setId(userDetailResponseMother.getUser().get(0).getUuid());

    }

    /**
     * Creates the user from the given userInfo by calling user service
     * @param requestInfo
     * @param tenantId
     * @param userInfo
     * @return
     */
    private User createUser(RequestInfo requestInfo,String tenantId, User userInfo) {

        userUtils.addUserDefaultFields(userInfo.getMobileNumber(),tenantId, userInfo);
        StringBuilder uri = new StringBuilder(config.getUserHost())
                .append(config.getUserContextPath())
                .append(config.getUserCreateEndpoint());

        CreateUserRequest user = new CreateUserRequest(requestInfo, userInfo);
        log.info(user.getUser().toString());
        UserDetailResponse userDetailResponse = userUtils.userCall(user, uri);

        return userDetailResponse.getUser().get(0);

    }

    /**
     * Updates the given user by calling user service
     * @param requestInfo
     * @param user
     * @param userFromSearch
     * @return
     */
    private User updateUser(RequestInfo requestInfo,User user,User userFromSearch) {

        userFromSearch.setName(user.getName());
        userFromSearch.setActive(true);

        StringBuilder uri = new StringBuilder(config.getUserHost())
                .append(config.getUserContextPath())
                .append(config.getUserUpdateEndpoint());


        UserDetailResponse userDetailResponse = userUtils.userCall(new CreateUserRequest(requestInfo, userFromSearch), uri);

        return userDetailResponse.getUser().get(0);

    }

    /**
     * calls the user search API based on the given accountId and userName
     * @param stateLevelTenant
     * @param accountId
     * @param userName
     * @return
     */
    public UserDetailResponse searchUser(String stateLevelTenant, String accountId, String userName){

        UserSearchRequest userSearchRequest =new UserSearchRequest();
        userSearchRequest.setActive(true);
        userSearchRequest.setUserType("CITIZEN");
        userSearchRequest.setTenantId(stateLevelTenant);

        if(StringUtils.isEmpty(accountId) && StringUtils.isEmpty(userName))
            return null;

        if(!StringUtils.isEmpty(accountId))
            userSearchRequest.setUuid(Collections.singletonList(accountId));

        if(!StringUtils.isEmpty(userName))
            userSearchRequest.setUserName(userName);

        StringBuilder uri = new StringBuilder(config.getUserHost()).append(config.getUserSearchEndpoint());
        return userUtils.userCall(userSearchRequest,uri);

    }

    /**
     * calls the user search API based on the given list of user uuids
     * @param uuids
     * @return
     */
    private Map<String,User> searchBulkUser(List<String> uuids){

        UserSearchRequest userSearchRequest =new UserSearchRequest();
        userSearchRequest.setActive(true);
        userSearchRequest.setUserType("CITIZEN");


        if(!CollectionUtils.isEmpty(uuids))
            userSearchRequest.setUuid(uuids);


        StringBuilder uri = new StringBuilder(config.getUserHost()).append(config.getUserSearchEndpoint());
        UserDetailResponse userDetailResponse = userUtils.userCall(userSearchRequest,uri);
        List<User> users = userDetailResponse.getUser();

        if(CollectionUtils.isEmpty(users))
            throw new CustomException("USER_NOT_FOUND","No user found for the uuids");

        Map<String,User> idToUserMap = users.stream().collect(Collectors.toMap(User::getUuid, Function.identity()));

        return idToUserMap;
    }

}
```
{% endcode %}



</details>

#### Changes to BirthApplicationEnrichment.java

Add the below methods to the enrichment class we created. When we search for an application, the code below will search for the users associated with the application and add in their details to the response object.

<details>

<summary>enrichFatherApplicantOnSearch</summary>

```java
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
        UserDetailResponse motherUserResponse = userService.searchUser(userUtils.getStateLevelTenant(application.getTenantId()),application.getMother().getId(),null);
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
```



</details>

#### Changes to BirthRegistrationService.java

Add in a userService object:

```java
 @Autowired
 private UserService userService;
```

And enhance the following two methods in BirthRegistrationService.java:

<details>

<summary>registerBtRequest</summary>

```java
public List<BirthRegistrationApplication> registerBtRequest(BirthRegistrationRequest birthRegistrationRequest) {
        birthApplicationValidator.validateBirthApplication(birthRegistrationRequest);
        birthApplicationEnrichment.enrichBirthApplication(birthRegistrationRequest);

        // Enrich/Upsert user in upon birth registration
        userService.callUserService(birthRegistrationRequest);

        // Push the application to the topic for persister to listen and persist
        producer.push(configuration.getCreateTopic(), birthRegistrationRequest);

        // Return the response back to user
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

        // Otherwise, return the found applications
        return applications;
    }
```

</details>

Add the following properties in application.properties file:

{% hint style="info" %}
Note that if you are port-forwarding using k8s, you will use localhost. Else, if you have a valid auth token, please provide the name of the host here.&#x20;
{% endhint %}

```properties
#User config
egov.user.host=http://localhost:8284/
egov.user.context.path=/user/users
egov.user.create.path=/_createnovalidate
egov.user.search.path=/user/_search
egov.user.update.path=/_updatenovalidate
```

_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
