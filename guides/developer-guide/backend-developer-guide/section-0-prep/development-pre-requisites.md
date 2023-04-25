# Development Pre-requisites

## Checklists

Before beginning development on top of DIGIT make sure:&#x20;

* [x] DIGIT code from DIGIT-OSS, egov-mdms-data, configs etc.. has been forked from GitHub under your organization’s umbrella account.&#x20;
* [x] You have access to the forked repositories from your GitHub user account. Note that the user account is different from the organization's account.&#x20;
* [x] Access to a DIGIT environment - FQDN, Access keys etc..The DIGIT environment can be a single VM setup for a development environment. Please refer to these docs for the installation of DIGIT.&#x20;
* [x] Install DIGIT in a development environment (Single VM setup) by following the [quick setup guide](https://core.digit.org/guides/installation-guide/quick-setup).&#x20;

We recommend pointing the following services to the dev environment -&#x20;

* User
* MDMS
* Localization
* Id-Gen
* URL-shortener
* Workflow

Some of the above services can also be port forwarded using Kubernetes to bypass user auth.

The following DIGIT services should be running locally:

* Persister
* Indexer (optional)
* PDF Service

<!---->

* [x] CD/CI has been set up for DIGIT. This is a pre-requisite to deploying new DIGIT modules. CD/CI processes will be used to build and deploy the new module that will be developed.&#x20;
* [x] [Design phase artefacts](design-inputs/)
* [x] In addition, knowledge of the following technologies is required for developing on DIGIT:

<!---->

* Java/J2EE
* Spring Boot.
* REST APIs and related concepts like path parameters, headers, JSON etc.
* Git
* PostgreSQL
* Kafka
