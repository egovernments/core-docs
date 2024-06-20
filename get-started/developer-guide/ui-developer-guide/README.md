---
description: DIGIT UI development guide
---

# UI Developer Guide

After the backend development and deployment of DIGIT, as per the steps detailed in the [Backend Developer Guide](../backend-developer-guide/), it is time to start building the UI screens. For illustration purposes, we will build the citizen and employee screens for the Sample module.&#x20;

This guide offers a systematic view of creating the application screens on DIGIT.

**Developer code:** Download the UI code from the link here [Birth-Registration. ](https://github.com/egovernments/DIGIT-OSS/tree/master)

**Key fundamentals** to browse through before initiating the DIGIT UI development.

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><mark style="color:blue;"><strong>DIGIT UI Components</strong></mark></td><td>Learn all about the architecture and key features of the DIGIT UI</td><td></td><td><a href="digit-ui/">digit-ui</a></td></tr><tr><td><mark style="color:blue;"><strong>DIGIT UI Pre-requisites Checklist</strong></mark></td><td>Find the technical resources and knowledge required to develop a user interface on DIGIT</td><td></td><td><a href="digit-ui-development-pre-requisites.md">digit-ui-development-pre-requisites.md</a></td></tr><tr><td><mark style="color:blue;"><strong>DIGIT UI Predefined Screens</strong></mark></td><td>Find the details of the DIGIT predefined screens.</td><td></td><td><a href="../../../guides/developer-guide/ui-developer-guide/pre-defined-screens-in-digit-ui/">pre-defined-screens-in-digit-ui</a></td></tr></tbody></table>

**Steps to follow:** Follow the cards below to build and deploy the DIGIT UI.

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><mark style="color:blue;"><strong>UI Configuration</strong></mark></td><td>DIGIT UI configuration required to enable it in any environment</td><td></td><td><a href="ui-configuration-devops.md">ui-configuration-devops.md</a></td></tr><tr><td><mark style="color:blue;"><strong>Local Development Setup</strong></mark></td><td>Set up the UI development environment locally</td><td></td><td><a href="local-development-setup.md">local-development-setup.md</a></td></tr><tr><td><mark style="color:blue;"><strong>Run Front End App</strong></mark> </td><td>Run the front end application locally</td><td></td><td><a href="run-application.md">run-application.md</a></td></tr><tr><td><mark style="color:blue;"><strong>Build &#x26; Deploy</strong></mark></td><td>Deploy the DIGIT-UI module</td><td></td><td><a href="create-a-new-ui-module-package/">create-a-new-ui-module-package</a></td></tr></tbody></table>

### Steps For Specific UI Instances&#x20;

The steps listed below depend on specific user requirements. Follow the user-specific scenarios to learn the UI setup details.

* [Create a new UI module/package](create-a-new-ui-module-package/)
* [Setup employee module](employee-module-setup/)
* [Setup citizen module](citizen-module-setup/)
* [Customise UI](customisation/)
* [Setup monitoring tools ](setup-monitoring-tools.md)
* [Generate APK for Employee and Citizen apps](android-web-view-and-how-to-generate-apk.md)

[**Run Sample Module** ](https://github.com/egovernments/DIGIT-OSS/tree/master/municipal-services/birth-death-services)- Once the setup is complete, run the sample module provided in this guide. Test run the module and deploy it using CI/CD to your development environment.

Visit our FAQs section to troubleshoot -

* [Troubleshoot browser network tab issues](faqs/troubleshoot-using-browser-network-tab.md)
* [Debug Android app using Chrome browser](faqs/debug-android-app-using-chrome-browser.md)
