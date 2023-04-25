# Configure Application Properties

**Overview:** The application.properties file is already populated with default values. Please read on to customise and add extra values for your application (if required).&#x20;

**Process Flow:** Kafka topics for the module that needs to be added are detailed [here](configure-application-properties.md#kafka-topics-for-module).&#x20;

{% hint style="info" %}
There are three ways of accessing services:

a. Run the code locally

b. Access the service in a DIGIT environment

c. Access the service locally via port forwarding. This bypasses Zuul's authentication and authorization.&#x20;

Wherever localhost is in the URL, Kubernetes port forwarding has been set up from the dev environment to the specified port. In your setup, modify the URLs for the various services depending on whether you are using them from an environment or running it locally or accessing them via port-forwarding.&#x20;

For example, if no port forwarding has been done, you will have to provide the FQDN of your digit install instead of localhost. Also, without port forwarding, you will have to update the auth tokens in your .aws profile file periodically.&#x20;
{% endhint %}

All dependent service host URLs and API endpoints should be added in application.properties. This guide uses the User, Localisation, HRMS, IDGen, MDMS & workflow services running in a DIGIT dev environment.&#x20;

**Steps:** Add the following properties to the `application.properties` file.

```properties
#Localization config
egov.localization.host=https://dev.digit.org
egov.localization.workDir.path=/localization/messages/v1
egov.localization.context.path=/localization/messages/v1
egov.localization.search.endpoint=/_search
egov.localization.statelevel=true

#mdms urls
egov.mdms.host=https://dev.digit.org
egov.mdms.search.endpoint=/egov-mdms-service/v1/_search

#hrms urls
egov.hrms.host=https://dev.digit.org
egov.hrms.search.endpoint=/egov-hrms/employees/_search

#User config
#egov.user.host=https://dev.digit.org
egov.user.host=http://localhost:8284/
egov.user.context.path=/user/users
egov.user.create.path=/_createnovalidate
egov.user.search.path=/user/_search
egov.user.update.path=/_updatenovalidate

#Idgen Config
egov.idgen.host=http://localhost:8285/
egov.idgen.path=egov-idgen/id/_generate

#Workflow config
is.workflow.enabled=true
egov.workflow.host=http://localhost:8280
egov.workflow.transition.path=/egov-workflow-v2/egov-wf/process/_transition
egov.workflow.businessservice.search.path=/egov-workflow-v2/egov-wf/businessservice/_search
egov.workflow.processinstance.search.path=/egov-workflow-v2/egov-wf/process/_search
```

The following properties must be added for configuring the database and Kafka server (Use the default values, in case you want to tune the Kafka server that can be overwritten during deployment).

Once all the external dependencies have been added to pom.xml and these maven changes have been reloaded, the following properties should be added to application.properties file to configure the database and Kafka for development -

```properties
#DATABASE CONFIGURATION
spring.datasource.driver-class-name=org.postgresql.Driver
spring.datasource.url=jdbc:postgresql://localhost:5432/birthregn
spring.datasource.username=birth
spring.datasource.password=birth
```

### Kafka Configuration

```properties
# KAFKA SERVER CONFIGURATIONS
kafka.config.bootstrap_server_config=localhost:9092
spring.kafka.consumer.value-deserializer=org.egov.tracer.kafka.deserializer.HashMapDeserializer
spring.kafka.consumer.key-deserializer=org.apache.kafka.common.serialization.StringDeserializer
spring.kafka.consumer.group-id={PLACEHOLDER_PUT_KAFKA_CONSUMER_NAME}
spring.kafka.producer.key-serializer=org.apache.kafka.common.serialization.StringSerializer
spring.kafka.producer.value-serializer=org.springframework.kafka.support.serializer.JsonSerializer
spring.kafka.listener.missing-topics-fatal=false
spring.kafka.consumer.properties.spring.json.use.type.headers=false

# KAFKA CONSUMER CONFIGURATIONS
kafka.consumer.config.auto_commit=true
kafka.consumer.config.auto_commit_interval=100
kafka.consumer.config.session_timeout=15000
kafka.consumer.config.auto_offset_reset=earliest

# KAFKA PRODUCER CONFIGURATIONS
kafka.producer.config.retries_config=0
kafka.producer.config.batch_size_config=16384
kafka.producer.config.linger_ms_config=1
kafka.producer.config.buffer_memory_config=33554432
```

### Kafka Topics For Module

Append Kafka to create and update topics for the module. DIGIT services use different to create and update topics per module:

```properties
# Birth registration Kafka config
btr.kafka.create.topic=save-bt-application
btr.kafka.update.topic=update-bt-application
btr.default.offset=0
btr.default.limit=10
btr.search.max.limit=50
```

