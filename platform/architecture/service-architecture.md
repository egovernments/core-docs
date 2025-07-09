---
description: Microservice reusable building blocks architecture
---

# Service Architecture

DIGIT consists of several reusable building blocks on top of which one can develop a citizen service delivery solution. Read on to learn more about the microservice building blocks architecture.

## Microservice - Building Blocks

To develop a new service, one needs to create a microservice and make it available through the API gateway. The API gateway calls the [**User Service**](../core-services/user/) for authentication and the [**Access Service**](../core-services/access-control-services.md) for authorisation. The service developer can configure the roles and map the roles and actions using the [**Master Data Management Service**](../core-services/mdms-v2-master-data-management-service/mdms-master-data-management-service/).

![DIGIT Services](<../../.gitbook/assets/image (311).png>)

[**Citizen Dashboard**](../../get-started/developer-guide/ui-developer-guide/citizen-module-setup/) - The service user interface can be developed as part of the Citizen Dashboard or can be an independent solution. The citizen can log in using a mobile number and OTP. They can apply for a new service using the service UI. The [**File Store Service**](../core-services/filestore-service.md) allows users to upload relevant documentation.

The [**Persister Service**](../core-services/persister-service/) stores the submitted application asynchronously into the registry. The PII data is encrypted using the [**Encryption Service**](../core-services/encryption-service/) before storing. All changes are digitally signed and logged using the [**Signed Audit Service**](../../get-started/developer-guide/backend-developer-guide/section-2-integrate-persister-and-kafka/enable-signed-audit.md) (ongoing). The [**Indexer Service**](../core-services/indexer-service/) transforms and enriches the application data. The [**Indexer Service**](../core-services/indexer-service/) also strips the PII data and sends it to the [**Analytics Data Store(ElasticSearch)**](../../guides/operations-guide/availability/backbone-services/elastic-search/).

The [**Dashboard Backend Service**](https://urban.digit.org/platform/configure-digit/services-overview/business-services/dashboard-analytics-backend) executes configured queries on the stripped data and makes the aggregated data available to the [**Dashboard Frontend**](../../get-started/operations-guide/availability/dss-dashboard.md) for the administrator or employee view. The views are in accordance with the user role access which is also configurable.

The [**Billing Service**](https://urban.digit.org/platform/configure-digit/services-overview/business-services/billing-service) generates a demand based on the calculation logic for the given service delivery. Based on this demand, a bill is generated against which the payment has to be made. The citizen can either make an online payment or can pay at the counter (offline payment). The [**Payment Gateway Service**](../core-services/payment-gateway-service.md) is called for online payments and this is integrated with third-party service providers. The service routes the citizen to the service provider's website and then back to the citizen's UI once the payment is successful.

The [**Collection service**](https://urban.digit.org/platform/configure-digit/services-overview/business-services/collection-service/collection-service-v2) is the payment registry and records all the successful payments. For offline payments, a record is made in the collection service after the collection of the Cash/Cheque/DD/RTGS. The allowed payment modes are configurable. The PDF service is used to generate receipts based on a configurable template.

The service then triggers the [**Workflow Service**](../core-services/workflow/) to assign tasks for verification and approval. Workflows can be configured. The **Employee Service** allows employee registrations and enables them to log in using the **Employee Dashboard**. The dashboard displays the list of pending applications as per the employee's role. The employee can perform actions on these applications using the employee UI for the service.

As the status changes or actions are taken on the applications the relevant [**SMS and Email Notification Service** ](../core-services/sms-notification-service/)sends the updates to the applicant. Once the application is approved, the applicant can download the final certificate which is generated using [**PDF Service**](../core-services/pdf-generation-service.md).

DIGIT has multi-tenant configuration capabilities. The [**Location Service**](../core-services/location.md) allows the configuration of the tenant hierarchy and maps multiple tenants like Country, State, District or State, Department, and Sub Department. Each tenant can have their own configurations for service, roles, workflows etc. This allows for variations across different agencies in tune with the local context.

The [**Language Service**](../core-services/localization-service/) facilitates the support of multiple languages in DIGIT. This service stores the translations in multiple languages.

![End to End Citizen Flow](<../../.gitbook/assets/Citizen WSD.png>)

## Core Service & Kafka Topics Mapping Details

The table below provides the mapping of various core services to **Kafka topics** used in a DIGIT-based system.

#### 🔄 Workflow Topics

| Produced By      | Topic                     | Consumed By                                | Purpose                                  |
| ---------------- | ------------------------- | ------------------------------------------ | ---------------------------------------- |
| egov-workflow-v2 | save-wf-transitions       | egov-workflow-v2-persister.yml (persister) | Persists workflow transition events      |
| egov-workflow-v2 | save-wf-businessservice   | egov-workflow-v2-persister.yml             | Saves a workflow business service config |
| egov-workflow-v2 | update-wf-businessservice | egov-workflow-v2-persister.yml             | Updates an existing workflow service     |

***

#### 📝 Service Request Topics

| Produced By     | Topic                   | Consumed By                   | Purpose                         |
| --------------- | ----------------------- | ----------------------------- | ------------------------------- |
| service-request | save-service-definition | service-request-persister.yml | Save a new service definition   |
| service-request | save-service            | service-request-persister.yml | Save an actual service instance |

***

#### 📤 Data Uploader Topics

| Produced By        | Topic              | Consumed By                                        | Purpose                        |
| ------------------ | ------------------ | -------------------------------------------------- | ------------------------------ |
| egov-data-uploader | infra.data.upload  | DataUploadConsumer.java (egov-data-uploader)       | Triggers data upload           |
| egov-data-uploader | save-upload-jobs   | uploader-persister.yml, egov-uploader-indexer.yaml | Saves details of upload jobs   |
| egov-data-uploader | update-upload-jobs | uploader-persister.yml, egov-uploader-indexer.yaml | Updates upload job status/info |

***

#### 🧾 Audit Topics

| Produced By                   | Topic                 | Consumed By                 | Purpose              |
| ----------------------------- | --------------------- | --------------------------- | -------------------- |
| audit-service; egov-persister | audit-create          | audit-service-persister.yml | Logs audit records   |
| audit-service; egov-persister | process-audit-records |                             | Processes audit logs |
| egov-user; report             | audit\_data           |                             | Transfers audit data |

***

#### 📱 Notifications (SMS, Email)

| Produced By         | Topic                          | Consumed By | Purpose                  |
| ------------------- | ------------------------------ | ----------- | ------------------------ |
| egov-user; user-otp | egov.core.notification.sms     |             | Send SMS notifications   |
| egov-user; user-otp | egov.core.notification.email   |             | Send email notifications |
| user-otp            | egov.core.notification.sms.otp |             | Send OTP via SMS         |

#### 📊 National Dashboard Topics

| Produced By               | Topic              | Consumed By       | Purpose             |
| ------------------------- | ------------------ | ----------------- | ------------------- |
| national-dashboard-ingest | nss-ingest-keydata | nss-persister.yml | Ingest NSS key data |

***

#### 📦 MDMS Topics

| Produced By | Topic                       | Consumed By        | Purpose                 |
| ----------- | --------------------------- | ------------------ | ----------------------- |
| mdms-v2     | save-mdms-schema-definition | mdms-persister.yml | Save schema definitions |
| mdms-v2     | save-mdms-data              | mdms-persister.yml | Save MDMS data          |
| mdms-v2     | update-mdms-data            |                    | Update MDMS data        |

***

#### 🌐 Boundary Service Topics

| Produced By      | Topic                                | Consumed By | Purpose                               |
| ---------------- | ------------------------------------ | ----------- | ------------------------------------- |
| boundary-service | dss-collection                       |             | For DSS data collection               |
| boundary-service | service-consumer-topic               |             | Used by service consumers             |
| boundary-service | create-boundary-entity               |             | Create new boundary entities          |
| boundary-service | update-boundary-entity               |             | Update boundary entities              |
| boundary-service | save-boundary-hierarchy-definition   |             | Save boundary hierarchy definition    |
| boundary-service | update-boundary-hierarchy-definition |             | Update boundary hierarchy definition  |
| boundary-service | save-boundary-relationship           |             | Save relationships between boundaries |
| boundary-service | update-boundary-relationship         |             | Update boundary relationships         |

***

#### 👤 User Events

| Produced By     | Topic                     | Consumed By | Purpose                        |
| --------------- | ------------------------- | ----------- | ------------------------------ |
| egov-user-event | save-user-events          |             | Save new user events           |
| egov-user-event | update-user-events        |             | Update user events             |
| egov-user-event | user-events-lat           |             | Possibly used for LAT tracking |
| egov-user-event | persist-user-events-async |             | Async user event persistence   |
| egov-user-event | update-user-events-async  |             | Async user event update        |

***

#### 🔍 Indexer Topics

| Produced By  | Topic             | Consumed By | Purpose                   |
| ------------ | ----------------- | ----------- | ------------------------- |
| egov-indexer | save-index-jobs   |             | Save indexing job details |
| egov-indexer | update-index-jobs |             | Update indexing job info  |
| egov-indexer | save-service-db   |             | Save service DB entry     |
| egov-indexer | update-service-db |             | Update service DB entry   |

#### 🤖 Chatbot Topics

| Produced By | Topic                             | Consumed By             | Purpose                   |
| ----------- | --------------------------------- | ----------------------- | ------------------------- |
| chatbot     | chatbot-conversation-state-insert | chatbot.yml (persister) | Insert conversation state |

***

#### 🚪 Gateway Topics

| Produced By | Topic      | Consumed By | Purpose             |
| ----------- | ---------- | ----------- | ------------------- |
| gateway     | res-filter |             | For async filtering |

***
