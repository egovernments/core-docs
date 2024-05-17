---
description: Microservice reusable building blocks architecture
---

# Service Architecture

DIGIT consists of several reusable building blocks on top of which one can develop a citizen service delivery solution. Read on to learn more about the microservice building blocks architecture.

## Microservice - Building Blocks

To develop a new service, one needs to create a microservice and make it available through the API gateway. The API gateway calls the [**User Service**](../core-services/user/) for authentication and the [**Access Service**](../core-services/access-control-services.md) for authorisation. The service developer can configure the roles and map the roles and actions using the [**Master Data Management Service**](../core-services/mdms-v2-master-data-management-service/mdms-master-data-management-service/).&#x20;

![DIGIT Services](<../../.gitbook/assets/image (311).png>)

[**Citizen Dashboard**](../../get-started/developer-guide/ui-developer-guide/citizen-module-setup/) - The service user interface can be developed as part of the Citizen Dashboard or can be an independent solution. The citizen can log in using a mobile number and OTP. They can apply for a new service using the service UI. The [**File Store Service**](../core-services/filestore-service.md) allows users to upload relevant documentation.&#x20;

The [**Persister Service**](../core-services/persister-service/) stores the submitted application asynchronously into the registry. The PII data is encrypted using the [**Encryption Service**](../core-services/encryption-service/) before storing. All changes are digitally signed and logged using the [**Signed Audit Service**](broken-reference) (ongoing).  The [**Indexer Service**](../core-services/indexer-service/) transforms and enriches the application data. The [**Indexer Service**](../core-services/indexer-service/) also strips the PII data and sends it to the [**Analytics Data Store(ElasticSearch)**](../../get-started/operations-guide/availability/backbone-services/elastic-search.md).&#x20;

The [**Dashboard Backend Service**](https://urban.digit.org/platform/configure-digit/services-overview/business-services/dashboard-analytics-backend) executes configured queries on the stripped data and makes the aggregated data available to the [**Dashboard Frontend**](../../get-started/operations-guide/availability/dss-dashboard.md) for the administrator or employee view. The views are in accordance with the user role access which is also configurable.&#x20;

The [**Billing Service**](https://urban.digit.org/platform/configure-digit/services-overview/business-services/billing-service) generates a demand based on the calculation logic for the given service delivery. Based on this demand, a bill is generated against which the payment has to be made. The citizen can either make an online payment or can pay at the counter (offline payment). The [**Payment Gateway Service**](../core-services/payment-gateway-service.md) is called for online payments and this is integrated with third-party service providers. The service routes the citizen to the service provider's website and then back to the citizen's UI once the payment is successful. &#x20;

The [**Collection service**](https://urban.digit.org/platform/configure-digit/services-overview/business-services/collection-service/collection-service-v2) is the payment registry and records all the successful payments. For offline payments, a record is made in the collection service after the collection of the Cash/Cheque/DD/RTGS. The allowed payment modes are configurable. The PDF service is used to generate receipts based on a configurable template.&#x20;

The service then triggers the [**Workflow Service**](../core-services/workflow/) to assign tasks for verification and approval. Workflows can be configured.  The **Employee Service** allows employee registrations and enables them to log in using the **Employee Dashboard**. The dashboard displays the list of pending applications as per the employee's role. The employee can perform actions on these applications using the employee UI for the service. &#x20;

As the status changes or actions are taken on the applications the relevant [**SMS and Email Notification Service** ](../core-services/sms-notification-service/)sends the updates to the applicant. Once the application is approved, the applicant can download the final certificate which is generated using [**PDF Service**](../core-services/pdf-generation-service.md). &#x20;

DIGIT has multi-tenant configuration capabilities. The [**Location Service**](../core-services/location.md) allows the configuration of the tenant hierarchy and maps multiple tenants like Country, State, District or State, Department, and Sub Department. Each tenant can have their own configurations for service, roles, workflows etc. This allows for variations across different agencies in tune with the local context.&#x20;

The [**Language Service**](../core-services/localization-service/) facilitates the support of multiple languages in DIGIT. This service stores the translations in multiple languages.



![End to End Citizen Flow](<../../.gitbook/assets/Citizen WSD.png>)

