# Email Notification Service

### Overview <a href="#overview" id="overview"></a>

The objective of this service is to create a common point to manage all the email notifications being sent out of the platform. Notification email service consumes emal requests from the kafka notification topic and process them to send it to an third party service. Modules like PT, TL, PGR etc make use of this service to send messages through the Kafka Queue.

### Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before you proceed with the documentation, make sure the following pre-requisites are met -

* Prior Knowledge of Java/J2EE
* Prior Knowledge of SpringBoot
* Prior Knowledge of Third party API integration
* Prior Knowledge of REST APIs and related concepts like path parameters, headers, JSON etc
* Prior Knowledge of Kafka and related concepts like Producer, Consumer, Topic etc.

### Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

* Provide common platform to send email notification to user
* Support localised email.

### Configuration Details <a href="#configuration-details" id="configuration-details"></a>

egov-notification-mail is a consumer which listens to the egov.core.notification.email topic, reads the message and generates email using SMTP Protocol. The services needs the the senders email configured. On the other hand, if senders email is not configured, the services gets the email id by internally calling egov-user service to fetch email id. Once the email is generated, the content is localized by egov-localization service after which its been notified to the email id.&#x20;

### Deployment Details <a href="#deployment-details" id="deployment-details"></a>

1. Deploy the latest version of notification email Service.
2. Make sure the consumer topic name for email service is added in deployment configs

### Integration <a href="#integration" id="integration"></a>

#### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

The email notification service is used to send out email notifications for all miscellaneous / adhoc services which citizens avail from ULBs.

#### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

* Can perform service-specific business logic without impacting the other module.
* In the future, if we want to expose the application to citizen then it can be done easily.

#### Steps to Integration <a href="#steps-to-integration" id="steps-to-integration"></a>

1. To integrate, the client service should send email requests to email notification consumer topic.
