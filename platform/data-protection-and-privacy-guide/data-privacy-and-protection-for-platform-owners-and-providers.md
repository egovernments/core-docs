# Data Privacy & Protection For Platform Owners & Providers

## Scope

DIGIT, an open-source platform, provides a citizen-facing service delivery system in the fields of urban governance, sanitation, health, and public finance management. As citizen data is collected and used for such governance services, data privacy and protection measures are required to ensure this data is managed responsibly and safely.&#x20;

This page is meant to be an online guide, providing guidelines for platform owners (providers of DIGIT-like systems) to maintain data privacy and protect individuals’ data.&#x20;

* Readers can use this to identify the steps they must take as platform owners or providers to ensure data privacy and protection in the context of a DIGIT or DIGIT-like implementation.&#x20;
* It can also provide source material for privacy policies, which should be included in each portal & application.&#x20;
* This is not a technical reference or documentation. It serves as a policy guideline.

References made to DIGIT are also applicable to other platforms similar to DIGIT. Not all parts of the guidelines or featured content may match the reader's platform, hence this document is open to be referred to in parts as needed.&#x20;

## D. Guidelines&#x20;

These guidelines are to be read through the eyes of specific roles in the journey of adopting a DIGIT-based system or platforms similar to DIGIT in a government entity/ies. For each such ‘role’ , a reader can follow its tasks in a given stage of implementation of DIGIT or such platform, and the guidelines associated with that task and stage.&#x20;

It is to be noted that similar guidelines can be found for ‘data controllers’ under the General data protection regulation of Europe. There are a few basic and minimum requirements that data controllers (bodies that decide the purpose for processing data and the means used to process the data) have to comply with to ensure data protection by default (DbD and PbD) and design (data minimization, implementing safeguards for protection of data, controlled access to data, limited purposeful storage, etc). In Europe, entities are legally obligated to maintain DbD and PbD or else they are heavily penalised.

### D.1 Guidelines for all roles&#x20;

There are a few common guidelines that all roles in the platform implementation process must follow. Data security measures and practices stand out as the core/foundational guideline to follow for all roles. DPP is only possible when the systems and computer resources receiving and storing data are secure (safe from any harm).&#x20;

Some key data security measures include:

* Access control: Establish audited and controlled access for personally identifying data, including authentication and authorization mechanisms. Authorize individuals only if they have a legal basis and a legitimate purpose to access the data.
* Encryption: Encrypt PII data both in transit and at rest to protect it from unauthorized access and theft.
* Data backup and disaster recovery: Regularly backing up PII data - including auditing the need for PII - if not required then deleting the PII, and implementing disaster recovery plans to ensure that important data can be recovered in the event of a data loss or breach.
* Network security: Implement firewalls, intrusion detection and prevention systems, and other network security measures to protect against cyber threats.
* Vulnerability management: Regularly scan for vulnerabilities and patch systems and applications to minimize the risk of a breach.
* Employee education: Educate employees/contractors/personnel on the importance of data security and provide training on best practices for protecting PII.
* Physical security: Implement physical security measures, such as access controls and video surveillance, to protect against unauthorized access to data centres and other data facilities.
* Third-party security: Carefully vet third-party vendors and service providers, to ensure that they have appropriate security measures in place to protect PII.
* Incident response: Develop and test incident response plans to ensure that the organization can quickly and effectively respond to a security breach.
* Compliance: Adhere to relevant security and privacy regulations, such as the IT Act, of 2000, and its subsequent amendments and Rules. Conforming with standards such as ISO 27001 is also a good practice.

### D.2 Detailed Guidelines for Platform Owners&#x20;

The roles we cover under these guidelines are that of:

* Platform Owners (any individuals or body that creates and owns the platform which facilitates/enables the governments to provide for delivery of service)

The next document in this series covers the following stakeholders -:&#x20;

* Administering authority (AA) (the body that is mandated to provide for the government service usually an agency or department of the State government). This can include bodies like [State Program Directorate and Program Monitoring Units. ](https://niua.in/cdg/UPYOG)
* Implementation agency/ system integrator (SI)(the body that implements the platform provided by the platform owner into the administering authority’s IT systems)&#x20;
* Maintenance team (can be an additional team that gets involved after the platform is implemented in the administering authority’s systems to maintain the system)

To understand what each role should do to safeguard DPP, it is important to understand what these roles do at each phase of the implementation of DIGIT.

#### D.2.1. Stage 0 -Program set-up&#x20;

#### What is a program?

A program can be a delivery of any government service/s which the AA is mandated to provide to citizens for which it requires a platform. Defining the scope of the program is within the power of an AA.

#### D.2.1.1 What happens at this stage?&#x20;

* A Memorandum of Understanding is signed between the AA and the platform owners
* State Program Head/Nodal Officer Appointed by the AA
* Resources and funding for the program are identified.
* The AA-specific procurement process is defined.
* SI team onboarding initiated.

#### D.2.1.2 Platform Owner at Stage 0&#x20;

* Share specifications for man-power and infrastructure&#x20;
* Program setup best practices are shared
* Enablement for product, configuration, infra

#### D.2.1.3. To-Dos

**Operational**

* Any kind of agreement to be signed between the platform owners and the AA (e.g. an MoU) must have clear terms of data management, liability and governance.
* Identify the risks and necessary measures with the AA to ensure that any present or future data processing conducted by the AA is safe by the design of the platform (Conduct data protection impact assessment )&#x20;
* Inform and clearly explain the platform’s in-house data practices and in-design DPP policies and practices of the platform to the AA.
* Create and maintain data use agreements with the AA (points on the legal framework for data access, what is to be done of the data and security controls are agreed on)
* Guide and assist AAs in training  their employees in DPP practices&#x20;
* Platform team to write a pre-mortem – an imaginary article looking back from the future on the feature’s perfect launch or failure – to help the AA and SI to focus on the privacy aspects that will ensure success.&#x20;

**Advisory**

* Encourage and guide AA to adopt Privacy by Default
* Encourage AA to include DPP-enabling tech/non-tech resources in infrastructure resource planning. ( For eg - budgeting and reserving resources for data privacy impact assessments on the modules to be deployed)
* Encourage and guide the AA team in creating their data privacy and protection policy&#x20;
* Encourage the AA to appoint privacy and data security-compliant Implementation teams or SI’s.

**Technical**

* Do not offer any service module unless it is not compliant with relevant data privacy and protection  (DPP) checks/standards and systems  (the reader may check the checklist in Appendix B of this [memo](global-best-practices-for-data-protection-and-privacy.md) to refer for DPP compliance)

#### D.2.2 Stage 1 - Program kickoff&#x20;

#### D.2.2.1 What happens at Stage 1

* &#x20;Publishing of the program charter and implementation plan.
* &#x20;Master data collection kickoff in Pilot ULBs
* Cloud Infrastructure is procured
* Program branding is done (name, logo, tagline etc.)&#x20;

#### D.2.2.2 Platform Owner’s Role at Stage 1&#x20;

* Guide and review manpower, infra, and program governance structure. Provide a stable platform version.

#### D.2.2.3 To-Dos

**Operational**

* Assist and encourage the AA team in setting a standardised data collection framework ( with DPP practices like minimum personal data collected, masked data to be maintained, collecting citizen consent before collecting data, create awareness on the legitimacy and requirement for data collected from citizens..)
* Assist the AA and SI team in placing DPP principles and practices as a priority in the program charter
* Onboarded implementation partner or SI  must comply with data principle practices enlisted [here](global-best-practices-for-data-protection-and-privacy.md)
* Implementation kick-off workshop must include training in DPP practices ( minimum data collection, masking at field level, etc)
* Encourage field-level ULB data collection team to collect the consent of citizens while collecting data and informing them on the purpose of their data being collected.

**Advisory**

* Encourage the AA team to keep DPP as a foremost priority in the implementation plan
* Advise the AA teams to collect as minimal data as possible to comply with the data minimisation principle ( at the master data collection level)
* Encourage within the AA employees, the behaviour of adopting privacy enhancing technology (PET). Highlight the increase of trust and reputation through the adoption of PETs.

**Technical**

* Procured cloud infrastructure providers must be given training for DPP practices (especially to understand their data storage/ retention period, nature of retention and purposes)

### D.2.3 Stage 2 - Solution Design

#### D.2.3.1 What happens at Stage 2&#x20;

* Standardized ontologies (uniform terminology for easier understanding), processes and workflows are created.
* Master data collected in the desired format.
* Agreement on AA - specific product customisations are required.&#x20;
* A detailed program plan is made and the tracking mechanism is finalised.&#x20;

#### D.2.3.2 Platform Owner’s Role at Stage 2

* Guide and review the platform's extension/customisation, data collection/migration, and accepted best practices.

#### D.2.3.2 To-Dos

**Operational**

* Guide and push for the inclusion of data privacy and protection definitions and practices within the service delivery module ontologies.&#x20;

While standardizing processes and workflows, encourage the AA and SI teams to:

* Conduct a Privacy Impact Assessment (PIA): To identify the personal data that is being collected, processed, and stored, and to assess the risks associated with these operations. This will help identify any privacy issues that need to be addressed in the workflows.
* Develop privacy policies and procedures that outline the AA’s commitment to data privacy, and specify the measures that will be taken to protect personal data. These policies and procedures should be integrated into the workflows of the modules.
* Train employees on data privacy principles, such as data minimization and privacy by design. This will help ensure that they are aware of the importance of protecting personal data and the measures they need to take to do so.
* Assist the AA and SI in designing a clear data breach response plan  (sets out procedures and clear lines of authority for responding to data breaches)
* Advice to regularly monitor and audit workflows to ensure that privacy policies and procedures are being followed and that personal data is being protected. This will help identify any areas where improvements can be made to ensure that data privacy is embedded in the workflows of the organization. Create a role that does the above.
* Assist the AAs in updating policies and procedures: Regularly review and update privacy policies and procedures in response to changes in technology, and data privacy regulations. This will help ensure that the state stays up-to-date with best practices for protecting personal data.
* Assist and guide the AA and SIs towards purposeful data migration and collection
* Insist for personally identifiable information in the master data to be only stored in an encrypted manner ( advise the AA on designing a DPP-based format for master data collection)
* Any changes or additions requested by the AA team that is contrary to any of the data privacy and protection regulations or principles must not be agreed to.

**Advisory**

* Advise maintaining a data security ISO standardization as a prerequisite (ISO 27001 is recommended)
* Encourage the AA team to create strict access to workflows ( audit log-ins, strict access logins)
* Encourage better privacy by design customisations ( for eg masking from the point of collection

**Technical**

* Implement privacy-enhancing technologies (PeTs), such as encryption, anonymization, and access control systems, to protect personal data. These technologies should be integrated into the workflows of the module to ensure that personal data is protected throughout its lifecycle.

#### D.2.4 Stage 3 - Customisations and Configuration

#### D.2.4.1 What happens at this stage?

* Configured/Customized product is created that is ready for UAT ( User acceptance testing).
* Monitoring Reports and Dashboards are ready ( to understand the rollout of the modules)
* Product artefacts like user guides are created.
* Identification of participants for the UAT session

#### D.2.4.2 Role of Platform Owner at Stage 3

* Guide and review architecture, solutions and UX.&#x20;
* Support in the configuration/customisation processes

#### D.2.4.3 To-Dos

**Operational**

* Create user guides to maintain privacy as default ( For eg - the [checklist in this document ](global-best-practices-for-data-protection-and-privacy.md)can be used as a user guide to understand compliance with privacy principles)

**Advisory**

* Ensure and advise for DPP-related privacy by default features to be installed in the software.
* Guide in the protection of hardware from security threats
* Ensure and assist the AA in making sure that all the security access and logins have been set up&#x20;
* Advice the state to include data privacy and protection [checklist questions](global-best-practices-for-data-protection-and-privacy.md) in the UAT phase&#x20;
* Guide and assist the AA and SIs in creating anonymised testing data&#x20;
* Guide the AA in setting up privacy-friendly UX such as creating options for citizens to provide active opt-ins, clearly separating between terms and conditions that are compulsory and those that are voluntary, and formulating or displaying meaningful privacy notices.

#### D.2.5 Stage 4 - UAT and Go-Live

#### D.2.5.1 What happens at Stage 4?

* UAT Sign-off & Go Live permitted for Pilot ULBs or other mandated govt bodies for delivery of services
* Setup of review & monitoring cadence.

#### D.2.5.2 Owner’s Role at Stage 4

* Guide and review solution implementation, communication/branding, training/adoption.

#### D.2.5.2. To-Dos

**Operational**

* Assist the AA and SI’s in conducting training of personnel on DPP practices. Sessions can be held on use cases such as:
  * paper-based data management
  * maintaining DPP for paper-to-digital migration&#x20;
  * identifying PII and classifying it,
  * creating a data usage policy,&#x20;
  * monitoring access to sensitive data,&#x20;
  * implementing encryption for data in transit and at rest,&#x20;
  * regularly testing security measures,&#x20;
  * providing general training and awareness around data protection,&#x20;
  * using multi-factor authentication, -ensuring secure disposal of confidential information,&#x20;
  * regularly updating security policies
* Check for any practices for DPP that are missed out or are not completely implemented into the designs&#x20;
* Set up a review process / add a DPP checklist within the already existing review process&#x20;
* Assist the AA and SI team in working on any issues or problems that arose from the UAT testing on DPP

#### D.2.6 Stage 5 - Statewide / ULB wide Rollout

#### D.2.6.1 What happens at Stage 5?

\-Statewide Rollout in batches

\- Help desk effectiveness assured

\- Critical bugs fixed

\- Program success metrics tracking kick-started&#x20;

#### D.2.6.2 What does the platform owner do at stage 5?

* Guide and review in change management, incident management, adoption and awareness plans

#### D.2.6.2 To-Dos

**Operational**

* Assist the AA team in creating awareness of DPP practices through training workshops and guide the SI’s in conducting such workshops
* Help the AA maintain and manage any DPP issues or data security issues (assist in incident management).&#x20;
* Become the advisory Point of contact for the AA for any data security or privacy issue.
* Establish clear procedure, based on MOU and in compliance with existing legal requirements, to ensure that in case any data is shared with the platform owner (e.g. for support or bug-fixing purposes):\
  \- A secure channel is used for sharing this data\
  \- The data is shared by a person who has the authority to share it\
  \- The AA has given authorisation to the platform owner to receive it\
  \- No other/unauthorised person receives or accesses this data\
  \- Data is not retained after the purpose for its sharing has been completed/achieved
* Assist the AA team and ULB employees in standardizing role creation, logins and access controls in change management&#x20;

**Advisory**

* Encourage AA to ensure:\
  \- Minimal, purposeful data is collected\
  \- Data collected, if sensitive, is encrypted and masked by default\
  \- ‘One role, one login’ and such login must not be shared with anyone other than the authorised role\
  \- Make citizens aware of the data policy and display it on the UX\
  \- Retain data with a documented purpose\
  \- Ensure all DPP design features are working and used correctly ( encryption, audit login records)\
