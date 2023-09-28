---
description: >-
  Data protection and privacy guidelines for DIGIT implementations for platform
  owners
---

# Platform Owner Guidelines

## Scope  <a href="#_vj7zzjs0bsw1" id="_vj7zzjs0bsw1"></a>

DIGIT, an open-source platform, provides a citizen-facing service delivery system in urban governance, sanitation, health, and public finance management.

As citizen data is collected and used for such governance services, data privacy and protection measures are required to ensure this data is managed responsibly and safely.

This document is created to be an online guide, providing guidelines for platform owners (providers of DIGIT-like systems) to maintain data privacy and protect individuals’ data.

* Readers can use this to identify the steps they must take as platform owners or providers to ensure data privacy and protection in the context of a DIGIT or DIGIT-like implementation.
* It can also provide source material for privacy policies, which should be included in each portal & application.
* This is not a technical reference or documentation. It serves as a policy guideline.

References made to DIGIT are also applicable to other platforms similar to DIGIT. Not all parts of the guidelines or featured content may match the reader's platform, hence this document is open to be referred to in parts as needed.

## **Basic Terms & Definitions** <a href="#_3znysh7" id="_3znysh7"></a>

### **What is data?** <a href="#_1o66mexb72h4" id="_1o66mexb72h4"></a>

Data is the information collected from an individual or about an individual. In DIGIT, data can be any information pertaining to a citizen, which is required for delivery of service and/or information exchange flow amongst citizen, employee, vendor and administrator. Data and information are interchangeably used.

### **What is data security?** <a href="#_v6gdeeea0fcw" id="_v6gdeeea0fcw"></a>

Data security is the act of securing and safeguarding data. Active measures are taken to protect the data from misuse or harm. Such actions can be pre-emptive i.e. security steps taken before the data is collected or the actions could be reactive i.e. steps taken after the platform has been set up. DIGIT recommends pre-emptive steps as a best practice, and has[ data security](https://core.digit.org/focus-areas/data-security) measures embedded within its design.

### **What is data privacy?** <a href="#_vmzhiqron6rd" id="_vmzhiqron6rd"></a>

Data privacy means keeping the data in the control of the individual and allowing the individual to decide what is to be done with their data. Data that is collected or shared without the consent of an individual, especially when exposed and combined with other data points, can cause citizens to be identified and targeted. That’s why protecting data indirectly protects the citizen as well.

Data Privacy requires protecting the data from unwarranted viewing, use, or sharing. This involves taking steps such as data minimisation (only collecting and storing data that serves a defined purpose), encrypting data, restricting access to the data, and/or masking what data is visible to users. DIGIT is designed to maintain the privacy of citizens and protect data by taking all the steps mentioned above and [more](https://core.digit.org/focus-areas/privacy).

### **What is personally identifiable information (PII) or personal data?** <a href="#_avw9r68m0hy3" id="_avw9r68m0hy3"></a>

PII stands for personally identifiable information or is also interchangeably used as personal data.

Personal data is defined under the Digital Personal Data Protection Act, 2023 [DPDP Act](https://www.meity.gov.in/writereaddata/files/Digital%20Personal%20Data%20Protection%20Act%202023.pdf) at Sec 2(t) - “personal data” means any data about an individual who is identifiable by or in relation to such data

Personal data is basically any information that makes a person identifiable. This consists of data that is unique for each person. When it is combined with other forms of data, it can help in identifying a person. For example, our biometric information, credit card details, passport details etc. are all PII.

### **What is a personal data breach?** <a href="#_oevc7uimklg1" id="_oevc7uimklg1"></a>

The DPDP Act at Sec 2 (u) states that “personal data breach” means any unauthorised processing of personal data or accidental disclosure, acquisition, sharing, use, alteration, destruction or loss of access to personal data, that compromises the confidentiality, integrity or availability of personal data

A personal data breach means a breach of security leading to the accidental or unlawful destruction, loss, alteration, or unauthorised disclosure of, or access to, personal data. This includes breaches that are the result of both accidental and deliberate causes. It also means that a breach is more than just about [<mark style="color:blue;">losing personal data</mark>](#user-content-fn-1)[^1]<mark style="color:blue;">.</mark>

Personal data breaches can include:

* access by an unauthorised third party;
* deliberate or accidental sharing of data, or of credentials that enable access to data, with an unauthorised person by a handler, collector or processor;
* sending personal data to an incorrect recipient;
* computing devices containing personal data being lost or stolen;
* alteration of personal data without permission; and
* loss of availability of personal data.

Both the above definitions can be read together, but the definition given in the DPDP Act would get a preference in case of a conflict.

### **What kind of data does DIGIT handle?** <a href="#_2et92p0" id="_2et92p0"></a>

The DIGIT platform does not handle data unless and until it is implemented in a particular context. Each implementation of DIGIT handles a combination of non-personal data and PII; the latter may further be classified into data which, in itself, identifies the individual to whom it pertains (“identified”) and data which, if combined with other data, can identify the individual to whom it pertains (“identifiable”)\[3].

## **B1. Personal Data / PII Of Residents/Citizens** <a href="#_pa9xsk8yd4hi" id="_pa9xsk8yd4hi"></a>

Specific data recorded in various applications that may be implemented on DIGIT include name, parent/spouse’s name, mobile number, city, email id, date of birth, door no/address, and pin code. Data from administrative record systems, such as revenue survey number or other property identifier, connection number, meter number etc. may also be recorded. In the event a person makes payments to the local government, information related to the payment, such as transaction number may also be recorded.

Any personal data collected and stored in DIGIT is encrypted, both in storage and transmission. When displayed, this [data is to be masked by default](../../../../focus-areas/privacy/). Users can request to unmask data; if they have the appropriate authorisation, they will be able to view the unmasked data, and this request to unmask will be [<mark style="color:blue;">recorded in an audit log</mark>](#user-content-fn-2)[^2].

DIGIT implementations are used to provide government services to residents of a given city, town, village etc. The data collected, as described above, are necessary for the delivery of such services. When a resident approaches their local government for a particular service, they can be required to share, or allow access to, the information necessary to provide that service.

### **B2. Personal Data / PII Of Employees** <a href="#_jnpmymlfya7u" id="_jnpmymlfya7u"></a>

DIGIT implementations also collect, store, process, and share information pertaining to employees of local government or other government agencies. Specific information can include name, age, gender, details of spouse or dependents, address, administrative details such as employee ID or other reference number, as well as information on bank accounts (used for processing salaries or pensions).

As employers, local governments may be required to maintain certain information on their employees and pensioners for tax purposes, such as PAN numbers; this information may be recorded and shared as well.

### **B3. Non-Personal Data** <a href="#_sps29nw1utrm" id="_sps29nw1utrm"></a>

DIGIT implementations may derive, store, process, and share transactional data, which describes the progress of any ongoing task (e.g. any service requested by a resident) through the systems of the local government or other government agency. This can include information about the specific role to whom a given task is assigned (or with whom it is pending), the amount of time elapsed on processing / completing a given request (or task / sub-part thereof), and whether this task has been completed within the benchmark or designated amount of time. It can also include details about the channel through which a particular request was received, such as the ULB counter, service centre, website, helpline, mobile app, chatbot, etc.

DIGIT implementations may derive, store, process, and share aggregated data. These aggregates are derived from the transactional data. This includes data such as aggregate or cumulative revenue collection, aggregate or cumulative number of service requests, percentage of requests resolved within the benchmark time period, etc. The above data may be further analysed and presented in terms of the type of collection, request, or complaint, the channel through which it was received, etc.

DIGIT implementations may collect, store, process, and share telemetry data, which studies how much time is spent on a given screen or field in a workflow/user interface (UI). Such data is normally processed and shared in aggregate, and not used to identify specific individuals. In the event that specific individuals are sought to be identified, such as for user research, their consent will be sought for the further processing or sharing of their data.

### B4. General Compliance With Legal Obligations & Global Best Practices <a href="#_et8374bgapwn" id="_et8374bgapwn"></a>

DIGIT is designed to enable compliance with requirements under Indian law, as well as global best practices, as follows:

* The requirement for a legal basis for the collection, storage, processing, use, and sharing of such data is fulfilled by the mandate of the local government or other government agency to provide a particular service.
* The requirement of a legitimate purpose is also met by the mandate of the local government or other government agency to provide that particular service.
* The requirement of proportionality is generally met by only collecting or accessing such data as is necessary for providing that particular service. This is also in line with the global best practice of data minimisation.
* The requirement for safeguards is generally met by the security and privacy measures, such as encryption and masking, described above; it is further met by implementing role-based access controls, which are aligned with the global best practice of differentiated access.
* The requirement for safeguards is further served by providing itemised notice, and by enabling any person to view what data of theirs has been collected/processed/shared (including the purpose for such collection/processing/sharing). Such provision of notice and visibility is further in line with global best practices of notice & user control. Such notice can only be provided in the context of a DIGIT implementation, and eGov provides a draft [privacy policy](https://docs.google.com/document/d/1TlGUZg5stbJPU5ZXUEiLM9LcBCkjmKjsjmEEPxsYCs4/edit?usp=sharing) to implementing entities.
* With respect to employees and pensioners, the requirements for legal basis, legitimate purpose, and proportionality are generally met by collecting, storing, processing, using, and sharing only such information as is relevant for assigning roles and administrative responsibilities, processing salaries or pensions, and completing any mandatory tax-related reporting.

### **Who Handles Data In The DIGIT Lifecycle?** <a href="#_tyjcwt" id="_tyjcwt"></a>

The datasets flow from a point of service (POS) device to the integrator system, and from the backend of the integrator system to the DIGIT platform.

Data may be entered into a DIGIT registry or database in one of four ways:

* A citizen directly enters the data into a web portal, application, chatbot etc., as part of requesting government services.
* A local government or other government entity employee or contractor may enter the data into the system on their allocated device (computer at the service counter, mobile application in the field, etc.), as part of their work in providing government services.
* Data is migrated/ported from some previous systems, including paper-based systems, especially during the initial setup of the DIGIT-based system. This is also known as data migration.
* Data is shared in digital formats, such as through APIs or machine-readable spreadsheets, from some other system or platform to a system running on DIGIT.

Each module in DIGIT has different _departmental employees_ feeding data at the field level.

These roles and their levels of access are determined by the administering authority (typically a local or state government), as part of the initial setup of the DIGIT-based system.

Existing roles may be modified and new roles may be created by persons who are authorised to act as system administrators following the initial setup. This means that the administering authority (or a person delegated this power by the administering authority) recognises these roles, and provides them with login credentials to access and collect citizen data for delivery of government services.

Examples of such roles that are recognised by our platform are: “EMPLOYEE","CITIZEN",”DOC\_VERIFIER",”FIELD\_INSPECTOR",”APPROVER","CLERK".

In any given implementation of DIGIT, the administering authority (local or state government) is understood to have responsibility for the data and is treated as the main data fiduciary with respect to the data of residents that is collected, stored, processed, used, or shared through or by the DIGIT-enabled tools or systems in use in its jurisdiction.

The primary responsibility for ensuring compliance with legal obligations and best practices with respect to data security, data protection, and privacy is thus that of the administering authority. To the extent that any other party (including eGov Foundation) serves as an agent of the administering authority, they are similarly considered responsible for ensuring such compliance, to the extent relevant to the tasks that they are performing.

## **Guidelines** <a href="#_rnray17wkmt3" id="_rnray17wkmt3"></a>

These guidelines are to be read through the eyes of specific roles in the journey of adopting a DIGIT-based system or platforms similar to DIGIT in a government entity/ies. For each such ‘role’, a reader can follow its tasks in a given stage of implementation of DIGIT or such platform, and the guidelines associated with that task and stage.

It is to be noted that similar guidelines can be found for ‘data controllers’ under the General data protection regulation of Europe. There are a few basic and minimum requirements that data controllers (bodies that decide the purpose for processing data and the means used to process the data) have to comply with to ensure data protection by default (DbD and PbD) and design (data minimization, implementing safeguards for protection of data, controlled access to data, [<mark style="color:blue;">limited purposeful storage</mark>](#user-content-fn-3)[^3], etc). In Europe, entities are legally obligated to maintain DbD and PbD or else they are heavily penalised.

### **D.1 Guidelines for all roles** <a href="#_1t3h5sf" id="_1t3h5sf"></a>

There are a few common guidelines that all roles in the platform implementation process must follow.

_Data security measures and practices stand out as the core / foundational guidelines to follow for all roles._

DPP is only possible when the systems and computer resources receiving and storing data are secure (safe from any harm). Some key data security measures include:

* Access control: Establish audited and controlled access for personally identifying data, including authentication and authorization mechanisms. Authorize individuals only if they have a legal basis and a [legitimate purpose to access the data](../../../../focus-areas/data-security/signed-data-audit.md).
* Encryption: Encrypt PII data both in transit and at rest to protect it from unauthorized access and theft.
* Data backup and disaster recovery: Regularly backing up PII data - including auditing the need for PII - if not required then deleting the PII, and implementing disaster recovery plans to ensure that important data can be recovered in the event of a data loss or breach.
* Network security: Implement firewalls, intrusion detection and prevention systems, and other network security measures to protect against cyber threats.
* Vulnerability management: Regularly scan for vulnerabilities and patch systems and applications to minimize the risk of a breach.
* Employee education: Educate employees/contractors/personnel on the importance of data security and provide training on best practices for protecting PII.
* Physical security: Implement physical security measures, such as access controls and video surveillance, to protect against unauthorized access to data centres and other data facilities.
* Third-party security: Carefully vet third-party vendors and service providers, to ensure that they have appropriate security measures in place to protect PII.
* Incident response: Develop and test incident response plans to ensure that the organization can quickly and effectively respond to a security breach.
* Compliance: Adhere to relevant security and privacy regulations, such as the IT Act, 2000, and its subsequent amendments and Rules. Conforming with standards such as ISO 27001 is also a good practice.

### **D.2 Detailed Guidelines for Platform Owners** <a href="#_4d34og8" id="_4d34og8"></a>

The roles we cover under these guidelines are that of:

* **Platform Owners** (any individuals or body that creates and owns the platform which facilitates/enables the governments to provide for delivery of service)

The next document in this series covers the following stakeholders -:

* **Administering authority** (**AA)** (the entity that is mandated to provide for the government service usually an agency or department of the State government). This can include bodies like the [State Program Directorate and Program Monitoring Units.](https://niua.in/cdg/UPYOG)
* **Implementation agency (IA)** / system integrator (the entity that implements the platform provided by the platform owner into the administering authority’s IT and operational systems).
* **Support agency (SA)** (the entity that may be involved after the platform is implemented, to maintain the system and provide support/troubleshooting.)

To understand what each role should do to safeguard DPP, it is important to understand what these roles do at each phase of the implementation of DIGIT.

### D.2.1. Stage 0 -Program set-up <a href="#_2s8eyo1" id="_2s8eyo1"></a>

**What is a program?**

A program can be a delivery of any government service/s which the AA is mandated to provide to citizens for which it requires a platform. Defining the scope of the program is within the power of an AA.

**D.2.1.1 **_**What happens at this stage?**_

* A Memorandum of Understanding is signed between the AA and the platform owners
* State Program Head/Nodal Officer Appointed by the AA
* Resources and funding for the program are identified.
* The AA-specific procurement process is defined.
* IA team onboarding initiated.

_**D.2.1.2 Platform Owner at Stage 0 -**_

* Share specifications for man-power and infrastructure
* Program setup best practices are shared
* Enablement for product, configuration, infra

**D.2.1.3. To-Do’s:**

**Operational:**

* Any kind of agreement to be signed between the platform owners and the AA (e.g. an MoU) must have clear terms of data management, liability, and governance.
* Inform and clearly explain the platform’s in-house data practices and in-design DPP policies and practices of the platform to the AA.
* Create and maintain data use agreements with the AA (points on the legal framework for data access, what is to be done of the data and security controls are agreed on)

**Advisory:**

* Encourage and guide AA to adopt Privacy by Default
* Encourage AA to include DPP-enabling tech/non-tech resources in infrastructure resource planning. ( For eg - budgeting and reserving resources for data privacy impact assessments on the modules to be deployed)
* Encourage and guide the AA team in creating their data privacy and protection policy
* Identify the risks and necessary measures with the AA to ensure that any present or future data processing conducted by the AA is safe by design of the platform (Conduct data protection impact assessment)
* Guide and assist AA’s in training their employees in DPP practices
* Platform team to write a pre-mortem – an imaginary article looking back from the future on the feature’s perfect launch or failure – to help the AA and IA to focus on the privacy aspects that will ensure success.
* Encourage the AA to appoint privacy and data security-compliant Implementation teams or IA’s.

**Technical:**

* Do not offer any service module unless it is not compliant with relevant data privacy and protection (**DPP**) checks/standards and systems (see checklist in Appendix B of this [memo](https://docs.google.com/document/d/10bsSWEmf2ebjNpGBs-BLXAVyL-sVFQ901GzuKpbNNyY/edit?usp=sharing))

### D.2.2 Stage 1 - Program kickoff <a href="#_bp6265gjkhb" id="_bp6265gjkhb"></a>

**D.2.2.1 What happens in Stage 1**

* Publishing of the program charter and implementation plan.
* Master data collection kickoff in Pilot ULBs
* Cloud Infrastructure is procured
* Program branding is done (name, logo, tagline etc.)

_**D.2.2.2**_** Platform Owner’s Role in Stage 1**

* Guide and review manpower, infra and program governance structure. Provide a stable platform version.

**D.2.2.3 To-Do**&#x20;

**Operational:**

* Assist and encourage the AA team in setting a standardised data collection framework (with DPP practices like minimum personal data collected, masking of data, providing clear and simple notice to residents.)
* Assist the AA and IA teams in placing DPP principles and practices in the program charter
* Implementation kick-off workshop must include training in DPP practices ( minimum data collection, masking at field level, etc.)
* Encourage field-level ULB data collection team to inform residents about what data is collected and for what purposes

**Advisory:**

* Encourage the AA team to keep DPP as a priority in the implementation plan
* Advise the AA teams to collect as minimal data as possible to comply with the data minimisation principle ( at the master data collection level)
* Encourage within the AA employees, the behaviour of adopting privacy enhancing technology (PET). Highlight the increase of trust and reputation through the adoption of PETs’.
* Encourage IA to comply with data principle practices enlisted [here](../global-standards-for-all.md).

**Technical:**

* Procured cloud infrastructure providers must be reviewed for DPP practices/compliance, especially around retention periods, access logs, and incident/breach management.

### D.2.3 Stage 2 - Solution Design <a href="#_b6v3q25yf9i" id="_b6v3q25yf9i"></a>

**D.2.3.1 What happens in Stage 2**

* Standardized ontologies (uniform terminology for easier understanding), processes and workflows are created.
* Master data collected in the desired format.
* Agreement on program-specific product customisations is required.
* A detailed program plan is made and the tracking mechanism is finalised.

**D.2.3.2 Platform Owner’s Role in Stage 2**

* Guide and review the platform's extension/customisation, data collection/migration and accepted best practices.

**D.2.3.3 To-Dos:**

**Operational:**

* While standardizing processes and workflows, encourage the AA andIA teams to conduct a Privacy Impact Assessment (PIA): To identify PII that is being collected, processed, and stored, and to assess the risks associated with these operations. This will help identify any privacy issues that need to be addressed in the workflows.
* Develop privacy policies and procedures that outline the AA’s / program’s commitment to data privacy, and specify the measures that will be taken to protect personal data. These policies and procedures should be integrated into the workflows of the modules.
* Train employees on data privacy principles, such as data minimization and privacy by design. This will help ensure that they are aware of the importance of protecting personal data and the measures they need to take to do so.
* Assist the AA and IA in designing a clear data breach response plan (sets out procedures and clear lines of authority for responding to data breaches)
* Any changes or additions requested by the AA team that are contrary to any of the data privacy and protection regulations or principles must not be agreed to.

**Advisory:**

* Advise to regularly monitor and audit workflows to ensure that privacy policies and procedures are being followed and that personal data is being protected. This will help identify any areas where improvements can be made to ensure that data privacy is embedded in the workflows of the organization. Create a role that does the above.
* Assist the AAs in updating policies and procedures: Regularly review and update privacy policies and procedures in response to changes in technology, and data privacy regulations. This will help ensure that the state stays up-to-date with best practices for protecting personal data.
* Advise maintaining a data security ISO standardization as a prerequisite (ISO 27001 is recommended)
* Encourage the AA team to create strict access to workflows (login-based access, with access logs and periodic audits)
* Encourage better privacy by design customisations (for eg, masking from the point of collection)

**Technical:**

* Implement privacy-enhancing technologies (PeTs), such as encryption, anonymization, and access control systems, to protect personal data. These technologies should be integrated into the workflows of the module to ensure that personal data is protected throughout its lifecycle.

### D.2.4 Stage 3 - Customisations and Configuration <a href="#_l42rwxdrxzd" id="_l42rwxdrxzd"></a>

**D.2.4.1 What happens in this stage?**

* A configured/customized product is created that is ready for UAT ( User acceptance testing).
* Monitoring Reports and Dashboards are ready ( to understand the rollout of the modules).
* Product artefacts like user guides are created.
* Identification of participants for the UAT session.

**D.2.4.2 Role of Platform Owner in Stage 3**

* Guide and review architecture, solutions and UX.
* Support in the configuration/customisation processes

**D.2.4.3 To-Dos**

**Operational:**

* Create user guides to maintain privacy as default (e.g. Appendix B in this [memo](https://docs.google.com/document/d/10bsSWEmf2ebjNpGBs-BLXAVyL-sVFQ901GzuKpbNNyY/edit?usp=sharing) can guide compliance with privacy principles.)

**Advisory:**

* Advise for privacy by default features to be adopted
* Guide in the protection of hardware from [<mark style="color:blue;">security threats</mark> ](#user-content-fn-4)[^4]
* Ensure and assist the AA in making sure that all access controls have been set up
* Advise the state to include data privacy and protection [checklist questions](https://docs.google.com/document/d/10bsSWEmf2ebjNpGBs-BLXAVyL-sVFQ901GzuKpbNNyY/edit) in the UAT phase
* Guide and assist the AA and IA in creating anonymised testing data
* Guide the AA in setting up privacy-friendly UX such as creating options for citizens to provide active opt-ins, clearly separating between terms and conditions that are compulsory and those that are voluntary, or formulating and displaying meaningful privacy notices.

### D.2.5 Stage 4 - UAT and Go-Live <a href="#_cj62zuwzif0j" id="_cj62zuwzif0j"></a>

**D.2.5.1 What happens in Stage 4?**

* UAT Sign-off & Go Live permitted for Pilot ULBs or other mandated govt bodies for delivery of services
* Setup of review & monitoring cadence.

**D.2.5.2 Owner’s Role in Stage 4**

* Guide and review solution implementation, communication/branding, training/adoption.

**D.2.5.3. To-Dos**

**Operational:**

* Assist the AA and IA in conducting training of personnel on DPP practices. Sessions can be held on use cases such as:
  * paper-based data management
  * maintaining DPP for paper-to-digital migration
  * identifying PII and classifying it,
  * creating a data usage policy,
  * monitoring access to sensitive data,
  * implementing encryption for data in transit and at rest,
  * regularly testing security measures,
  * providing general training and awareness around data protection,
  * using multi-factor authentication,
  * ensuring secure disposal of confidential information,
  * updating security policies on a regular basis
* Check for any practices for DPP that are missed out or are not completely implemented into the designs
* Set up a check for DPP compliance within the program review process
* Assist the AA and IA in working on any issues or problems that arose from the UAT testing on DPP

### D.2.6 Stage 5 - Statewide / ULB-wide Rollout <a href="#_9w8g79m1za4n" id="_9w8g79m1za4n"></a>

**D.2.6.1 **_**What happens at Stage 5?**_

**-**Statewide Rollout in batches

**-** Help desk effectiveness assured

**-** Critical bugs fixed

**-** Program success metrics tracking kick-started&#x20;

_**D.2.6.2 What does the platform owner do at stage 5?**_

* Guide and review in change management, incident management, adoption and awareness plans

**D.2.6.3 To-Do’s:**

**Operational:**

* Establish clear procedure, based on MOU and in compliance with existing legal requirements, to ensure that in case any data is shared with the platform owner (e.g. for support or bug-fixing purposes):\
  \- A secure channel is used for sharing this data\
  \- The data is shared by a person who has the authority to share it\
  \- The AA has given authorisation to the platform owner to receive it\
  \- No other/unauthorised person receives or accesses this data\
  \- Data is not retained after the purpose for its sharing has been completed/achieved
* Assist the AA team and ULB employees in standardizing role creation, logins and access controls in change management

**Advisory**

* Encourage AA to ensure:\
  \- Minimal, purposeful data is collected\
  \- Data collected, if sensitive, is encrypted and masked by default\
  \- ‘One role, one login’ and such login must not be shared with anyone other than the authorised role\
  \- Make citizens aware of the data policy and display it on the UX\
  \- Retain data with a documented purpose\
  \- Ensure all DPP design features are working and used correctly ( encryption, audit login records)
* Assist the AA team in creating awareness on DPP practices through training workshops and guide the IA in conducting such workshops
* Help the AA maintain and manage any DPP issues or data security issues (assist in incident management).
* Become an advisory point of contact for the AA for any data security or privacy issue.

### D.2.7 Stage 6 - Sustenance and Maintenance <a href="#_l1s971qcvo39" id="_l1s971qcvo39"></a>

**D.2.7.1 What happens at Stage 6?**

* The first batch of ULBs have been made live after the Pilot.
* There is the adoption of the platform in the program’s jurisdictional zone and amongst its ULB employees and citizens.

**D.2.7.2 What does the platform owner do at Stage 6?**

* Support and guidance in continued adoption
* Ad-hoc assistance is required in troubleshooting problems

**D.2.7.3 To Do’s**

**Operational**

* Assist if there is any issue or doubt that arises in data management, access controls, or security of the platform
* If permitted, regularly scan for vulnerabilities and patch systems and applications to minimize the risk of a breach

**Advisory**

* Guides AA and IA in better data confidentiality and privacy management.
* If AA and IA insist, take part in leading training programs for employees on best data practices.&#x20;

[^1]: Information Technology (Indian Computer Emergency Response Team and Manner of Performing Functions and Duties Rules, 2013, Sec. 2(i), defines cyber security breaches as “_unauthorised acquisition or unauthorised use by a person as well as an entity of data or information that compromises the **confidentiality**, integrity, or availability of information maintained in a computer resource.”_. - [https://www.cert-in.org.in/PDF/G.S.R\_20(E).pdf](https://www.cert-in.org.in/PDF/G.S.R\_20\(E\).pdf)\
    \- we can understand what it means in other jurisdictions like that of the UK or EU [Personal data breaches | ICO](https://ico.org.uk/for-organisations/guide-to-data-protection/guide-to-the-general-data-protection-regulation-gdpr/personal-data-breaches/)&#x20;

[^2]: This capability is present in the DIGIT platform. Implementing agencies should work with respective Administering Authorities to suitably implement this. This is currently implemented in a few modules. We are moving towards making this a universal feature across all features.&#x20;

[^3]: Article 25 and 32 of the GDPR

[^4]: Can refer to this document released by the Ministry of Home Affairs on Information Security best practices : [Information Security Best Practices (mha.gov.in)](https://www.mha.gov.in/sites/default/files/Documents\_InformationSecurity\_25062019.pdf)
