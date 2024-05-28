---
description: Digital Infrastructure for Governance and Inclusive Transformation
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

**D**igital **I**nfrastructure for **G**overnance and **I**nclusive **T**ransformation (DIGIT) is an open-source, scalable, interoperable platform for responsive public service delivery and good governance.  It enables government agencies to digitize public service delivery  - providing unified interfaces for citizens, front-line employees and administrators to exchange information with each other in a seamless and trusted manner. DIGIT is an open-source platform built for scale. DIGIT is multi-tenant and can enable the digital transformation of multiple government agencies at speed and scale using a common shared infrastructure.&#x20;

<div align="left">

<img src=".gitbook/assets/image (253).png" alt="">

</div>

## Motivation

Government agencies deliver and manage a host of public services. Each of them are increasingly leveraging information technology to automate and manage delivery of these services. Inadvertently,  they endup building systems  have common functionality and also end up duplicating similar data sets that are all out of synch. This leads to several challenges in the long term.&#x20;

1. Lack of Single Source of Truth - Multiple systems with similar datasets leads to multiple sources of truth.&#x20;
2. Siloed - These systems often don't talk to each other hence citizens have to run pillar to post to get same data in multiple systems updated to receive services and benefits. Administrators also struggle to get access to data to identify areas of improvement. Employees have to learn to work with multiple systems to deliver services.
3. Scalability - Many of these systems are built for internal users and cannot be opened up for direct access to citizens. This makes it difficult for citizens to access their own data.&#x20;
4. Vendor Lock-In - Often these systems have been developed by external vendors and government agencies do not have capacity to take these over leading to vendor lock-in.&#x20;

<div align="left">

<img src=".gitbook/assets/image (192).png" alt="Traditional application oriented approach leads to siloes, wasteful duplication, non-scalable and difficult to integrate">

</div>

Multiple other challenges like security concerns and limited technical capabilities hinder the government's ability to effectively utilise technology for large-scale public service delivery.

DIGIT platform is developed using sound architectural principles to enable multiple government agencies to deliver public services is an inclusive and accessible to all citizens and business in at scale and speed. DIGIT provide a shared infrastructure consist of shared data registries and common services like authentication, authorisation, workflow, notification, payments etc. that enable agencies to develop and deliver services in a secure, scalable and cost effective manner.&#x20;

<figure><img src=".gitbook/assets/image (323).png" alt="" width="375"><figcaption></figcaption></figure>

Refer to the [DIGIT platform design principles](platform/principles/) page.

## Typical Public Service Design

A typical public service delivery starts with a citizen applying for a service or a service connection. The diagram below abstracts the typical information exchange flow required to enable the delivery of a service.

![](<.gitbook/assets/image (159).png>)

A digital system offers the following capabilities to improve citizen experience:

1. Register/Login - Citizens can register, sign in, or authenticate themselves. Single sign-on capability streamlines access to digital services.&#x20;
2. Apply/Upload - Citizens can request services by completing an application form and uploading necessary documents. Services should be accessible through multiple channels and in various languages.&#x20;
3. Pay/Bill - Citizens can make payments for services and download bills. Multiple payment options, including digital and cash, should be available..&#x20;
4. Inform/Track - Citizens can track service progress or receive updates via SMS, email, or app notifications.
5. Support/Feedback - Citizens can raise support requests or provide feedback on service closure. The system should allow configuring surveys and feedback forms, with the ability to analyse responses for corrective action.

The following capabilities support the employee and management experience:

1. Assign - Employees or vendors can assign service applications or trigger workflows tailored to different user/agency local requirements.
2. Search/View - Employees or vendors can search for and view applications based on multiple attributes.
3. Update/Comment - Employees can update and comment on service applications, facilitating structured and unstructured data exchange between parties.
4. Deliver/Verify- Employees or vendors can deliver services, such as setting up a new connection, or verify and certify information provided by citizens. Offline-capable apps are crucial in low mobile coverage areas, with data synchronization capabilities to handle load spikes.&#x20;
5. Monitor/Improve - Administrators can monitor service performance and identify areas for improvement. All transactions should generate data events in an analytical database for comprehensive performance monitoring.
6. Plan/Budget - Administrators and policymakers can plan and budget for service improvement, linking expenditures to outcomes.

## DIGIT Service Design

DIGIT offers a set of [building blocks](platform/core-services/) (i.e. services) that can leveraged to develop any [digital services ](./#typical-public-service)while adhering to the [key design principles](./#key-principles). Additionally, DIGIT provides optional accelerators like DIGIT UI and Dashboard Framework that can be extended to create citizen, employee and administrator dashboards.&#x20;

The diagram below illustrates how reusable building blocks interact to realise a typical public service delivery. Leveraging reusable building blocks not only speeds up delivery but also ensures well-structured digital services. The interactions between these services are detailed in the [Service Architecture](platform/architecture/service-architecture.md).&#x20;

![DIGIT Services](<.gitbook/assets/image (270).png>)

All services are built on DIGIT emits micro-level transactional data into an analytical database. This is key for real-time monitoring and auditing of the operations. It facilitates planning, budgeting and policy decision-making.&#x20;

DIGIT is proven and well-supported serving over 1000 cities. Ecosystem partners including System Integrators are using DIGIT to build and deliver services.  DIGIT Core LTS 2.9 version comes with long-term support. This implies that any technical issues like security or performance reported on any of these services in the DIGIT Core 2.9 LTS version will be fixed by the DIGIT team.&#x20;

DIGIT is easy to install, configure and use. To install DIGIT on your servers use the [DIGIT Installation Guide](get-started/installation-guide/). To design and develop a new service on the DIGIT Platform go through the [DIGIT Design Guide](get-started/design-guide/) and [DIGIT Developer Guide](get-started/developer-guide/).  You can also take up the DIGIT Certification through the [DIGIT Academy](https://app.gitbook.com/o/-MEQmzNGXk5ajuZujG7E/s/kI0HGCGboIe1ltcfV9XD/). &#x20;

If you want to experience DIGIT or develop on DIGIT, you can also access the DIGIT demo using [Sandbox](accelerators/sandbox.md).&#x20;

DIGIT comes with several accelerators. These include [UI frameworks](accelerators/ui-frameworks/) and [Integration Adapters](accelerators/integrations/). These are optional. You may choose to develop or reuse your UI framework and Integration Adapters.&#x20;

We organize several events for architects and developers on DIGIT. Keep a watch on the [Events](https://egov.org.in/events/) Page for upcoming events.&#x20;

Several volunteers are contributing to DIGIT in many ways. If you want to volunteer, check out our [contribute](accelerators/contribute.md) page.&#x20;

## Contact Us

{% embed url="https://egov.org.in/contact/" %}

