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

