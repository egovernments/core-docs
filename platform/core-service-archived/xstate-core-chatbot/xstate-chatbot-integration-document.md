# XState-Chatbot Integration Document

## Overview <a href="#overview" id="overview"></a>

The [XState-Chatbot](https://github.com/egovernments/core-services/tree/xstate-chatbot/xstate-chatbot) is a revamped version of the [chatbot](https://github.com/egovernments/core-services/tree/master/chatbot), which provides functionality to the user to access PGR module services like filing complaints, tracking complaints and notifications from WhatsApp. It allows the user to view receipts and pay bills for Property, Trade Licence, Fire NOC, Water and Sewerage and BPA service module.

## Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

* File PGR complaint
* Track PGR complaint
* Support images when filing complaints
* Notifications to citizens when an employee performs any action on the complaint
* Allow users to search and pay bills of different modules.
* Allow users to search and view receipts of different modules.
* Allow users to change the language of their choice to have a better experience.
* Put user interactions on an elastic search for telemetry.

## Integration Details <a href="#integration" id="integration"></a>

### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

The XState chatbot can be integrated with any other module to improve the ease of searching and viewing bills/past payment receipts and to improve speed and convenience for bill payments. It can be integrated with the PGR module for easiness of creation and tracking of the complaint.

### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

* Increase in convenience and ease of making the bill payment.
* Increase in no. of users opting for online payment.
* Improvement in demand collection efficiency
* Creating an additional channel for payment.
* Remove dependency on mobile/web apps or counter.

## Integration Approach <a href="#integration-details" id="integration-details"></a>

**Integration of New Whatsapp Provider**

Whatsapp provider is a third-party service that acts as an intermediary between the user WhatsApp client and the XState-Chatbot server. All messages coming/going to/from the user pass through the WhatsApp provider. The chatbot calls the WhatsApp provider to send messages to the user. When a user responds to any WhatsApp message the WhatsApp provider calls the Chatbot service configured endpoint with details like messages sent by the user, the sender number etc.

If any new WhatsApp provider is to be used with a chatbot, code must be written to convert the provider’s incoming messages to the format that the chatbot understands. The final output from the chatbot is also converted to the WhatsApp provider’s API request format.

Currently, the XState-Chatbot service is using ValueFirst as the WhatsApp Provider. This will require provider-specific environment variables to be configured. If the provider changes then, all these environment variables will also change. A few of those environment variables are stored as secrets, so these values need to be configured in _env_-secrets.yaml.

As this is a revamped version of the chatbot service, all of the secrets should already be present. There is no need to create new secrets.

#### Integration of PGR complaint feature in XState-Chatbot <a href="#integration-of-pgr-complaint-feature-in-xstate-chatbot" id="integration-of-pgr-complaint-feature-in-xstate-chatbot"></a>

The integration of PGR with a chatbot can be enabled and disabled by making changes in this [file](https://github.com/egovernments/core-services/blob/xstate-chatbot/xstate-chatbot/nodejs/src/machine/service/service-loader.js).\
By exporting the respective PGR service file, the PGR service feature can be sable and vice versa.

## Configuration Details

**Configuration of PGR version in chatbot**

To configure the PGR module to use in Xstate-chatbot - the below variable values need to change in the [environment file](https://github.com/egovernments/eGov-infraOps/blob/master/helm/environments/qa.yaml#L207) as per the requirement.

* pgrVersion
* pgrUpdateTopic

To configure PGR v2 in XState chatbot then pgrVersion should be ‘v2' and pgrUpdateTopic should be 'update-pgr-request’.

**Adding Information Images in PGR Complaint Creation and Open Search Information Image**

To configure the filestoreid for an informational image follow the steps mentioned below

1. Download the images from the section _**Information Images for PGR and Open Search**_
2. Upload the image into the filestore server. Use the upload file API from the Postman collection [here](https://www.getpostman.com/collections/bdb059c5af698f0d81d6).&#x20;
3. For the PGR information image mention the filestore id [here](https://github.com/egovernments/DIGIT-DevOps/blob/master/deploy-as-code/helm/environments/qa.yaml#L219) in the environment file.
4. For open search, the information image mentions the filestore id [here](https://github.com/egovernments/DIGIT-DevOps/blob/master/deploy-as-code/helm/environments/qa.yaml#L220) in the environment file.

**For example:**

a) if supportedLocales: process.env.SUPPORTED\_LOCALES || 'en\_IN,hi\_IN' then valuefirst-notification-resolved-templateid: "12345,6789"

b) if supportedLocales: process.env.SUPPORTED\_LOCALES || 'hi\_IN,en\_IN' then valuefirst-notification-resolved-templateid: "6789,12345"

_(Note: Both lists should not be empty - they must contain at least one element)_

#### **Configuration of push notification template messages** with a button <a href="#hardbreak-configuration-of-push-notification-template-messages-with-button" id="hardbreak-configuration-of-push-notification-template-messages-with-button"></a>

Template messages with buttons are maintained in the same way as described in the previous section (**Configuration of push notification template messages**)

There are two types of button message

* Quick Reply
* Call To Action

The Value First document below provides more details.&#x20;

{% embed url="https://713524410-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FX13sH0e4xi7bV1juDmGX%2Fuploads%2Ft9QHUELEFrg4Uk9oq6Db%2Fuserguide-valuefirst-whatsapp-v1.0.4-190421-1-.pdf?alt=media&token=636510fe-0240-455c-b085-06b849822f32" %}
Value First Whatsapp User Guide
{% endembed %}

#### Integration of Bill Payment and Receipt Search feature in Xstate-Chatbot <a href="#integration-of-bill-payment-and-receipt-search-feature-in-xstate-chatbot" id="integration-of-bill-payment-and-receipt-search-feature-in-xstate-chatbot"></a>

The integration of the Bill payment and receipt search feature with the chatbot is enabled and disabled by making changes in this [file](https://github.com/egovernments/core-services/blob/develop/xstate-chatbot/nodejs/src/machine/service/service-loader.js). The payment and receipt search feature can be enabled and vice versa by exporting the respective bill service and receipt service file.

**Configuration of module for Bill payment and Receipt search**

To configure the list of modules to appear as an option for payment and receipt, Add the module business service code to the list present in the [environment](https://github.com/egovernments/DIGIT-DevOps/blob/master/deploy-as-code/helm/environments/qa.yaml#L216) file.

**For example:**\
If the application modules are defined in the variable - `bill-supported-modules: "WS, PT, TL" -`the defined modules appear in the bill payment and receipt search. In the given example,  the modules Water and Sewerage, Property Tax, and Trade License appear for bill payment and receipt search.

Add the message bundle, validation and service code for the locality searcher in [egov-bill](https://github.com/egovernments/core-services/blob/develop/xstate-chatbot/nodejs/src/machine/service/egov-bill.js) and [egov-receipt](https://github.com/egovernments/core-services/blob/develop/xstate-chatbot/nodejs/src/machine/service/egov-receipts.js) files.

<table><thead><tr><th width="288">Environmental Variables</th><th>Description</th></tr></thead><tbody><tr><td><code>WHATSAPP_BUSINESS_NUMBER</code></td><td>The mobile number to be used on server</td></tr><tr><td><code>VALUEFIRST_USERNAME</code></td><td>Username for configured number for sending messages to user through whatsapp provider API calls</td></tr><tr><td><code>VALUEFIRST_PASSWORD</code></td><td>Password for configured number for sending messages to user through whatsapp provider API calls</td></tr><tr><td><code>GOOGLE_MAPS_API_KEY</code></td><td>Maps API key to access geocoding feature</td></tr><tr><td><code>ROOT_TENANTID</code></td><td>Contains state level tenantid value</td></tr><tr><td><code>SUPPORTED_LOCALES</code></td><td>This variable contains the list supported language in chatbot. If there is a need to add new language in chatbot, then its respective locale need to add in this list.</td></tr><tr><td><code>PGR_VERSION</code></td><td>Contains PGR version value to use (i.e v1 or v2)</td></tr><tr><td><code>PGR_UPDATE_TOPIC</code></td><td>Depends on PGR version respective PGR update kafka topic name should mention here. Example: If <code>PGR_VERSION: 'v2'</code> then <code>PGR_UPDATE_TOPIC: 'update-pgr-request'</code></td></tr><tr><td><code>BILL_SEARCH_LIMIT</code></td><td>Limit for showing maximum number of bills on search.</td></tr><tr><td><code>RECEIPT_SEARCH_LIMIT</code></td><td>Limit for showing maximum number of receipts on search.</td></tr><tr><td><code>COMPLAINT_SEARCH_LIMIT</code></td><td>Limit for showing maximum number of complaints on search.</td></tr><tr><td><code>BILL_SUPPORTED_MODULES</code></td><td>Contains the list of modules to be use for bill payment and receipts search.</td></tr><tr><td><code>INFORMATION_IMAGE_FILESTORE_ID</code></td><td>Contains the filestoreid of informational image, which shows how to share the user current location.</td></tr><tr><td><code>OPEN_SEARCH_IMAGE_FILESTORE_ID</code></td><td>Contains the filestoreid of open search informational image, which shows how to use open search pay feature for bill payment</td></tr><tr><td><code>USER_SERVICE_HARDCODED_PASSWORD</code></td><td>This variable contain fixed value of login password and otp. This value has to configured in <em>env</em>-secrets.yaml.</td></tr><tr><td><code>GEO_SEARCH</code></td><td>Boolean flag to enable and disable city / locality nlp search</td></tr></tbody></table>

**Configuration of Telemetry File**

Add this [telemetry file](https://github.com/egovernments/configs/pull/629/files) in the [config repo](https://github.com/egovernments/configs/tree/DEV/egov-indexer) and mention the filename in the respective [environment yaml file](https://github.com/egovernments/DIGIT-DevOps/blob/master/deploy-as-code/helm/environments/qa.yaml#L263).

#### **Searcher config file:** <a href="#hardbreak-searcher-config-file" id="hardbreak-searcher-config-file"></a>

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/localitySearcher.yml at qa · egovernments/configs](https://github.com/egovernments/configs/blob/qa/egov-searcher/localitySearcher.yml)

**Cron job mdms entry:**

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">RAIN-2768 Added entry in cron job api config file · egovernments/egov-mdms-data@30881ab](https://github.com/egovernments/egov-mdms-data/commit/30881ab4f759c8b607417be2047b46865ec953ef)

#### **Localisation for PGR service** <a href="#hardbreak-localisation-for-pgr-service-hardbreak" id="hardbreak-localisation-for-pgr-service-hardbreak"></a>

Information images for PGR and Open Search

![](<../../../.gitbook/assets/image (276).png>)![](<../../../.gitbook/assets/image (8) (1).png>)

## Reference Docs

### Doc Links <a href="#doc-links" id="doc-links"></a>

| Title                                                                  |
| ---------------------------------------------------------------------- |
| [Chatbot Message Localisation](xstate-chatbot-message-localisation.md) |
| [NLP-search Engine](../nlp-engine-service/)                            |

### API List

| Title                                                                                   |
| --------------------------------------------------------------------------------------- |
| [/xstate-chatbot/message](https://www.getpostman.com/collections/57615217a846330672c6)  |
| [/xstate-chatbot/reminder](https://www.getpostman.com/collections/47c10d1bc82a7133c269) |
| [/xstate-chatbot/status](https://www.getpostman.com/collections/47c10d1bc82a7133c269)   |

{% file src="../../../.gitbook/assets/eGov-WhatsApp Template (14th July 2021).xlsx" %}
