# Introduction To Data Privacy & Protection Guidelines

## A. Basic Terms & Definitions

#### What is data?

Data is the information collected from an individual or about an individual. In DIGIT, data can be any information pertaining to a citizen, which is required for delivery of service and/or information exchange flow amongst citizen, employee, vendor and administrator. Data and information are interchangeably used.

#### What is data security?&#x20;

Data security is the act of securing and safeguarding data. Active measures are taken to protect the data from misuse or harm. Such actions can be pre-emptive i.e. security steps taken before the data is collected or the actions could be reactive i.e. steps taken after the platform has been set up. DIGIT recommends pre-emptive steps as a best practice, and has[ data security](https://core.digit.org/focus-areas/data-security) measures embedded within its design.

#### What is data privacy?

Data privacy means keeping the data in the control of the individual and allowing the individual to decide what is to be done with their data. Data that is collected without consent of an individual, when exposed and combined with other data points can cause citizens to be identified and targeted. That’s why protecting data indirectly protects the citizen as well.

Data Privacy requires protecting the data from unwarranted viewing or use. This involves taking steps such as masking or encrypting data, restricting access to the data, collecting and storing data that serves a defined purpose. DIGIT is designed to maintain the privacy of citizens and protect data by taking all the steps mentioned above and [more](https://core.digit.org/focus-areas/privacy).&#x20;

#### What is personally identifiable information (PII)?

PII stands for personally identifiable information or is also interchangeably used as personal data. Personal data is basically any information that makes a person either identifiable. This consists of data that is unique for each person. When it is combined with other forms of data, it can help in identifying a person. For example, our biometric information, credit card details, and passport details are all PII.&#x20;

#### What is a  personal data breach?

A personal data breach means a breach of security leading to the accidental or unlawful destruction, loss, alteration, or unauthorised disclosure of, or access to, personal data. This includes breaches that are the result of both accidental and deliberate causes. It also means that a breach is more than just about [losing personal data](#user-content-fn-1)[^1].&#x20;

Example:

Personal data breaches can include:

* access by an unauthorised third party;
* deliberate or accidental action (or inaction) by a data handler or collector or processor;
* sending personal data to an incorrect recipient;
* computing devices containing personal data being lost or stolen;
* alteration of personal data without permission; and
* loss of availability of personal data

## B. What Kind Of Data Does DIGIT Handle?

DIGIT handles a combination of non-personal data and PII. Personal data may further be classified into data which, in itself, identifies the individual to whom it pertains (“identified”) and data which, if combined with other data, can identify the individual to whom it pertains (“identifiable”).

### B1. Personal Data / PII of Residents/citizens

Specific data recorded in various applications that may be implemented on DIGIT include name, parent/spouse’s name, mobile number, city, email id, date of birth, door no/address, and pin code. Data from administrative record systems, such as revenue survey number or other property identifier, connection number, meter number etc. may also be recorded. In the event a person makes payments to the local government, information related to the payment, such as transaction number may also be recorded.

Any personal data collected and stored in DIGIT is encrypted, both in storage and transmission. When displayed, this data is to be masked by default. Users can request to unmask data; if they have the appropriate authorisation, they will be able to view the unmasked data, and this request to unmask will be recorded in an audit log. &#x20;

DIGIT is used to provide government services to residents of a given city, town, village etc. The data collected, as described above, are necessary for the delivery of such services. When a resident approaches their local government for a particular service, they can be required to share, or allow access to, the information necessary to provide that service.

### B2. Personal Data / PII of Employees

DIGIT also collects, stores, processes, and shares information pertaining to employees of local government or other government agencies. Specific information can include name, age, gender, details of spouse or dependents, address, administrative details such as employee ID or other reference numbers, as well as information on bank accounts (used for processing salaries or pensions).&#x20;

As employers, local governments may be required to maintain certain information on their employees and pensioners for tax purposes, such as PAN numbers; this information may be recorded and shared as well.&#x20;

### B3. Non-Personal Data

DIGIT derives, stores, processes, and shares transactional data, which describes the progress of any ongoing task (e.g. any service requested by a resident) through the systems of the local government or other government agency. This can include information about the specific role to whom a given task is assigned (or with whom it is pending), the amount of time elapsed on processing / completing a given request (or task / sub-part thereof), and whether this task has been completed within the benchmark or designated amount of time. It can also include details about the channel through which a particular request was received, such as the ULB counter, service centre, website, helpline, mobile app, chatbot, etc.

DIGIT derives, stores, processes, and shares aggregated data. These aggregates are derived from the transactional data. This includes data such as aggregate or cumulative revenue collection, the aggregate or cumulative number of service requests, the percentage of requests resolved within the benchmark time period, etc. The above data may be further analysed and presented in terms of the type of collection, request, or complaint, the channel through which it was received, etc. &#x20;

DIGIT may collect, store, process, and share telemetry data, which studies how much time is spent on a given screen or field in a workflow/user interface (UI). Such data is normally processed and shared in aggregate, and will not be used to identify specific individuals. In the event that specific individuals are sought to be identified, such as for user research, their consent will be sought for the further processing or sharing of their data.

### B4. General Compliance with Legal Obligations and Global Best Practices

DIGIT is designed to enable compliance with legal requirements (under Indian law) as well as global best practices, as follows:

* The requirement for a legal basis for the collection, storage, processing, use, and sharing of such data is thus the mandate of the local government or other government agency to provide that particular service.
* The requirement of a legitimate purpose is also met by the mandate of the local government or other government agency to provide that particular service.
* The requirement of proportionality is generally met by only collecting or accessing such data as is necessary for providing that particular service. This is also in line with the global best practice of data minimisation.
* The requirement for safeguards is generally met by the security and privacy measures, such as encryption and masking, described above; it is further met by implementing role-based access controls, which are aligned with the global best practice of differentiated access.&#x20;
* The requirement for safeguards is further served by providing itemised notice, and by enabling any person to view what data of theirs has been collected/processed/shared (including the purpose for such collection/processing/sharing), which are provisions in the DPDP Bill, 2022. Such provision of notice and visibility is further in line with global best practices of notice & user control.
* With respect to employees and pensioners, the requirements for legal basis, legitimate purpose, and proportionality are generally met by collecting, storing, processing, using, and sharing only such information as is relevant for assigning roles and administrative responsibilities, processing salaries or pensions, and completing any mandatory tax-related reporting.

## C. Who Handles Data In The DIGIT Lifecycle?

The datasets flow from a point of service (POS) device to the integrator system and from the backend of the integrator system to the DIGIT platform.&#x20;

Data may be entered into a DIGIT registry or database in one of four ways:

* A citizen directly enters the data into a web portal, application, chatbot etc., as part of requesting for government services.&#x20;
* A local government or other government entity employee or contractor may enter the data into the system on their allocated device (computer at the service counter, mobile application in the field, etc.), as part of their work in providing government services.
* Data is migrated/ported from some previous systems, including paper-based systems, especially during the initial setup of the DIGIT-based system. This is also known as data migration.
* Data is shared in digital formats, such as through APIs or machine-readable spreadsheets, from some other system or platform to a system running on DIGIT.

Each module in DIGIT has different departmental employees feeding data at the field level.&#x20;

These roles and their levels of access are determined by the administering authority (typically a local or state government), as part of the initial setup of the DIGIT-based system; existing roles may be modified and new roles may be created by persons who are authorised to act as system administrators following the initial setup. This means that the administering authority (or a person delegated this power by the administering authority) recognises these roles, and provides them with login credentials to access and collect citizen data for the delivery of government services.&#x20;

Examples of such roles that are recognised by our platform are: “EMPLOYEE", "CITIZEN",” DOC\_VERIFIER",” FIELD\_INSPECTOR",” APPROVER", "CLERK".

In any given implementation of DIGIT, the administering authority (local or state government) is understood to have responsibility for the data and is treated as the main data fiduciary with respect to the data of residents that is collected, stored, processed, used, or shared through or by the DIGIT-enabled tools or systems in use in its jurisdiction.&#x20;

The primary responsibility for ensuring compliance with legal obligations and best practices with respect to data security, data protection, and privacy is thus that of the administering authority. To the extent that any other party (including eGov Foundation) serves as an agent of the administering authority,  they are similarly considered responsible for ensuring such compliance, to the extent relevant to the tasks that they are performing. \
\


[^1]: We don’t have a per se law defining personal data breach yet, hence we can understand what it means in other jurisdictions like that of the UK or EU [Personal data breaches | ICO](https://ico.org.uk/for-organisations/guide-to-data-protection/guide-to-the-general-data-protection-regulation-gdpr/personal-data-breaches/)

