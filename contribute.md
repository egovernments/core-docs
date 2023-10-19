---
description: Contribute to DIGIT platform - Check out this space for frequent updates
---

# Contribute

## **Why Contribute To DIGIT?**

DIGIT is an open-source citizen service and governance platform. It is designed to streamline interactions between citizens, government employees, service providers, administrators and policymakers. The low-capacity national and sub-national government agencies do not have the ability to develop systems that can deliver services in a scalable and reliable manner. Additionally, they end up building systems that are closed and which lock data into departmental silos. This makes it difficult for citizens to access data, market players to deliver services and administrators or policymakers to make decisions. Each system builds and deploys multiple common functionalities for authentication, authorisation, location, notification, demand, payment etc. The issues, highlighted above, have severe impacts on the ability of government agencies to deliver coordinated services to citizens. &#x20;

The DIGIT platform is the architect of Digital Public Infrastructure that offers three layers of reusable microservices that help address these issues effectively.

1. **Common Services** - Include authentication, authorisation, notification, payment, workflow etc. There are 25 such common services.&#x20;
2. **Domain Services** - Include individual, household, property, beneficiary, program, etc. These services store data and make them available through APIs to any application in a scalable and secure manner.&#x20;
3. **Data Exchange** - To avoid point-to-point integrations, it is critical to build data exchange mechanisms and standards that enable agencies to exchange data in a trusted and non-repudiatable manner. This enables all agencies to deliver services in a coordinated fashion. For instance, once a birth is registered in the civil registry the health department should automatically schedule a vaccine or once the property is registered water, and electricity department automatically updates the details in their database. Data exchanges also enable a seamless flow of financial and service-related data between funding and implementing agencies in the government - streamlining the flow of money which is critical for service delivery. Lack of information results in delays in payments to frontline workers, employees, pensioners, vendors etc. which impacts service delivery.&#x20;

Building on an open-source platform like DIGIT can enable governments in low-capacity countries to deliver and govern services delivery in a scalable and reliable manner.&#x20;

## **How Can You Contribute?**

To operate in low-capacity environments, platforms need to be not just secure and scalable but also easy to install, build on and operate.&#x20;

Listing down the list of challenges you can help solve -&#x20;

1. How can we make DIGIT more secure, performant, reliable, and privacy-conserving?&#x20;
   * Review the code and suggest improvements
     * [x] How DIGIT works at a high level is described here - [https://core.digit.org/platform/architecture/service-architecture](https://core.digit.org/platform/architecture/service-architecture)
     * [x] DIGIT Core Services and DIGIT Urban Services - code bases are available here - [https://github.com/egovernments/DIGIT-OSS](https://github.com/egovernments/DIGIT-OSS)
2. How can we make it easy to build and install DIGIT, especially in low-capacity environments?
   * DIGIT infrastructure architecture is available here - [https://core.digit.org/platform/architecture/infra-architecture](https://core.digit.org/platform/architecture/infra-architecture)
   * The installation scripts are available here - [https://github.com/egovernments/DIGIT-DevOps](https://github.com/egovernments/DIGIT-DevOps)
   * We are exploring ideas like installation wizards. Any such ideas are welcome.&#x20;
3. How do we help more developers build on DIGIT?
   * How do we make it easier to integrate low code no code environments to build applications on top of DIGIT?
   * How do we interoperate with existing open-source DPGs e.g. MOSIP, DHIS2, Sunbird, OpenLMIS etc. to enable a seamless exchange of information? How do we conform to standards like HL7 and GS1?&#x20;
4. Develop standards where not available&#x20;
   * Unified Government Interface specifications are being developed to address issues of service discovery, unified experience for citizens, federated service execution, unified billing, unified data for administrators and policymakers, and coordinated service delivery across agencies. We envision a standard API interface so that services can be delivered not just through government portals and apps but also through payment and e-commerce apps developed by startups and market players ensuring services reach every citizen of the country. Standardised APIs can democratise service delivery and enable market players to participate in service delivery. Think of this as UPI for Government Services. This initiative is still in its formative stages, if you are interested you can reach out to us at - [https://usi.digit.org/](https://usi.digit.org/)
5. Develop Products on top of DIGIT
   * We have built a few products on top of DIGIT e.g. Citizen Portal, Assisted Service Delivery Mobile App (with offline capabilities to deliver services in remote areas), Employee Workbench, and Administrative Dashboards. The code is available at [https://github.com/egovernments/DIGIT-OSS/tree/master/frontend](https://github.com/egovernments/DIGIT-OSS/tree/master/frontend). It's getting a little heavy. We are trying to modularise this and convert this into plug-and-play for new services. Your input on this will be very valuable.
   * Voice - How can we deliver services using a voice interface? Anyone interested in exploring the delivery of services using voice and AI4Bharat - [https://ai4bharat.org/](https://ai4bharat.org/) - How can we fill out a form for initiating a service delivery using voice?&#x20;
   * IOT - Sanitation Mission team is looking for help tracking measurement data from FSTP plants.
   * Many low and middle-income countries don't have Unique IDs like Aadhar, when distributing benefits, how do we enable deduplication/authentication of beneficiaries in an offline manner and using a privacy-preserving method?
6. Enhance Core Platform
   * Parallel Workflows - DIGIT Core has a workflow component that is currently implemented as a simple state machine. There is a requirement to support parallel workflows - this may translate to supporting multiple states in the state machine.&#x20;
     * [x] Code is available here -[https://github.com/egovernments/DIGIT-OSS/tree/master/core-services/egov-workflow-v2](https://github.com/egovernments/DIGIT-OSS/tree/master/core-services/egov-workflow-v2)
     * [x] Documentation is available here - [https://core.digit.org/platform/core-services/workflow-service](https://core.digit.org/platform/core-services/workflow-service)

{% hint style="success" %}
Check out this space for updates. If you are interested or have any questions post them on our Discussion Board - [https://github.com/egovernments/Digit-Core/discussions](https://github.com/egovernments/Digit-Core/discussions).&#x20;

Join our Discord channel ([click here for the invite link](https://discord.gg/X7QAjmvjBp)) to get the latest updates and participate in discussions on everything DIGIT - projects, events, new ideas etc.
{% endhint %}

