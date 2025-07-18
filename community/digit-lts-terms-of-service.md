---
description: Terms of Service (ToS) for DIGIT LTS
---

# DIGIT LTS - Terms Of Service

## Overview

This document outlines the principles and practices for long-term support of DIGIT as an open-source platform. It is not a commercial support agreement.

Digital Infrastructure for Governance and Inclusive Transformation (DIGIT) is an open-source, scalable, interoperable platform for responsive public service delivery and good governance.  It enables government agencies to digitise public service delivery  - providing unified interfaces for citizens, front-line employees and administrators to exchange information with each other in a seamless and trusted manner. DIGIT is an open-source platform built for scale. DIGIT is multi-tenant and can enable the digital transformation of multiple government agencies at speed and scale using a common shared infrastructure. eGov Foundation is the majority contributor and maintainer of DIGIT.

DIGIT 2.9 represents the most recent Long-Term Support (LTS) version, offering a stable and reliable foundation for governments and their partners to build robust public service delivery systems. This version emphasises enhanced security measures, improved system stability, streamlined deployment processes, simplified configuration, and comprehensive documentation. Periodic updates, encompassing both minor adjustments and significant enhancements, will be released as necessary. More information is [available here](../platform/releases/).

## License

DIGIT 2.9 LTS is licensed under the MIT license. It is a short and simple permissive license with conditions only requiring preservation of copyright and license notices.

## Support & Maintenance&#x20;

{% hint style="info" %}
Note: This document lays out the Terms of Service to support [DIGIT 2.9 LTS Core Services](../platform/core-services/) only. This does not include domain Services built on DIGIT. Example: DIGIT Urban Services or Health Campaigns, etc.&#x20;
{% endhint %}

### Support Services

Users are requested to use the [Guides available here](../get-started/installation-guide/) to install and start using DIGIT LTS. Documentation will be updated at regular intervals based on feedback from users. Inputs to the documentation can be [submitted here](https://github.com/egovernments/Digit-Core/discussions) with the tag ‘ documentation’.&#x20;

As the main contributor and maintainer of DIGIT, eGov strives to ensure the bugs/ issues/ enhancements reported by the community are attended to on a best effort basis. All users are requested to contribute to the discussion board as per their capacity.&#x20;

### Issue Reporting Process&#x20;

* First, the user/ partner should check the GitHub core repo for the same/ similar issue already reported and the fixes/workarounds provided.
* If the above is not available, the user/ partner shall provide details of investigations carried out by their teams, along with logs and inferences leading them to believe that the issue lies with the core services of the DIGIT LTS. https://github.com/egovernments/Digit-Core/discussions is the single point for all discussions which require support. Please ensure the use of appropriate tags ( if any) before submitting a new issue.&#x20;

The eGov support team shall acknowledge the discussion board input and analyse it. If it qualifies as an issue, it will be moved to the issue list for the users to track there. The support team will check versions to ensure that the services running are supported by the LTS version.

Response SLAs: Hours of support: 9 am to 6 pm Indian Standard Time, Monday to Friday (excluding public holidays).

<table><thead><tr><th width="174.46875">Severity</th><th width="412.44140625">Description</th><th>First Response SLA</th></tr></thead><tbody><tr><td><p>P1, </p><p>Production Halted</p></td><td>Critical bug impacting service for which the cause is unknown. No bypass or work around available. Typically, security bugs will be top priority and taken up in this category</td><td>1 working day</td></tr><tr><td><p>P2, </p><p>Production Degraded</p></td><td>A key component of the applications is degraded, unusable or unavailable, user has isolated it to an issue in the core services. No workaround available. </td><td>2 working days</td></tr><tr><td>P3, Business Unaffected</td><td>A component of the application is degraded, which causes a minor inconvenience, but a workaround is available.</td><td>4 working days</td></tr></tbody></table>

> \*First Response SLA is defined as the committed time frame within which the support team acknowledges a reported issue after receiving any additional clarifications from the user and initiates investigation or action

{% hint style="info" %}
**Note:** Security vulnerabilities should be reported privately using the Security tab in the repository. Please do not disclose them in public issues or discussions.
{% endhint %}

Wherever feasible, the eGov support team shall provide a resolution to the issue by issuing:

1. For P1 issues, eGov will provide a patch release to close out the issue. The timeline for patch release will be dependent on the estimated amount of work required and will be communicated to the users. Such fixes will be added to the backlog to be considered for the DIGIT LTS roadmap in the next iterations after following the regular QA processes.&#x20;
2. For others, clarification or a workaround to resolve the issue. In this case, the eGov support team will provide troubleshooting support to the user/ partner who has a time-critical dependency on resolving the issues and users are encouraged to contribute this back to the platform.&#x20;
3. If this is found to be a genuine bug in the core services, which is already on the platform roadmap, eGov will plan to fix it in a newer release, and the user/Partner will get the fix once upgraded by eGov.
4. Support will be limited to the core services of the platform. Refer to the [list of services here](../platform/core-services/). Elements like UI Frameworks are available for users, but are not supported. In case of any changes to the core services by the user/partner, then those services and their dependent services will no longer be supported. However, users are encouraged to report any issues on the discussion board for potential resolution by the DIGIT community.

{% hint style="info" %}
Please note that all issues will be responded to, but not attended to by eGov Foundation alone and will be resolved on a best effort basis. We aim to anchor a community around DIGIT, which over time will enable resolution by different members of the community. We request that users from organisations signed up on the Partner Program please mention the same for priority response.
{% endhint %}

## Maintenance & Updates

Any known issues in the LTS would be documented on GitHub in the core platform repo so that users can check for fixes/workarounds.&#x20;

eGov will share the DIGIT roadmap with users every quarter.. The roadmap will provide enough detail that allow the Partner to plan for changes at their end. All issues on the discussion board will be taken into consideration while finalising the platform roadmap. The platform roadmap will be published on Gitbook with a discussion board for any Q\&A. &#x20;

Any user in the community is allowed to raise a pull request on the DIGIT core repository. At present, the core team at eGov is responsible for maintaining the core repository and ensuring the timely review and resolution of pull requests.

## Duration & End-of-Life (EOL)

**Support Period:** Support for this iteration of DIGIT (2.9 LTS)  will be available for five years (till 2029), with a clear migration guide available to facilitate the transition to subsequent LTS versions once the current support period concludes.

**End-of-Life Policy:** End of Service Life (EOSL) considerations for the LTS version will be shared by eGov. EOSL will be flagged as per the upgrade guideline. This will also act as a trigger for upgrades. Notice will be provided at least 6 months in advance of EoL wherever possible.

## User Responsibilities

Security: Please refer to the [general and role-based security and privacy guidelines](../guides/security-and-privacy-guide/) for DIGIT.

* eGov will share the security audit reports carried out periodically, as and when these security audits are conducted.
* Users/ partners are responsible for maintaining security, such as applying updates in a timely manner and securing their environment against threats.

## Disclaimers & Limitations Of Liability

**Disclaimers:** As the primary contributor and maintainer of DIGIT, eGov will publish the latest reliability, accuracy and performance benchmarks for DIGIT LTS as and when they are done. However, we request all users to benchmark the parameters themselves and report in case of significant deviations. In such cases, eGov will work with the user to check for possible issues, but it does not guarantee the exact same performance.

**Liability Limitations:** Limits on the liability of the software provider for damages arising from the use of the LTS release, including indirect or consequential damages.

Under no circumstances shall eGov or any of its employees, consultants, trustees, directors or agents be liable in any amount for special, incidental, consequential or indirect damages, loss of goodwill or profits, or exemplary or punitive damages, irrespective of who initiates the claim. eGov disclaims any and all liability in relation to the Platform and the services, if any, provided under this document.

## Privacy & Data Protection

**Data Collection & Privacy Guidelines:**&#x20;

The DIGIT Platform team ensures key security and privacy features are incorporated in DIGIT and provides guidelines for other actors. Refer to [this section](../guides/security-and-privacy-guide/#digit-platform-practices) for detailed guidelines. Partners/users are encouraged to follow these guidelines while developing/ implementing programs using DIGIT LTS.

**Modification of Terms:**&#x20;

In the event of material changes to eGov’s financial or operational capacity, the terms of DIGIT Support may be revised with 60 days' prior written notice.

**Acceptance of Changes:**&#x20;

Continued use of the LTS release by users/ partners will constitute acceptance of any updated terms.

## Contact Information

Support Contact: All questions/ queries related to LTS release may be posted on the GitHub discussion link [here.](https://github.com/egovernments/Digit-Core/discussions)

## Additional Provisions

Third-Party Software: DIGIT core services are developed using the following technologies&#x20;

* Java Spring Boot
* Apache Kafka
* Spring Cloud Gateway
* Postgres
* Elastic Search
* Docker
* Kubernetes
* Terraform

{% hint style="info" %}
More information about these open-source tools and API gateways used in DIGIT is [available here](../platform/architecture/technology-architecture/). DIGIT support will be subject to the support terms and conditions of these underlying technologies, and some issues arising out of underlying issues in any of these technologies cannot be covered as part of this support document.&#x20;
{% endhint %}
