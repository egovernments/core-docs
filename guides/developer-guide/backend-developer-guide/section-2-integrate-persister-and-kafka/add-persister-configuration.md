# Add Persister Configuration

## Overview

This page provides the steps on how to add persister configuration.

The persister configuration is written in a YAML format. The INSERT and UPDATE queries for each table are added in prepared statement format, followed by the jsonPaths of values that have to be inserted/updated.

For example, for a table named studentinfo with id, name, age, and marks fields, the following configuration will get the persister ready to insert data into studentinfo table -

{% code lineNumbers="true" %}
```yaml
serviceMaps:
 serviceName: student-management-service
 mappings:
 - version: 1.0
   description: Persists student details in studentinfo table
   fromTopic: save-student-info
   isTransaction: true
   queryMaps:
       - query: INSERT INTO studentinfo( id, name, age, marks) VALUES (?, ?, ?, ?);
         basePath: Students.*
         jsonMaps:
          - jsonPath: $.Students.*.id

          - jsonPath: $.Students.*.name

          - jsonPath: $.Students.*.age

          - jsonPath: $.Students.*.marks
```
{% endcode %}

## Steps

### **Add Persister Configuration**&#x20;

1. Fork the [configs repo](https://github.com/egovernments/configs). Ignore if done already. Clone configs repo in the local environment.

```git
git clone -o upstream https://github.com/<your_configs_repo>/configs
```

2. Persister configurations for all modules are present under the `egov-persister` folder. Create a file by the name of `btr-persister.yml` (or any other name) under the `egov-persister` folder.
3. Add the following content to it -

{% code lineNumbers="true" %}
```yaml
serviceMaps:
  serviceName: btr-services
  mappings:
    - version: 1.0
      description: Persists birth details in tables
      fromTopic: save-bt-application
      isTransaction: true	
      queryMaps:

        - query: INSERT INTO eg_bt_registration(id,tenantid,applicationnumber,babyfirstname,babylastname,fatherid,motherid,doctorname,hospitalname,placeofbirth,timeofbirth,createdby,lastmodifiedby,createdtime, lastmodifiedtime) VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?,?,?,?);
          basePath: BirthRegistrationApplications.*
          jsonMaps:
            - jsonPath: $.BirthRegistrationApplications.*.id

            - jsonPath: $.BirthRegistrationApplications.*.tenantId

            - jsonPath: $.BirthRegistrationApplications.*.applicationNumber
          
            - jsonPath: $.BirthRegistrationApplications.*.babyFirstName
            
            - jsonPath: $.BirthRegistrationApplications.*.babyLastName
          
            - jsonPath: $.BirthRegistrationApplications.*.fatherOfApplicant.id
            
            - jsonPath: $.BirthRegistrationApplications.*.motherOfApplicant.id
                                           
            - jsonPath: $.BirthRegistrationApplications.*.doctorName
            
            - jsonPath: $.BirthRegistrationApplications.*.hospitalName
            
            - jsonPath: $.BirthRegistrationApplications.*.placeOfBirth

            - jsonPath: $.BirthRegistrationApplications.*.timeOfBirth
            
            - jsonPath: $.BirthRegistrationApplications.*.auditDetails.createdBy

            - jsonPath: $.BirthRegistrationApplications.*.auditDetails.lastModifiedBy

            - jsonPath: $.BirthRegistrationApplications.*.auditDetails.createdTime
            
            - jsonPath: $.BirthRegistrationApplications.*.auditDetails.lastModifiedTime

        - query: INSERT INTO eg_bt_address(id, tenantid, doorno, latitude, longitude, buildingname, addressid, addressnumber, type, addressline1, addressline2, landmark, street, city, locality, pincode, detail, registrationid, createdby, lastmodifiedby, createdtime, lastmodifiedtime) VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?);
          basePath: BirthRegistrationApplications.*
          jsonMaps:
            - jsonPath: $.BirthRegistrationApplications.*.address.id

            - jsonPath: $.BirthRegistrationApplications.*.address.tenantId

            - jsonPath: $.BirthRegistrationApplications.*.address.doorNo

            - jsonPath: $.BirthRegistrationApplications.*.address.latitude

            - jsonPath: $.BirthRegistrationApplications.*.address.longitude

            - jsonPath: $.BirthRegistrationApplications.*.address.buildingName

            - jsonPath: $.BirthRegistrationApplications.*.address.addressId

            - jsonPath: $.BirthRegistrationApplications.*.address.addressNumber

            - jsonPath: $.BirthRegistrationApplications.*.address.type

            - jsonPath: $.BirthRegistrationApplications.*.address.addressLine1

            - jsonPath: $.BirthRegistrationApplications.*.address.addressLine2

            - jsonPath: $.BirthRegistrationApplications.*.address.landmark

            - jsonPath: $.BirthRegistrationApplications.*.address.street

            - jsonPath: $.BirthRegistrationApplications.*.address.city

            - jsonPath: $.BirthRegistrationApplications.*.address.locality.name

            - jsonPath: $.BirthRegistrationApplications.*.address.pincode

            - jsonPath: $.BirthRegistrationApplications.*.address.detail

            - jsonPath: $.BirthRegistrationApplications.*.id

            - jsonPath: $.BirthRegistrationApplications.*.address.createdBy

            - jsonPath: $.BirthRegistrationApplications.*.address.lastModifiedBy

            - jsonPath: $.BirthRegistrationApplications.*.address.createdTime

            - jsonPath: $.BirthRegistrationApplications.*.address.lastModifiedTime

    - version: 1.0
      description: Update birth registration applications in table
      fromTopic: update-bt-application
      isTransaction: true
      queryMaps:
        - query: UPDATE eg_bt_registration SET tenantid = ?,babyFirstName = ?, timeOfBirth = ? WHERE id=?;
          basePath: BirthRegistrationApplications.*
          jsonMaps:
            - jsonPath: $.BirthRegistrationApplications.*.tenantId

            - jsonPath: $.BirthRegistrationApplications.*.babyFirstName
           
            - jsonPath: $.BirthRegistrationApplications.*.timeOfBirth

            - jsonPath: $.BirthRegistrationApplications.*.id
```
{% endcode %}

### **Run Persister Locally**

1. Import all the core-services projects as Maven projects into your IDE. It is assumed that you have already cloned the DIGIT code locally.&#x20;
2. Modify the application.properties file in the egov-persister project and set the following property:

{% code overflow="wrap" %}
```properties
egov.persist.yml.repo.path=file:///Users/subha/Code/configs/egov-persister/btr-persister.yml
```
{% endcode %}

{% hint style="info" %}
**Note:** You can set a comma-separated list of files as the value of the above property. If you are running multiple services locally, then this has to be a comma-separated list of persister config files. Make sure you always give the absolute path.
{% endhint %}

3. Make sure the Spring DB configurations and Flyway config reflect the same database as what has been set in the module itself. Otherwise, we will see failures in the persister code.&#x20;

```properties
spring.datasource.driver-class-name=org.postgresql.Driver
spring.datasource.url=jdbc:postgresql://localhost:5432/birthregistration3
spring.datasource.username=yourusername
spring.datasource.password=yourpassword
```

4. Make sure the Kafka is running locally. Now, go ahead and run the EgovPersistApplication from the IDE. Check the console to make sure it is listening to the right topics as configured in your module's application.properties file.

The persister is now ready for use.

### **Deploy Persister Configuration**

{% hint style="info" %}
**Note:** Below steps are for when you deploy your code to the DIGIT env, not for local development. You may choose to do this when you build and deploy.&#x20;
{% endhint %}

1. Push the code to the appropriate branch from which your environment will read it.&#x20;
2. Navigate to your fork of the DIGIT-DevOps repository. Under the `deploy-as-code/helm/environments` directory, find the deployment helm chart that was used to deploy DIGIT. &#x20;
3.  In the deployment helm chart (which was used to set up the DIGIT environment), find "egov-persister". Find the "persist-yml-path" property and add the path to your new persister file here.&#x20;

    In the snippet below, `file:///work-dir/configs/egov-persister/birth-module-developer-guide.yml`

{% code overflow="wrap" lineNumbers="true" %}
```yaml
egov-persister:
  replicas: 6
  persist-yml-path: "file:///work-dir/configs/egov-persister/privacy-audit.yml,file:///work-dir/configs/egov-persister/pgr-migration-batch.yml,file:///work-dir/configs/egov-persister/pgr-services-persister.yml,file:///work-dir/configs/egov-persister/pdf-filestoreid-update.yml,file:///work-dir/configs/egov-persister/chatbot.yml,file:///work-dir/configs/egov-persister/pt-mutation-calculator-persister.yml,file:///work-dir/configs/egov-persister/apportion-persister.yml,file:///work-dir/configs/egov-persister/property-services-registry.yml,file:///work-dir/configs/egov-persister/billing-services-persist.yml,file:///work-dir/configs/egov-persister/egf-bill.yaml,file:///work-dir/configs/egov-persister/egov-user-event-persister.yml,file:///work-dir/configs/egov-persister/egov-workflow-v2-persister.yml,file:///work-dir/configs/egov-persister/firenoc_persiter.yaml,file:///work-dir/configs/egov-persister/hrms-employee-persister.yml,file:///work-dir/configs/egov-persister/pdf-generator.yml,file:///work-dir/configs/egov-persister/pg-service-persister.yml,file:///work-dir/configs/egov-persister/pgr.v3.yml,file:///work-dir/configs/egov-persister/property-services.yml,file:///work-dir/configs/egov-persister/pt-calculator-v2-persister.yml,file:///work-dir/configs/egov-persister/pt-drafts.yml,file:///work-dir/configs/egov-persister/pt-persist.yml,file:///work-dir/configs/egov-persister/tl-billing-slab-persister.yml,file:///work-dir/configs/egov-persister/tl-calculation-persister.yml,file:///work-dir/configs/egov-persister/tradelicense.yml,file:///work-dir/configs/egov-persister/uploader-persister.yml,file:///work-dir/configs/egov-persister/collection-migration-persister.yml,file:///work-dir/configs/egov-persister/water-persist.yml,file:///work-dir/configs/egov-persister/water-meter.yml,file:///work-dir/configs/egov-persister/assessment-persister.yml,file:///work-dir/configs/egov-persister/sewerage-persist.yml,file:///work-dir/configs/egov-persister/bpa-persister.yml,file:///work-dir/configs/egov-persister/property-services-migration-temp-config.yml,file:///work-dir/configs/egov-persister/assessment-persister-migration-temp.yml,file:///work-dir/configs/egov-persister/migration-batch-count-persister.yml,file:///work-dir/configs/egov-persister/land-persister.yml,file:///work-dir/configs/egov-persister/noc-persister.yml,file:///work-dir/configs/egov-persister/fsm-persister.yaml,file:///work-dir/configs/egov-persister/vehicle-persister.yaml,file:///work-dir/configs/egov-persister/vendor-persister.yaml,file:///work-dir/configs/egov-persister/fsm-calculator-persister.yaml,file:///work-dir/configs/egov-persister/echallan.yml,file:///work-dir/configs/egov-persister/egov-document-upload-persister.yml,file:///work-dir/configs/egov-persister/egov-survey-service-persister.yml,file:///work-dir/configs/egov-persister/firenoc-calculator-persister.yml,file:///work-dir/configs/egov-persister/bulk-bill-generation-audit.yml,file:///work-dir/configs/egov-persister/nss-persister.yml,file:///work-dir/configs/egov-persister/birth-death.yml,file:///work-dir/configs/egov-persister/bulk-bill-generator-ws.yml,file:///work-dir/configs/egov-persister/bulk-bill-generator-sw.yml,file:///work-dir/configs/egov-persister/audit-service-persister.yml,file:///work-dir/configs/egov-persister/birth-module-developer-guide.yml"

```
{% endcode %}

4. Raise a PR to the appropriate branch of the DevOps repo (master, in egov case) which was forked/used to create the deployment. Once that is merged, restart the indexer service in your environment so it will pick up this new config for the module.&#x20;

