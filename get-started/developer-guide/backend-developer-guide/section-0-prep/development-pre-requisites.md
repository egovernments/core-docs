# Development Pre-requisites

## Checklist

Before starting development on top of DIGIT make sure:&#x20;

* [x] To check out the [Development Pre-requisites Training Resources ](../../pre-requisites-training-resources.md#backend-pre-requisites-tutorials)page to learn how to deploy the required tools.
* [x] DIGIT code from DIGIT-OSS, egov-mdms-data, configs etc.. has been forked from GitHub under your organization’s umbrella account.&#x20;
* [x] You have access to the forked repositories from your GitHub user account. Note that the user account is different from the organization's account.&#x20;
* [x] Access a DIGIT environment - FQDN, Access keys etc..The DIGIT environment can be a single VM setup for a development environment. Please refer to these docs for the installation of DIGIT.&#x20;
* [x] Install DIGIT in a development environment (Single VM setup) by following the [quick setup guide](https://core.digit.org/guides/installation-guide/quick-setup).&#x20;
* [x] It is recommended to deploy the following services in the development environment -
  * [User](../../../../platform/core-services/user/)
  * [MDMS](../../../../platform/core-services/mdms-master-data-management-service/)
  * [Localization](../../../../platform/core-services/location.md)
  * [Id-Gen](../../../../platform/core-services/id-generation-service.md)
  * [URL-shortener](../../../../platform/core-services/url-shortening-service.md)
  * [Workflow](../../../../platform/core-services/workflow/)

Some of the above services can also be port-forwarded using Kubernetes to bypass user authentication.

* [x] Make sure the following DIGIT services are running in the local environment:
  * [Persister](../../../../platform/core-services/persister-service/)
  * [Indexer ](../../../../platform/core-services/indexer-service/)(optional)
  * [PDF Service](../../../../platform/core-services/pdf-generation-service.md)
* [x] [CD/CI](broken-reference) has been set up for DIGIT. This is a pre-requisite to deploying new DIGIT modules. CD/CI processes will be used to build and deploy the new module that will be developed.&#x20;
* [x] [Design phase artefacts](design-inputs/)
* [x] In addition, knowledge of the following technologies is required for developing on DIGIT: (Refer to the [DIGIT Pre-requisites tutorials](development-pre-requisites.md#digit-pre-requisites-tutorials) for help with installing and deploying these tools)
  * Java/J2EE
  * Spring Boot
  * REST APIs and related concepts like path parameters, headers, JSON etc.
  * Git
  * PostgreSQL
  * Kafka
