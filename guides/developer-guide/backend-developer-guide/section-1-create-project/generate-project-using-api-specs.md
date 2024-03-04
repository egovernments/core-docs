---
description: Generate Project Stub
---

# Generate Project Using API Specs

## **Overview**

This page provides detailed steps for generating projects using the given API specifications.

## **Steps**

### **Build A Microservice**

1. Prepare [Swagger ](https://swagger.io/docs/specification/2-0/what-is-swagger/)contracts that detail all the APIs that the service is going to expose for external consumption. eGov uses a customised [Swagger Codegen ](https://github.com/egovernments/Digit-Core/blob/codegen-openapi-3.0/accelerators/codegen/codegen-RELEASE-1.0.jar)tool.&#x20;
2. Download the jar file and make sure it is available in the classpath. Use the [Swagger Codegen tool](https://github.com/egovernments/Digit-Core/blob/codegen-openapi-3.0/accelerators/codegen/codegen-RELEASE-1.0.jar) to generate client SDKs using these Swagger contracts.&#x20;

{% hint style="info" %}
Refer to the following tutorials to understand the creation of Swagger contracts -&#x20;

[OpenAPI 3.0 Tutorial| Swagger Tutorial For Beginners | Design REST API Using Swagger Editor](https://youtu.be/mViFmjcDOoA)&#x20;
{% endhint %}

### Generate API Skeleton

1. Use the generic command below to create an API skeleton for any Swagger contract:

{% hint style="info" %}
```
java -jar codegen-1.0-SNAPSHOT-jar-with-dependencies.jar 
-l -t -u {CONTRACT_PATH } -a project_name -b /path/to/code/folder
```
{% endhint %}

The following sequence is used to generate the API skeleton using codegen jar:

1. Navigate to the folder where you have downloaded the codegen jar.
2. Execute the following command:

```
java -jar codegen-1.0-SNAPSHOT-jar-with-dependencies.jar -l -t -u https://github.com/egovernments/DIGIT-Dev/blob/birth-registration-service/municipal-services/birth-registration/birth-registration-api-spec.yaml -a birth-registration -b digit
```

OR

Download the contract [available here ](https://github.com/egovernments/DIGIT-OSS/tree/master/municipal-services/birth-death-services)and save it in a file locally. Run the following command to generate the skeleton code from the contract.

```
java -jar codegen-1.0-SNAPSHOT-jar-with-dependencies.jar -l -t -u file:///{ABSOLUTE_PATH_OF_FILE} -a birth-registration -b digit
```

2. Rename the `output` folder to birth-registration.&#x20;
3. Import it in Eclipse or VS Code.
4. Update the spring-boot-starter-parent to 2.2.6-RELEASE in pom.xml.&#x20;
5. Perform a maven update once the spring boot version is updated.&#x20;
6. Make sure the following dependency is present in the pom.xml. If the version is different, make sure to update it to the version given below:&#x20;

```xml
<dependency>
	<groupId>org.egov.services</groupId>
	<artifactId>services-common</artifactId>
	<version>2.0.0-SNAPSHOT</version>
</dependency>
```

7. Put a slash in front of server.contextPath and add this property to the application.properties file which helps request handlers to serve requests -

```
server.contextPath=/birth-registration
server.servlet.context-path=/birth-registration
```

8. Add the below external dependencies to pom.xml:

{% code lineNumbers="true" %}
```xml
<dependency>
   <groupId>org.flywaydb</groupId>
   <artifactId>flyway-core</artifactId>
</dependency>
<dependency>
   <groupId>org.egov</groupId>
   <artifactId>mdms-client</artifactId>
   <version>0.0.2-SNAPSHOT</version>
</dependency>
<dependency>
   <groupId>org.postgresql</groupId>
   <artifactId>postgresql</artifactId>
   <version>42.2.2.jre7</version>
</dependency>
```
{% endcode %}

