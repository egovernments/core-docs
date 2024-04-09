---
description: An open source platform for service delivery and governance
cover: .gitbook/assets/Docs Website Banner 4 (1).png
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Overview

**DIGIT** is an open source platform to enable delivery and governance of public service. It enables seamless and unified exchange of information between citizens, employees & vendors, administrators and policymakers. It is built for scale. It is multi-tenant i.e multiple services delivered by multiple agencies can be developed on single instance of DIGIT.&#x20;

<div align="left">

<img src=".gitbook/assets/image (253).png" alt="">

</div>

## Motivation

Government agencies build applications to deliver and manage public services. However, they face several challenges especially in low and middle income countries.

**Inability to scale limits citizen access** - Many of these applications are not built to scale and cannot be opened up for direct access to systems.&#x20;

<div align="left">

<img src=".gitbook/assets/image (192).png" alt="Traditional application oriented approach leads to siloes, wasteful duplication, non-scalable and difficult to integrate">

</div>

**Data access impacts service delivery** - Most of these systems do not they have the ability to exchange data with other applications. Data gets locked in these siloed applications. The burden of coordinating between these agencies and keeping their data updated rests on the citizens. Multiple siloed systems also increases burden on the employees who have to remember multiple password and often copy data from one to another. Data from multiple systems are often poor quality and hard to correlate. This makes is impossible for Administrators to get unified view of the data which can help them monitor performance and identify areas of improvement.&#x20;

**Vendor Lock-In -** Many of these systems are proprietary and agencies are locked in with the vendor. This limits ability to evolve system independently as needs change.&#x20;

There are several other issues like security of data and inability to evolve the system due to system complexity. Poor systems in government limits access to data for citizens, employees and administrators. This impacts service delivery and governance.

Primary motivation of building DIGIT is to enable inclusive and accessible public services by making it easy for government agencies and partners to transform digital systems at speed and scale by adopting robust design principles.&#x20;

## Key Principles

DIGIT is designed based on the following principles&#x20;

1. **Security and Privacy** - DIGIT is designed to be secure by default, with configurable role based access. All PII is encrypted and no PII is emitted into analytical systems.&#x20;
2. **Single Source of Truth** - Shared Data Registries ensures data is kept up to date and reused without creating multiple copies of transactional data. This is key for good governance and service delivery.&#x20;
3. **Flexible** - DIGIT is designed to enable each tenant to configure their own master data, workflows and if required their build and deploy their own version of the service even on a shared infrastructure.&#x20;
4. &#x20;**Modular** - All DIGIT components are modular microservices with well defined APIs. All services can be scaled, evolved and deployed independent of each other.&#x20;
5. **Interoperable** - API first design and uses of Open Standards wherever possible ensure DIGIT is interoperable with other systems. Data can be exchanged seamlessly as and when required.
6. **Ease of Use** - DIGIT is designed keep in mind ease of access of all actors - citizens, employees, administrators as well as developers, system administrator etc. All data is available through API which can be used to channel specific applications - web, mobile, chat etc.&#x20;
7. **Open** - DIGIT is open source, uses all open source technologies and standards to ensure that data and core services are never vendor locked-in.&#x20;

## Typical Public Service

A typical public service delivery starts with a citizen applying for a service or a service connection. The diagram below abstracts the typical information exchange flow that needs to be enabled between the various actors to deliver service.

![](<.gitbook/assets/image (159).png>)

A digital service must provide the following capabilities to enable effective citizen service.&#x20;

1. Register/Login - Ability for the citizens to register or sign in or identify themselves.
2. Apply/Upload - Ability for the citizens to request services by filling out an application form and uploading a set of valid documents.
3. Pay/Bill - Ability for the citizens to pay for the service and be able to download a bill for the payment made.
4. Inform/Track - Ability for the citizen to track or receive updates about the applied services.
5. Assign - Ability for the employees or vendors to assign the service application or trigger a workflow that would assign it to an employee or a vendor.
6. Search/View - Ability for the employees or vendors to search and view the application.
7. Update/Comment - Ability for the employees to update and comment on the service application.&#x20;
8. Deliver/Verify- Ability for the employees or vendors to deliver the service e.g. set up a new water connection or verify/certify the information provided such as verifying economic status.
9. Support/Feedback - Ability for citizens to raise support requests in case of an exception or provided feedback in case of closure of the service request.
10. Monitor/Improve - Ability for the administrators to monitor service performance and identify areas of improvement.
11. Plan/Budget - Ability for administrators and policymakers to plan and budget continuous improvement of services.&#x20;

To build a digital system that adheres to the above key principles, DIGIT provides a set of  building blocks which a developer can leverage. DIGIT also provides optional accelerators like DIGIT UI and Dashboard Framework that can be extended to develop citizen, employee and administrator dashboards. The diagram below illustrates how some of the reusable building blocks interact to realize a typical public service delivery. The interactions between these services have been detailed out in the [Service Architecture](platform/architecture/service-architecture.md).&#x20;

![DIGIT Services](<.gitbook/assets/image (270).png>)

DIGIT is already being used to deliver services in 1000+ cities. Ecosystem partners including System Integrators are using DIGIT to build and deliver services.&#x20;

DIGIT is easy to install, configure and use. To install DIGIT on your servers use the [DIGIT Installation Guide](get-started/installation-guide/). To design and develop a new service on DIGIT Platform go through the [DIGIT Design Guide](get-started/design-guide/) and [DIGIT Developer Guide](get-started/developer-guide/).  You can also take up the DIGIT Certification through the [DIGIT Academy](https://app.gitbook.com/o/-MEQmzNGXk5ajuZujG7E/s/kI0HGCGboIe1ltcfV9XD/). &#x20;

If you want to experience DIGIT or develop on DIGIT, you can also access DIGIT demo using [Sandbox](platform/get-started/access.md).&#x20;

DIGIT comes with several accelerators. These include [UI frameworks](accelerator/ui-frameworks.md) and [Integration Adapters](platform/integrations/). These are optional. You may choose to develop or reuse your own UI framework and Integration Adapters.&#x20;

We organize several events for architects and developers on DIGIT. Keep a watch on the [Events](https://egov.org.in/events/) Page for upcoming events.&#x20;

Several volunteers are contributing to DIGIT in many ways. If you want to volunteer, check out our [contribute](platform/contribute.md) page.&#x20;

## Contact Us

{% embed url="https://egov.org.in/contact/" %}

