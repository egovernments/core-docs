---
description: An open source service delivery and governance platform
cover: .gitbook/assets/Docs Digit Banner copy.jpg
coverY: 0
---

# Introducing DIGIT Platform

## Vision

To enable good citizen service, citizens, employees, vendors, administrators and policymakers to collaborate and exchange information seamlessly.

## Overview

**DIGIT** is a service delivery and governance platform. It enables ease of access to services for citizens, ease of coordination for employees & vendors, ease of administration for administrators and ease of policy-making for policymakers & researchers.

<div align="left">

<img src=".gitbook/assets/image (24).png" alt="">

</div>

## Goals

The diagram below abstracts the typical information exchange flow that needs to be enabled between the various actors to deliver effective citizen service.

![](<.gitbook/assets/image (203).png>)

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

## Approach

Each government agency builds applications that provide some or all of the above-mentioned capabilities. However, most of these applications are not built to scale or have the ability to exchange data with other applications. This results in locked data within application siloes that renders it unusable to other services. It is a primary cause for the fragmented experience of the citizens - who find it difficult to discover and use these services. The employees are forced to remember multiple passwords and use several applications at work. Administrators fail to get the integrated information required for monitoring performance and identifying areas of improvement. The result is poor planning and inflated budgets.

<div align="left">

<img src=".gitbook/assets/image (256).png" alt="Traditional application oriented approach leads to siloes, wasteful duplication, non-scalable and difficult to integrate">

</div>

DIGIT is built using platform-based principles that enable the seamless sharing of data and functionality through well-defined building blocks. The building blocks can be integrated into higher-level services that can also be recomposed further to deliver unified data and experiences.&#x20;

![](<.gitbook/assets/image (163).png>)

Core services and core data registries are grouped together to define the "Foundation" or "Core Platform". These services and registries are reused by services that are part of Urban, Sanitation, Health Platforms etc. All services and registries are exposed through well-defined APIs which can be used to build applications that deliver a unified experience to citizens, employees, vendors, administrators and policymakers.

Refer to the [platform design principles ](platform/principles.md)that define DIGIT capabilities.

To enable the capabilities required to develop a good service, DIGIT provides a set of reusable building blocks (microservices) listed below that adhere to the above principles. A developer can build any service or registry by reusing the DIGIT services. DIGIT also provides accelerators like DIGIT Web Dashboard that can be extended to develop citizen, employee and administrator dashboards. More details on each of the services are available on the [Platform Architecture](platform/architecture/service-architecture.md) page.&#x20;

![DIGIT Services](<.gitbook/assets/image (99).png>)

## Useful Links

To install and start developing using DIGIT, visit the [Get Started](getting-started/) page.

The list of developer [Checklists/Guidelines](platform/checklists/) ensures that the services built using DIGIT are robust and easy to use.&#x20;

Check out the platform [training resources](getting-started/training-and-certification/training-resources.md) page and access our multiple walk-through videos.

## Contact Us

{% embed url="https://egov.org.in/contact/" %}

