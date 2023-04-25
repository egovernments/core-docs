---
description: Generate Project Stub
---

# Generate Project Using API Specs

**Steps:** The first step in developing a microservice starts with preparing [Swagger ](https://swagger.io/docs/specification/2-0/what-is-swagger/)contracts that detail all the APIs that the service is going to expose for external consumption.

Use the Swagger Codegen tool and SwaggerHub to generate server stubs and client SDKs using these Swagger contracts.

{% hint style="info" %}
The following tutorial can be used for the creation of Swagger contracts -&#x20;

[OpenAPI 3.0 Tutorial| Swagger Tutorial For Beginners | Design REST API Using Swagger Editor](https://youtu.be/mViFmjcDOoA)&#x20;
{% endhint %}

Download the customized Codegen jar from [here](https://github.com/egovernments/DIGIT-OSS/blob/DIGIT\_DEVELOPER\_GUIDE/utilities/codegen-1.0-SNAPSHOT-jar-with-dependencies.jar) and make sure it is available in the class path.&#x20;

Following is the generic command to create an API skeleton for any swagger contract:

{% hint style="info" %}
```
java -jar codegen-1.0-SNAPSHOT-jar-with-dependencies.jar 
-l -t -u {CONTRACT_PATH } -a project_name -b /path/to/code/folder
```
{% endhint %}

For this guide, the following should be the sequence to generate the API skeleton using codegen jar:

1. Go to the folder where you have downloaded the codegen jar.
2. Execute the following command:

```
java -jar codegen-1.0-SNAPSHOT-jar-with-dependencies.jar -l -t -u https://github.com/egovernments/DIGIT-Dev/blob/birth-registration-service/municipal-services/birth-registration/birth-registration-api-spec.yaml -a birth-registration -b digit
```

OR

Download the contract from [here ](https://github.com/egovernments/DIGIT-Dev/blob/birth-registration-service/municipal-services/birth-registration/birth-registration-api-spec.yaml)and save it in a file locally. Run the following command to generate the skeleton code from the contract.

```
java -jar codegen-1.0-SNAPSHOT-jar-with-dependencies.jar -l -t -u file:///{ABSOLUTE_PATH_OF_FILE} -a birth-registration -b digit
```

1. Rename the `output` folder to birth-registration. Import it in Eclipse or VS Code.
2. Update the spring-boot-starter-parent to 2.2.6-RELEASE in pom.xml. After updating the spring boot version do a maven update.
3. Put a slash in front of server.contextPath and add this property to application.properties file which helps requests handlers to serve requests -

```
server.contextPath=/birth-registration
server.servlet.context-path=/birth-registration
```

&#x20;4\. Add these external dependencies to pom.xml:

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

