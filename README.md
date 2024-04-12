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

**D**igital **I**nfrastructure for **G**overnance and **I**nclusive **T**ransformation (DIGIT) is an open-source, scalable, interoperable platform for responsive public service delivery and good governance.  It enables governments to digitize public service delivery with intuitive interfaces for citizens, front-line employees and administrators. DIGIT enables a seamless and unified exchange of information between citizens, employees & vendors, administrators and policymakers. DIGIT is an open-source platform built for scale. It enables the digital transformation of multiple government departments and is highly flexible enabling it to serve a variety of needs.&#x20;

<div align="left">

<img src=".gitbook/assets/image (253).png" alt="">

</div>

## Motivation

Government bodies deliver and manage a host of public services. Technology is the enabler in providing the infrastructure for seamless management and governance. The key challenge here is the several limitations (listed below) facing the effective adoption and implementation of technology, especially in low and middle-income countries.&#x20;

**Multiple Similar Systems -** In a federated government structure, multiple agencies operate at national, regional, and local levels, each implementing its custom-built systems. The system architecture is often hard-wired to support specific requirements of individual ministries, departments and agencies for distinct sectors. These systems, though similar, cannot be reused in case the policies change in future.

**Scalability Issues** - Most of these applications are not scalable in terms of meeting the evolving demands of a growing population or achieving streamlined governance objectives. The scope of localised systems is limited to specific goals that often include data collection or coordination between stakeholders. This restricts the scope for promoting ease of service delivery.&#x20;

<div align="left">

<img src=".gitbook/assets/image (192).png" alt="Traditional application oriented approach leads to siloes, wasteful duplication, non-scalable and difficult to integrate">

</div>

**Data Fragmentation** - Most of these systems do not they have the ability to exchange data with other applications. Data gets locked in these siloed applications. The burden of keeping the data updated rests on the citizens. Multiple siloed systems also increases burden on the employees who have to remember multiple password and often copy data from one application to another. Data from multiple systems are often poor quality and hard to correlate. This makes is impossible for Administrators to get unified view of the data which can help them monitor performance and identify areas of improvement.&#x20;

**Vendor Lock-In -** Many of these systems are proprietary and government agencies are locked in with the vendor. This limits the ability of agencies to evolve system to meet evolving needs.

There and several other issues like security and limited technology capacity impedes the ability of governments to leverage technology for public service delivery at scale.

Technology is designed properly can make public service delivery inclusive and accessible by all citizens. DIGIT is a set of reusable building blocks built using robust design principles and can accelerate digital transformation of public service delivery systems.&#x20;

## Key Principles

DIGIT is designed based on the following principles&#x20;

1. **Single Source of Truth** - Shared Data Registries ensures data is kept up to date and reused without creating multiple copies of transactional data. DIGIT registries are accessible through standard APIs and can be leveraged by multiple service providers.&#x20;
2. **Security and Privacy** - DIGIT is designed to be secure by default, with configurable role based access. All PII is encrypted and no PII is emitted into analytical systems.&#x20;
3. **Flexible** - DIGIT is designed to enable each tenant (agency or service provider) to configure their own master data, workflows and if required they can build and deploy their own version of the service even on a shared infrastructure e.g. if an tenant (agency) wants to build a different service charge calculator instead of reusing a generic one, they can do so.&#x20;
4. &#x20;**Modular** - All DIGIT components are modular microservices with well defined APIs. All services can be scaled, evolved and deployed independent of each other.&#x20;
5. **Interoperable** - API first design and use of Open Standards wherever possible ensures DIGIT is interoperable with other systems. Data can be exchanged seamlessly as and when required. This also allows market players to innovate rapidly to reach last mile without agencies losing strategic control of the data and key services. E.g. government agencies can ensure policy compliance through master data and workflow management while allowing market actors to build applications that delivers varied experience for different for different user groups.&#x20;
6. **Ease of Use** - DIGIT is designed keep in mind ease of access of all actors - citizens, employees, administrators as well as developers, system administrator etc. All data is available through API which can be used to channel specific applications - web, mobile, chat etc.&#x20;
7. **Open** - DIGIT is open source, uses all open source technologies and standards to ensure that data and core services are never vendor locked-in. MIT License gives the right to any agency or its partners to copy the source code and deploy it for their needs.

## Typical Public Service

A typical public service delivery starts with a citizen applying for a service or a service connection. The diagram below abstracts the typical information exchange flow that needs to be enabled between the various actors to deliver a service.

![](<.gitbook/assets/image (159).png>)

A digital system must provide the following capabilities to enable effective citizen service.&#x20;

1. Register/Login - Ability for the citizens to register or sign in or identify themselves. Ability to sign in using a single login id is key to enabling ease of access to digital services.&#x20;
2. Apply/Upload - Ability for the citizens to request services by filling out an application form and uploading a set of valid documents. Citizens should be able to access services from multiple channels and in their preferred language.&#x20;
3. Pay/Bill - Ability for the citizens to pay for the service and be able to download a bill for the payment made. Multiple options to pay through digital payments or cash should be available.&#x20;
4. Inform/Track - Ability for the citizen to track or receive updates about the applied services through SMS, Email or App Notifications.
5. Assign - Ability for the employees or vendors to assign the service application or trigger a workflow that would assign it to an employee or a vendor.  System should allow for configuring different workflows for different tenants to meet local needs.&#x20;
6. Search/View - Ability for the employees or vendors to search and view the application. Search should be enabled on multiple attributes.
7. Update/Comment - Ability for the employees to update and comment on the service application. In complex service delivery, back and forth is required between various parties. System should allow for structured and unstructured data flows between parties.&#x20;
8. Deliver/Verify- Ability for the employees or vendors to deliver the service e.g. set up a new water connection or verify/certify the information provided such as verifying economic status. Most service delivery requires field visit by staff or vendors. In low mobile coverage areas, apps with offline capabilities are required. Synchronization of data from these apps create load spikes and the system design should be able to handle these situations.&#x20;
9. Support/Feedback - Ability for citizens to raise support requests in case of an exception or provided feedback in case of closure of the service request. This requires ability configure surveys and feedback forms & analyze the responses to take corrective action.
10. Monitor/Improve - Ability for the administrators to monitor service performance and identify areas of improvement. All transactions must be accompanied with data events into analytical database that allows slicing and dicing the data required for performance monitoring.&#x20;
11. Plan/Budget - Ability for administrators and policymakers to plan and budget continuous improvement of services. This requires ability to link outlays to outputs.&#x20;

DIGIT provides a set of  [building blocks](platform/core-services/) that can leveraged to build above described [digital services ](./#typical-public-service)that adheres to the [key design principles](./#key-principles). DIGIT also provides optional accelerators like DIGIT UI and Dashboard Framework that can be extended to develop citizen, employee and administrator dashboards. The diagram below illustrates how some of the reusable building blocks interact to realize a typical public service delivery. The interactions between these services have been detailed out in the [Service Architecture](platform/architecture/service-architecture.md).&#x20;

![DIGIT Services](<.gitbook/assets/image (270).png>)

DIGIT is already being used to deliver services in 1000+ cities. Ecosystem partners including System Integrators are using DIGIT to build and deliver services.&#x20;

DIGIT is easy to install, configure and use. To install DIGIT on your servers use the [DIGIT Installation Guide](get-started/installation-guide/). To design and develop a new service on DIGIT Platform go through the [DIGIT Design Guide](get-started/design-guide/) and [DIGIT Developer Guide](get-started/developer-guide/).  You can also take up the DIGIT Certification through the [DIGIT Academy](https://app.gitbook.com/o/-MEQmzNGXk5ajuZujG7E/s/kI0HGCGboIe1ltcfV9XD/). &#x20;

If you want to experience DIGIT or develop on DIGIT, you can also access DIGIT demo using [Sandbox](platform/get-started/access.md).&#x20;

DIGIT comes with several accelerators. These include [UI frameworks](accelerator/ui-frameworks.md) and [Integration Adapters](platform/integrations/). These are optional. You may choose to develop or reuse your own UI framework and Integration Adapters.&#x20;

We organize several events for architects and developers on DIGIT. Keep a watch on the [Events](https://egov.org.in/events/) Page for upcoming events.&#x20;

Several volunteers are contributing to DIGIT in many ways. If you want to volunteer, check out our [contribute](platform/contribute.md) page.&#x20;

## Contact Us

{% embed url="https://egov.org.in/contact/" %}

