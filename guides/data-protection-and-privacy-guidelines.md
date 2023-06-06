---
description: Data protection and privacy guidelines for DIGIT implementations
---

# Data Protection & Privacy Guidelines

## Scope

DIGIT, an open-source platform, provides a citizen-facing service delivery system in the fields of urban governance, sanitation, health, and public finance management. As citizen data is collected and used for such governance services, data privacy and protection measures are required to ensure this data is managed responsibly and safely.&#x20;

This page is meant to be an online guide, providing guidelines for platform owners (providers of DIGIT-like systems) to maintain data privacy and protect individuals’ data.&#x20;

* Readers can use this to identify the steps they must take as platform owners or providers to ensure data privacy and protection in the context of a DIGIT or DIGIT-like implementation.&#x20;
* It can also provide source material for privacy policies, which should be included in each portal & application.&#x20;
* This is not a technical reference or documentation. It serves as a policy guideline.

References made to DIGIT are also applicable to other platforms similar to DIGIT. Not all parts of the guidelines or featured content may match the reader's platform, hence this document is open to be referred to in parts as needed.&#x20;

## A. Basic Terms & Definitions&#x20;

#### What is data?

Data is the information collected from an individual or about an individual. In DIGIT, data can be any information pertaining to a citizen, which is required for delivery of service and/or information exchange flow amongst citizen, employee, vendor and administrator. Data and information are interchangeably used.

#### What is data security?&#x20;

Data security is the act of securing and safeguarding data. Active measures are taken to protect the data from misuse or harm. Such actions can be pre-emptive i.e. security steps taken before the data is collected or the actions could be reactive i.e. steps taken after the platform has been set up. DIGIT recommends pre-emptive steps as a best practice, and has[ data security](https://core.digit.org/focus-areas/data-security) measures embedded within its design.

#### What is data privacy?

Data privacy means keeping the data in the control of the individual and allowing the individual to decide what is to be done with their data. Data that is collected or shared without the consent of an individual, especially when exposed and combined with other data points, can cause citizens to be identified and targeted. That’s why protecting data indirectly protects the citizen as well.

Data Privacy requires protecting the data from unwarranted viewing, use, or sharing. This involves taking steps such as data minimisation (only collecting and storing data that serves a defined purpose), encrypting data, restricting access to the data, and/or masking what data is visible to users. DIGIT is designed to maintain the privacy of citizens and protect data by taking all the steps mentioned above and [more](https://core.digit.org/focus-areas/privacy).&#x20;

#### What is personally identifiable information (PII)?

PII stands for personally identifiable information or is also interchangeably used as personal data. Personal data is basically any information that makes a person either identifiable. This consists of data that is unique for each person. When it is combined with other forms of data, it can help in identifying a person. For example, our biometric information, credit card details, passport details etc. are all PII.&#x20;

#### What is a  personal data breach?

A personal data breach means a breach of security leading to the accidental or unlawful destruction, loss, alteration, or unauthorised disclosure of, or access to, personal data. This includes breaches that are the result of both accidental and deliberate causes. It also means that a breach is more than just about losing personal data.&#x20;

Personal data breaches can include:

* access by an unauthorised third party;
* deliberate or accidental mishaps with data by a  handler, collector or processor;
* sending personal data to an incorrect recipient;
* computing devices containing personal data being lost or stolen;
* alteration of personal data without permission; and
* loss of availability of personal data.

## B. What kind of data does DIGIT handle?

The DIGIT platform does not handle data unless and until it is implemented in a particular context. Each implementation of DIGIT handles a combination of non-personal data and PII; the latter may further be classified into data which, in itself, identifies the individual to whom it pertains (“identified”) and data which, if combined with other data, can identify the individual to whom it pertains (“identifiable”).

### B1. Personal Data / PII of Residents/citizens

Specific data recorded in various applications that may be implemented on DIGIT include name, parent/spouse’s name, mobile number, city, email id, date of birth, door no/address, and pin code. Data from administrative record systems, such as revenue survey number or other property identifier, connection number, meter number etc. may also be recorded. In the event a person makes payments to the local government, information related to the payment, such as transaction number may also be recorded.

Any personal data collected and stored in DIGIT is encrypted, both in storage and transmission. When displayed, this data is to be masked by default. Users can request to unmask data; if they have the appropriate authorisation, they will be able to view the unmasked data, and this request to unmask will be recorded in an audit log. &#x20;

DIGIT implementations are used to provide government services to residents of a given city, town, village etc. The data collected, as described above, are necessary for the delivery of such services. When a resident approaches their local government for a particular service, they can be required to share, or allow access to, the information necessary to provide that service.

### B2. Personal Data / PII of Employees

DIGIT implementations also collect, store, process, and share information pertaining to employees of local government or other government agencies. Specific information can include name, age, gender, details of spouse or dependents, address, administrative details such as employee ID or other reference numbers, as well as information on bank accounts (used for processing salaries or pensions).&#x20;

As employers, local governments may be required to maintain certain information on their employees and pensioners for tax purposes, such as PAN numbers; this information may be recorded and shared as well.

### B3. Non-Personal Data

DIGIT implementations may derive, store, process, and share transactional data, which describes the progress of any ongoing task (e.g. any service requested by a resident) through the systems of the local government or other government agency. This can include information about the specific role to whom a given task is assigned (or with whom it is pending), the amount of time elapsed on processing / completing a given request (or task / sub-part thereof), and whether this task has been completed within the benchmark or designated amount of time. It can also include details about the channel through which a particular request was received, such as the ULB counter, service centre, website, helpline, mobile app, chatbot, etc.

DIGIT implementations may derive, store, process, and share aggregated data. These aggregates are derived from the transactional data. This includes data such as aggregate or cumulative revenue collection, the aggregate or cumulative number of service requests, the percentage of requests resolved within the benchmark time period, etc. The above data may be further analysed and presented in terms of the type of collection, request, or complaint, the channel through which it was received, etc. &#x20;

DIGIT implementations may collect, store, process, and share telemetry data, which studies how much time is spent on a given screen or field in a workflow/user interface (UI). Such data is normally processed and shared in aggregate, and not used to identify specific individuals. In the event that specific individuals are sought to be identified, such as for user research, their consent will be sought for the further processing or sharing of their data.

### B4. General Compliance with Legal Obligations and Global Best Practices

DIGIT is designed to enable compliance with requirements under Indian law, as well as global best practices, as follows:

* The requirement for a legal basis for the collection, storage, processing, use, and sharing of such data is fulfilled by the mandate of the local government or other government agency to provide a particular service.
* The requirement of a legitimate purpose is also met by the mandate of the local government or other government agency to provide that particular service.
* The requirement of proportionality is generally met by only collecting or accessing such data as is necessary for providing that particular service. This is also in line with the global best practice of data minimisation.
* The requirement for safeguards is generally met by the security and privacy measures, such as encryption and masking, described above; it is further met by implementing role-based access controls, which are aligned with the global best practice of differentiated access.&#x20;
* The requirement for safeguards is further served by providing itemised notice, and by enabling any person to view what data of theirs has been collected/processed/shared (including the purpose for such collection/processing/sharing). Such provision of notice and visibility is further in line with global best practices of notice & user control. Such notice can only be provided in the context of a DIGIT implementation, and eGov provides a draft [privacy policy](https://docs.google.com/document/d/1TlGUZg5stbJPU5ZXUEiLM9LcBCkjmKjsjmEEPxsYCs4/edit?usp=sharing) to implementing entities.
* With respect to employees and pensioners, the requirements for legal basis, legitimate purpose, and proportionality are generally met by collecting, storing, processing, using, and sharing only such information as is relevant for assigning roles and administrative responsibilities, processing salaries or pensions, and completing any mandatory tax-related reporting.

## C. Who handles data in the DIGIT lifecycle?

The datasets flow from a point of service (POS) device to the integrator system, and from the backend of the integrator system to the DIGIT platform.&#x20;

Data may be entered into a DIGIT registry or database in one of four ways:

* A citizen directly enters the data into a web portal, application, chatbot etc., as part of requesting government services.&#x20;
* A local government or other government entity employee or contractor may enter the data into the system on their allocated device (computer at the service counter, mobile application in the field, etc.), as part of their work in providing government services.
* Data is migrated/ported from some previous systems, including paper-based systems, especially during the initial setup of the DIGIT-based system. This is also known as data migration.
* Data is shared in digital formats, such as through APIs or machine-readable spreadsheets, from some other system or platform to a system running on DIGIT.

Each module in DIGIT has different departmental employees feeding data at the field level.&#x20;

These roles and their levels of access are determined by the administering authority (typically a local or state government), as part of the initial setup of the DIGIT-based system.

Existing roles may be modified and new roles may be created by persons who are authorised to act as system administrators following the initial setup. This means that the administering authority (or a person delegated this power by the administering authority) recognises these roles, and provides them with login credentials to access and collect citizen data for the delivery of government services.&#x20;

Examples of such roles that are recognised by our platform are: “EMPLOYEE", "CITIZEN",” DOC\_VERIFIER", ”FIELD\_INSPECTOR", ”APPROVER", "CLERK".

In any given implementation of DIGIT, the administering authority (local or state government) is understood to have responsibility for the data and is treated as the main data fiduciary with respect to the data of residents that is collected, stored, processed, used, or shared through or by the DIGIT-enabled tools or systems in use in its jurisdiction.&#x20;

The primary responsibility for ensuring compliance with legal obligations and best practices with respect to data security, data protection, and privacy is thus that of the administering authority. To the extent that any other party (including eGov Foundation) serves as an agent of the administering authority,  they are similarly considered responsible for ensuring such compliance, to the extent relevant to the tasks that they are performing.

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

\
\
\
\


####
