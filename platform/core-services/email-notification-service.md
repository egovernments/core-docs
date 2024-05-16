# Email Notification Service

## Overview <a href="#overview" id="overview"></a>

The objective of this service is to create a common point to manage all the email notifications being sent out of the platform. The notification email service consumes email requests from the Kafka notification topic and processes them to send them to a third-party service. Modules like PT, TL, PGR etc make use of this service to send messages through the Kafka Queue.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before you proceed with the documentation, make sure the following pre-requisites are met -

* Prior knowledge of Java/J2EE
* Prior knowledge of SpringBoot
* Prior knowledge of Third party API integration
* Prior knowledge of REST APIs and related concepts like path parameters, headers, JSON etc
* Prior knowledge of Kafka and related concepts like Producer, Consumer, Topic etc.

## Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

* Provide a common platform to send email notifications to the user
* Support localised email.

## Configuration Details <a href="#configuration-details" id="configuration-details"></a>

The egov-notification-mail is a consumer which listens to the egov.core.notification.email topic reads the message and generates email using SMTP Protocol. The services need the senders' email configured. On the other hand, if the senders' email is not configured, the services get the email id by internally calling egov-user service to fetch the email id. Once the email is generated, the content is localized by egov-localization service after which it is notified to the email id.&#x20;

## Deployment Details <a href="#deployment-details" id="deployment-details"></a>

1. Deploy the latest version of the notification email service.
2. Make sure the consumer topic name for email service is added in deployment configs

## Integration Details <a href="#integration" id="integration"></a>

### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

The email notification service is used to send out email notifications for all miscellaneous/ad-hoc services which citizens avail from ULBs.

### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

* Can perform service-specific business logic without impacting the other module.
* In the future, if we want to expose the application to citizens then it can be done easily.

### Integration Steps <a href="#steps-to-integration" id="steps-to-integration"></a>

To integrate, the client service should send email requests to email notification consumer topics.

### Reference Documents

Play around with the API's : [DIGIT-Playground](https://digit-api.apidog.io/doc-507201)&#x20;
