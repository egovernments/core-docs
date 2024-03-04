# Implement Kafka Producer & Consumer

## Overview

Follow the steps detailed below to implement [Kafka Producer](implement-kafka-producer-and-consumer.md#producer) & [Consumer](implement-kafka-producer-and-consumer.md#consumer).

## Producer

Producer classes help in pushing data from the application to Kafka topics.  DIGIT has a custom implementation of KafkaTemplate class in the tracer library called CustomKafkaTemplate. This implementation of the Producer class does not change across services of DIGIT.&#x20;

### **Steps**

1.  Access the producer implementation details here - [Producer Implementation. ](https://github.com/egovernments/DIGIT-Dev/blob/master/municipal-services/pgr-services/src/main/java/org/egov/pgr/producer/Producer.java)

    The Codegen jar already has created a Producer class. We will continue using it.&#x20;
2. Make sure the `tracer` dependency version in the `pom.xml` is 2.0.0-SNAPSHOT.&#x20;

## Consumer

For our guide, we will be implementing a notification consumer in the following section.

Once an application is created/requested or progresses further in the workflow, notifications can be triggered as each of these events is pushed onto Kafka topics which can be listened to and an sms/email/in-app notification can be sent to the concerned user(s).

For our guide, we will be implementing a notification consumer which will listen to the topic on which birth registration applications are created. Create a customised message and send it to the notification service (sms/email) to trigger notifications to the concerned users.&#x20;

{% hint style="info" %}
**Sending SMS notifications to the customer:**

Once an application is created/updated the data is pushed on Kafka topic. We trigger notifications by consuming data from this topic. Whenever any message is consumed the service will call the localisation service to fetch the SMS template. It will then replace the placeholders in the SMS template with the values in the message it consumed.&#x20;

(For example, It will replace the {NAME} placeholder with the owner name from the data consumed). Once the SMS text is ready, the service pushes this data on the notification topic. SMS service consumes data from notification topic and triggers SMS.
{% endhint %}

### **Steps**&#x20;

1. Open `Kafka/NotificationConsumer.java` and paste the following code:

{% code lineNumbers="true" %}
```java
package digit.kafka;

import com.fasterxml.jackson.databind.ObjectMapper;
import digit.service.NotificationService;
import digit.web.models.BirthRegistrationRequest;
import lombok.extern.slf4j.Slf4j;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.kafka.annotation.KafkaListener;
import org.springframework.kafka.support.KafkaHeaders;
import org.springframework.messaging.handler.annotation.Header;
import org.springframework.stereotype.Component;

import java.util.HashMap;

@Component
@Slf4j
public class NotificationConsumer {

    @Autowired
    private ObjectMapper mapper;

    @Autowired
    private NotificationService notificationService;

    @KafkaListener(topics = {"${egov.bt.registration.create.topic}"})
    public void listen(final HashMap<String, Object> record, @Header(KafkaHeaders.RECEIVED_TOPIC) String topic) {

        try {

            BirthRegistrationRequest request = mapper.convertValue(record, BirthRegistrationRequest.class);
            //log.info(request.toString());
            notificationService.prepareEventAndSend(request);

        } catch (final Exception e) {

            log.error("Error while listening to value: " + record + " on topic: " + topic + ": ", e);
        }
    }

}

```
{% endcode %}

2. Create a POJO by the name of SMSRequest in the `web.models` package and add the following content to it:

{% code lineNumbers="true" %}
```java
package digit.web.models;

import lombok.*;

@Getter
@AllArgsConstructor
@NoArgsConstructor
@Builder
@ToString
public class SMSRequest {
    private String mobileNumber;
    private String message;
}

```
{% endcode %}

3.  Create a class by the name of `NotificationService` under `service` folder to handle preparation of customised messages and pushing the notifications.&#x20;

    Add the following content to it -

{% code lineNumbers="true" %}
```java
package digit.service;

import digit.config.BTRConfiguration;
import digit.kafka.Producer;
import digit.web.models.BirthRegistrationApplication;
import digit.web.models.BirthRegistrationRequest;
import digit.web.models.SMSRequest;
import lombok.extern.slf4j.Slf4j;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.web.client.RestTemplate;

import java.util.ArrayList;
import java.util.List;
@Slf4j
@Service
public class NotificationService {

    @Autowired
    private Producer producer;

    @Autowired
    private BTRConfiguration config;

    @Autowired
    private RestTemplate restTemplate;

    private static final String smsTemplate = "Dear {FATHER_NAME} and {MOTHER_NAME} your birth registration application has been successfully created on the system with application number - {APPNUMBER}.";

    public void prepareEventAndSend(BirthRegistrationRequest request){
        List<SMSRequest> smsRequestList = new ArrayList<>();
        request.getBirthRegistrationApplications().forEach(application -> {
            SMSRequest smsRequestForFather = SMSRequest.builder().mobileNumber(application.getFatherMobileNumber()).message(getCustomMessage(smsTemplate, application)).build();
            SMSRequest smsRequestForMother = SMSRequest.builder().mobileNumber(application.getMotherMobileNumber()).message(getCustomMessage(smsTemplate, application)).build();
            smsRequestList.add(smsRequestForFather);
            smsRequestList.add(smsRequestForMother);
        });
        for (SMSRequest smsRequest : smsRequestList) {
            producer.push(config.getSmsNotificationTopic(), smsRequest);
            log.info("Messages: " + smsRequest.getMessage());
        }
    }

    private String getCustomMessage(String template, BirthRegistrationApplication application) {
        template = template.replace("{APPNUMBER}", application.getApplicationNumber());
        template = template.replace("{FATHER_NAME}", application.getFather().getName());
        template = template.replace("{MOTHER_NAME}", application.getMother().getName());
        return template;
    }

}
```
{% endcode %}

