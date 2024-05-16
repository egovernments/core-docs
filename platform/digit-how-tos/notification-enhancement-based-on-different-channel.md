# Notification Enhancement Based On Different Channel

## Overview

Configuration of the notification messages for a business service based on the channel for the same event.

## **Key Functionalities** <a href="#key-functionalities" id="key-functionalities"></a>

* For a specific action of the user, he/she will get an SMS and email as an acknowledgement.
* Users can get SMS, Event, and email based on different channels.
* The application allows one to either send different messages across all channels based on their actions.

## **Configuration Details** <a href="#details-of-enhancement" id="details-of-enhancement"></a>

* To have this functionality for different business services, a channel names file was created and added to the MDMS data.&#x20;
* It contains information about the combination of different actions and channels for a particular business service. Example below:

{% code lineNumbers="true" %}
```json
 "channelList": [
 {   "businessService": "PT.CREATE",
     "module": "PT",
     "action" : "OPEN",
     "channelNames": ["SMS", "EMAIL", "EVENT"]
 },
 {
      "businessService": "BPA.CREATE",
      "module": "BPA",
      "action" : "SENDBACKTOCITIZEN",
      "channelNames": ["SMS", "EMAIL", "EVENT"]
  },
  {
      "businessService": "NewTL",
      "module": "TL",
      "action": "FORWARD",
      "channelNames": ["SMS", "EMAIL", "EVENT"]
  },
  {
      "businessService": "WS.CREATE",
      "module": "WS",
      "action" : "ACTIVATE_CONNECTION",
      "channelNames": ["SMS", "EMAIL", "EVENT"]
  },
   {
      "businessService": "SW.CREATE",
      "module": "SW",
      "action" : "APPROVE_CONNECTION",
      "channelNames": ["SMS", "EMAIL", "EVENT"]
    }
]
```
{% endcode %}

* The different channels are
  * SMS: ID (Mobile Number)
  * Event&#x20;
  * Email: ID (Email ID)
* This feature enables the functionality that checks for the channels present in the file and sends the notifications accordingly.&#x20;
* For the SMS event, it would send the SMS notification and log “Sending SMS Notification” for the Event it would log, “Event Notification Sent”, and for Email, it would log, “Email Notification Sent”.

### **Steps To Enable/Disable Channels** <a href="#steps-for-enabling-disabling-channels-for-a-particular-business-service" id="steps-for-enabling-disabling-channels-for-a-particular-business-service"></a>

To add/delete any particular channel for a business service -

* Update channelNames array in the [Channel List](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/Channel/channelList.json) file and add/delete the channel you want a business service’s action to have.
* Restart egov-mdms-service to apply the changes.
* Configure your business service - follow the steps mentioned below.

### **Configure Business Service** <a href="#configuration-for-a-particular-business-service" id="configuration-for-a-particular-business-service"></a>

* Adding details about the particular action and the channels you want that action to trigger in the [Channel List](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/Channel/channelList.json) file in egov-mdms-data repository.
* For any record that comes into the topic first, the service should fetch all the required data like user name, property id, mobile number, tenant id, etc from the record that we fetched from the topic.
* Respected localization templates should be upserted before in the required environment using the [localization service](https://digit-discuss.atlassian.net/wiki/spaces/DOPS/pages/1798012942). Restart the localization service to have the newly updated templates available.
* Then we should fetch the message content from localization and the service replaces the placeholders with the actual data.
* Then put the record in whichever channel’s Kafka topic that the sms, event or email service is listening to.
* Then the respective channel services (sms, event, email) will send out the notifications.

