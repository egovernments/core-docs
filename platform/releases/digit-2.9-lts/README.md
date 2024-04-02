# DIGIT 2.9 LTS

DIGIT 2.9 represents the most recent Long-Term Support (LTS) version, offering a stable and reliable foundation. This version emphasises enhanced security measures, improved system stability, streamlined deployment processes, simplified configuration, and comprehensive documentation. Periodic updates, encompassing both minor adjustments and significant enhancements, will be released as necessary. Support for this iteration of DIGIT will be available for the upcoming five years, with a clear migration guide available to facilitate the transition to subsequent LTS versions once the current support period concludes.

### Benefits of Long Term Support

1. **Extended Support:** LTS versions come with an extended period of support, which includes security updates, bug fixes, and sometimes even minor feature enhancements. This extended support period will last for 5 years, which means that users do not need to upgrade to newer versions frequently to receive critical updates.
2. **Stability:** The LTS release is typically more stable than regular releases because it undergoes more extensive testing and bug fixing. Compatibility: With the extended support period, the LTS release ensures better compatibility with third-party applications and hardware over time. Developers and vendors have a stable base to target, reducing the frequency of compatibility issues.
3. **Reduced Costs:** For businesses, the reduced need for frequent upgrades can translate into lower IT costs. Upgrading to a new version often involves significant effort in testing, deployment, and sometimes even hardware upgrades. LTS releases help spread these costs over a longer period.
4. **Predictability:** LTS release provides a predictable upgrade path, making it easier for organisations to plan their IT infrastructure, training, and budgets. Knowing the support timeline in advance helps in strategic planning and resource allocation.
5. **Focus on Core Features and Performance:** Since the LTS release is not focused on adding new features aggressively, the bulk of efforts are spent on optimising for performance and reliability. This focus benefits users who need a solid and efficient system rather than the latest features.
6. **Community and Vendor Support:** LTS releases will often have a larger user base, which means a more extensive community support network is available.

### What is new in LTS

* Infra/Backbone upgrade:\
  &#x20;\- Postgres upgrade   \
  &#x20;\- Kafka upgrade\
  &#x20;\- Redis upgrade\
  &#x20;\- Kubernetes upgrade\
  &#x20;\- Elasticsearch upgrade
* Use of helm file for deployment management
* Upgrade of core service dependencies
* Upgrade to DIGIT libraries
* Spring Cloud Gateway
* Test Automation script
* Single Click deployment using Github Actions

### New Services in LTS

* MDMS V2
* Workbench (MDMS UI)
* Boundary Service (Beta)

### New Functionalities

* Admin UI to configure Master Data
* Functionality to define schema and attribute validation for master data
* Maintain master data in the database&#x20;
* Hot reload of MDMS data&#x20;
* Configurable Rate limiting for services using helm&#x20;
* Deployment of DIGIT without any local tool setup/configuration (via browser)
* Ability to create and link boundary nodes using UI/APIs
* Geospatial queries like proximity search to locate boundary nodes

### **Summary of Technical Enhancements and Fixes:**

* Filestore Service: Fixed flow to store and retrieve files from Azure blob storage.
* PDF Service: Fixed bug where \_create API creates duplicate PDF for each request and fixed kafka message getting pushed on single partition.
* SMS Notification Service: Added API for sms bounce backtracking.
* Mail Notification Service: Added support for attachments.
* User OTP Service: Added support for sending OTP via email by emitting email events.
* User Service: Added fallback to default message if user email update localization messages are not configured.
* Workflow Service: Introduced state-level business service fallback as part of v2 business service search API.
* Dashboard Analytics: Introduced feature to perform DIVISION operation on metric chart responses.
* Location Service: Fixed bug where search on root level boundary type yields empty search response.
* Privacy Exemplar: Data privacy changes for masking/unmasking PII data were introduced as part of this exemplar.
* Encryption Client Library: As part of privacy changes, the enc-client library was introduced to support encryption-related functionalities.
* Codegen: Enhanced codegen utility to support open API 3.0 specifications.
* Persister: Enhanced persister to make it compatible with Signed Audit Service.
* Human Resource Management Service: Fixed bug where employee search causes server error in single instance clusters.
* DIGIT Developer Guide: Backend and Frontend guides along with a sample birth registration spring-boot module, citizen and employee React modules were developed as part of this guide.
* DIGIT Installer Enhancement: DIGIT Installer was simplified and detailed tutorial document was created for installing DIGIT services on AWS. (**Note:** Simplified DIGIT Installer has not been merged to master yet and is being released separately because many of our clusters are still running on legacy DevOps configurations)
* Upgraded all helm charts to support Kubernetes version upgrade from 1.20 to 1.28.

## Bug Fixes

<table><thead><tr><th width="122.33333333333331">S.no.</th><th>Service</th><th>Description of the fix</th></tr></thead><tbody><tr><td>1</td><td>PDF Service</td><td>Fixed bug where _create API creates duplicate PDF for each request.</td></tr><tr><td>2</td><td>PDF Service</td><td>Fixed issue where pdf service was pushing data to only one kafka topic partition</td></tr><tr><td>3</td><td>User Service</td><td>Fixed bug where updating citizen profile causes server error, fixed bug where employee details are updateable via citizen profile update API.</td></tr><tr><td>4</td><td>Location Service</td><td>Fixed bug where search on root level boundary type yields empty search response.</td></tr><tr><td>5</td><td>Human Resource Management Service</td><td>Fixed bug where employee search causes server error in single instance clusters.</td></tr></tbody></table>

## Document Resources & Links

| Enhanced Service Documents                                                                                          |
| ------------------------------------------------------------------------------------------------------------------- |
| [Filestore Service](https://core.digit.org/platform/core-services/filestore-service)                                |
| [PDF Service](https://core.digit.org/platform/core-services/pdf-generation-service)                                 |
| [Email Notification Service](https://core.digit.org/platform/core-services/email-notification-service)              |
| [User Service](https://core.digit.org/platform/core-services/user-services)                                         |
| [Workflow Service](https://core.digit.org/platform/core-services/workflow-service)                                  |
| [Location Service](https://core.digit.org/platform/core-services/location-services)                                 |
| [Access Control Service](https://core.digit.org/platform/core-services/access-control-services)                     |
| [Master Data Management Service](https://core.digit.org/platform/core-services/mdms-master-data-management-service) |
| [Payment Gateway Service](https://core.digit.org/platform/core-services/payment-gateway-service)                    |
| [Indexer Service](https://core.digit.org/platform/core-services/indexer-service)                                    |
| [URL Shortening Service](https://core.digit.org/platform/core-services/url-shortening-service)                      |
| [Persister Service](https://core.digit.org/platform/core-services/persister-service)                                |
| [Encryption Service](https://core.digit.org/platform/core-services/encryption-service)                              |
| [ID Generation Service](https://core.digit.org/platform/core-services/id-generation-service)                        |
| [Gateway Service](gateway-deployment-with-spring-cloud.md)                                                          |
| [User OTP Service](https://core.digit.org/platform/core-services/user-otp-service)                                  |
| [Audit Service](https://core.digit.org/platform/core-services/audit-service)                                        |
| [Service Request](https://core.digit.org/platform/core-services/service-request)                                    |

