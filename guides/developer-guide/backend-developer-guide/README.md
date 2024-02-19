---
description: DIGIT backend development guide
---

# Backend Developer Guide

This guide provides detailed steps for developers to create a new microservice on top of DIGIT. At the end of this guide, you will be able to run the [sample module](https://github.com/egovernments/DIGIT-OSS/tree/master/tutorials/backend-developer-guide/btr-services) provided with this guide (code provided), test it out locally and also deploy it using CI CD to your DIGIT environment.

This guide walks you through steps described below:

* How to set up your development environment
* How to develop the registries, services, and APIs  for a voter registration module that were described in the [Design Guide](../../design-guide/)
* How to integrate with an existing DIGIT environment and re-use a lot of the common services using Kubernetes port forwarding
* How to test the new module and debug
* How to build and deploy the new service in the DIGIT environment

The guide is divided into multiple sections for ease of use. Click on the section cards below to follow the development steps.

<table data-view="cards"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><a href="section-0-prep/"><mark style="color:blue;"><strong>Section 0: System Setup</strong></mark></a></td><td>Learn all about the development pre-requisites, design inputs, and environment setup</td><td></td></tr><tr><td><a href="section-1-create-project/"><mark style="color:blue;"><strong>Section 1: Create Project</strong></mark></a></td><td>The first step is to create and configure a spring boot project</td><td></td></tr><tr><td><a href="section-2-integrate-persister-and-kafka/"><mark style="color:blue;"><strong>Section 2: Integrate Persister Service</strong></mark></a></td><td>The next step is to integrate the Persister service and Kafka to enable read/write from the DB</td><td></td></tr><tr><td><a href="section-3-integrate-microservices/"><mark style="color:blue;"><strong>Section 3: Integrate with other DIGIT services</strong></mark></a></td><td>Steps on how to integrate with other key DIGIT services</td><td></td></tr><tr><td><a href="section-4-integrate-billing-and-payment/"><mark style="color:blue;"><strong>Section 4: Billing &#x26; Payment Integration</strong></mark></a></td><td>Learn how to integrate the billing and payment services to the module</td><td></td></tr><tr><td><a href="section-5-other-advanced-integrations/"><mark style="color:blue;"><strong>Section 5: Advanced Integrations</strong></mark></a></td><td>Learn how to integrate advanced services to the built module</td><td></td></tr><tr><td><a href="section-6-run-final-application.md"><mark style="color:blue;"><strong>Section 6: Run Application</strong></mark></a></td><td>Test run the built application in the local environment</td><td></td></tr><tr><td><a href="section-7-build-and-deploy-instructions.md"><mark style="color:blue;"><strong>Section 7: Build &#x26; Deploy Instructions</strong></mark></a></td><td>Deploy and run the modules</td><td></td></tr></tbody></table>

Access the sample module [here](https://github.com/egovernments/DIGIT-OSS/tree/master/tutorials/backend-developer-guide/btr-services). Download and run this in the local environment.



