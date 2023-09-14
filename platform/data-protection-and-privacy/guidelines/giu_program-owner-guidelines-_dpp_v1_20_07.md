# GIU\_Program Owner guidelines \_DPP\_V1\_20\_07

**Data Protection and Privacy Guidelines for DIGIT Implementations**

**(Program Owners)**

_eGovernments Foundation, July 2023_

### DOCUMENT METADATA <a href="#_58vqdh9ic1z7" id="_58vqdh9ic1z7"></a>

1. Jira project #:
2. Title: Data Protection and Privacy Guidelines for DIGIT Implementations - Program Owners
3. Version #: 1
4. Version date: 20/07/23
5. Objective: Publish these guidelines on the DIGIT website
6. Audience: External
7. Author: BL , AN
8. Reviewer(s):
   1. V1:
   2. V2:
9. Review date:
10. Notes / Comments:
11. Works referred: [GIU\_Guidelines\_ DPP\_V1\_23\_02.docx - Google Docs](https://docs.google.com/document/d/1\_XJmWRqWUq83rKv\_MHWqChM-s8LulVQe/edit)

**DOCUMENT METADATA 1**

A. Scope of these guidelines 3

B.1 Stage 0 -Program set-up 4

B.1.1 What happens at this stage? 4

B.1.2 Program Owners role at Stage 0: 4

B.1.3 To-Do’s 4

B.2. Stage 1 - Program kickoff 7

B.2.1 What happens at Stage 1- 7

B.2.2 What does the Prog’s team do at Stage 1: 7

B.2.3 To-Do’s: 7

B.3 Stage 2 - Solution Design 10

B.3.1 What happens at Stage 2 - 10

B.3.2 What does the Prog team do at this stage? 10

B.3.3 To-Do’s: 10

B.4 Stage 3 - Customization and Configuration 11

B.4.1 What happens at this stage? 11

B.4.2 What does the Prog do at Stage 3? 12

B.4.3 To-Do’s: 12

B.5 Stage 4 - UAT and Go-Live 13

B.5.1 What happens at Stage 4? 13

B.5.2 What does the Prog team do at Stage 4? 13

B.5.3. To- Do’s 13

B.6 Stage 5 - Statewide / ULB-wide Rollout 15

B.6.1 What happens at Stage 5? 15

B.6.2 What does the Prog do at Stage 5? 15

B.6.3 To-Do’s: 15

B.7. Stage 6- SUSTENANCE & ONGOING IMPROVEMENT 16

B.7.1. What happens at Stage 6? 16

B.7.2 What does the Prog do at this stage? 16

B.7.3 To-Do’s: 16

### &#x20;<a href="#_tl7ytlot0qyl" id="_tl7ytlot0qyl"></a>

### **Scope of these guidelines** <a href="#_finvglukkilj" id="_finvglukkilj"></a>

DIGIT, an open-source platform, enables governments and service providers to provide an interdepartmental coordination and citizen-facing service delivery system - currently, in the fields of urban governance, sanitation, health, and public finance management.

As citizen data is collected and used for such governance services, data privacy and protection measures are required to ensure this data is managed responsibly and safely.

This document is created to be an online guide, providing guidelines for Program owners to maintain data privacy and protect individuals’ data.

* Readers can use this to identify the steps they must take, in their capacity as program owners, to ensure data privacy and protection in the context of a DIGIT or DIGIT-like implementation.
* It can also provide source material for privacy policies, which should be included in each portal & application.
* This is not a technical reference or documentation. It serves as a policy guideline.

References made to DIGIT are also applicable to other platforms similar to DIGIT. Not all parts of the guidelines or featured content may match the reader's platform or context, hence this document is open to be referred to in parts as needed.

These guidelines are to be read through the eyes of roles that are part of the program owners' **(Prog)** offices in the journey of adopting a DIGIT-based system or platforms similar to DIGIT in a government entity/ies.

If a government authority adopts DIGIT as a citizen service platform, then these guidelines are apt. Some points in the guidelines may not be relevant to platforms other than DIGIT in the governance ecosystem. Hence these guidelines have to be read as advisory.

The previous document in this series covered the guidelines for platform owners **(PO)**, implementing agencies **(IA)** and administering authorities **(AA)**.

_These guidelines share great similarity with the ones created for the AA_

For this document to understand what each program owner should do to safeguard data privacy and protection (**DPP)**, it is important to understand what a Prog does at each phase of the implementation of DIGIT.

_Guidelines to be read with the Digital Personal Data Protection Act, 2023_

As the Prog adopts DIGIT , it gets access to digital personal data and therefore comes into the ambit of the Digital Personal Data Protection Act, 2023 (DPDP Act)\[1]. The roles a Prog plays as per the DPDP Act, can be of a data fiduciary\[2] and/or of a data processor\[3]. Depending on the nature of control the Prog has over deciding the purpose and means of data processing shall make it either a data fiduciary and no such control shall make it a data processor. Therefore obligations for both the roles have to be considered for a Prog to remain compliant with the DPDP Act,2023.

For these guidelines we assume that the Prog processes digital personal data to provide for certain benefits, services, certificates, licenses or permits ( these cover most of the functions that DIGIT provides and are mandates of Urban Local Bodies )

### **B.1 Stage 0 -Program set-up** <a href="#_d6nd612vi81g" id="_d6nd612vi81g"></a>

**What is a program?**

A program can be a delivery of any government service/s which the AA is mandated to provide to citizens for which it requires a platform. Defining the scope of the program is within the power of an AA.

#### **B.1.1 What happens at this stage?** <a href="#_i4ysv1i2ktpu" id="_i4ysv1i2ktpu"></a>

* A Memorandum of Understanding is signed between the AA and the platform owners. A Prog can also be party to the MoU, or may be an equal power holding or subordinate entity of the AA (which signs the MOU).
* A State Program Head/Nodal Officer is appointed by the Prog
* Resources and funding for the program are identified.
* The Prog-specific procurement process is defined.
* IA team onboarding is initiated.

#### **B.1.2 Program Owners role at Stage 0:** <a href="#_3nhj8r81i7uc" id="_3nhj8r81i7uc"></a>

* Ensure onboarding of manpower and infrastructure as specified.
* Lead the setup of the program and related governance structure
* Appoint the program steering committee and nodal officers.
* Initiate the onboarding of the implementation partner.
* Initiate the onboarding of cloud infrastructure provider.
* Guide, support or enable the identification of module deployment priorities

#### **B.1.3 To-Do’s** <a href="#_o2sxxhqvmxds" id="_o2sxxhqvmxds"></a>

**Must-haves:**

* Must fold in clauses and language in the MoU or data access/sharing agreement around:
* Data confidentiality and privacy breach provisions with consequences (as prescribed under Sec 72 of the Information Technology Act, 2000)
* For strict access controls , damage accountability, and consequences for any data privacy and security breach (as prescribed under Sec 43A IT Act, 2000)

**Preferable practices:**

* Actions which the Prog should ensure are required of the IA (i.e. included as responsibilities of the IA in the contract) are:
* Maintain transparency in data practices and mandate regular reporting
* Create safeguards against non-authorized third-party access to data
* Implement appropriate security controls like encryption at source, masking of data, RBAC logins, conduct regular security audits and checks.
* Conduct periodic audits of access
* Report any data security breach to the Prog
* Regularly educate the employees of the Prog on data privacy, data ethics and data privacy.
* Conduct a risk assessment of the platform technology along with regular data protection impact assessment (DPIA). It is important that the platform owner is involved in this assessment, as they are probably the best placed to evaluate the technologies that might be used and that might involve a high risk for the rights and freedoms of people, making the DPIA necessary.
* The cloud infrastructure provider should be selected on the grounds that it:

\- Maintains and implements data protection policies.

\- Encrypts PII with private keys,

\- Conduct regular security checks and audits on data security and privacy

\- Safeguards data from being shared with unauthorized users

\- Maintains transparent data storage and governance models

### **B.2. Stage 1 - Program kickoff** <a href="#_u7fbjnxklmm" id="_u7fbjnxklmm"></a>

#### **B.2.1 **_**What happens at Stage 1-**_ <a href="#_4sqe9wpbptny" id="_4sqe9wpbptny"></a>

* Publishing of the program charter and implementation plan.
* Master data collection kickoff in Pilot ULBs (Urban Local Body)
* Cloud Infrastructure is procured
* Program branding is done (name, logo, tagline etc.)

### **B.2.2 What does the Prog’s team do at Stage 1:** <a href="#_6awpo89sejbq" id="_6awpo89sejbq"></a>

* Appoint the data collection team and initiate data collection from the Pilot ULBs/ bodies in the required format.
* Be a part of the implementation kick-off workshop or help organize it to include relevant stakeholders
* Assist in creating the program charter and implementation plan

#### **B.2.3 To-Do’s:** <a href="#_aqutoz97v3hx" id="_aqutoz97v3hx"></a>

**Must-haves:**

* Proof of consented collecting of personal data (past and future)
* Proof of source - presently held personal data and any past personal data which is to be processed is sourced from a database , register or book that is maintained by the administering authority

The DPDP Act permits the Prog to process any personal digital data of citizens for providing a benefit, subsidy, service, certificate, license or permit ( in this case any urban local body function such as birth or death certificate, property license, building plan permit etc) **subject to the below conditions** :

(i) she has previously consented to the processing of her personal data by the Administering authority or any of its instrumentalities for any subsidy, benefit, service, certificate, licence or permit; or (ii) such personal data is available in digital form in, or in non-digital form and digitised subsequently from, any database, register, book or other document which is maintained by the administering authority or any of its instrumentalities and is notified by the Central Government. All of the above must follow standards that the Central Government may set as policies to follow for processing.

Such previously consented evidence for personal data collection must be maintained for compliance.

* Include in the program charter:
* That the data provider i.e. the resident is the owner of the data.
* Include the duty of maintaining data privacy and confidentiality of data collected in the program charter to avoid any illegal breach
* Include in the implementation plan
* Access controls and data collection practices to avoid breach of privacy or confidentiality of data
* Consequences for third party unauthorized access to data
* Safeguard measures to avoid any breach of law
* Training of data collection teams in topics of safe data access, collection and storage
* Safe and audited data sharing and transfer channels of data
* Cloud infrastructure to have sufficient data safety and security features . It must have privacy by design inbuilt in its infrastructural design ( encrypted storage, tight access controls, strict data security)

**Preferable/Good practices:**

* At this stage, a best practice model of master data collection ( steps listed below) can be designed (Here, master data is the primary data needed for module functionality.)
* The master data collection model design includes:
* Collecting data only if it is needed for a specific legitimate reason and defined purpose ( data minimisation\[4] , legitimate purpose\[5] ).
* Informing residents about the legal basis and reason/purpose for their data being collected ( when collected directly from the resident)
* Data encryption and masking when data is being migrated from paper to digital or old or new digital systems
* Strategies for safe storage of data ( on paper or digitally).
* Destroying paper-based data after a defined migration period (AA or Prog to define a data deletion period post-migration).
* Maintaining dashboards that display the nature of data to be collected and their corresponding purposes and uses (for transparency and awareness of citizens).
* Embedding DPP practices in the implementation plan. For example, in the processes of data migration and data processing , the system does not permit sensitive data to be visible to unauthorized roles, strict logins are maintained, and IA employees are trained in safe data handling.
* Draft / adopt a data privacy policy.
* Ensure, through scope setting and reviews, that the IA is onboarding a team with appropriate Data privacy and protection safeguarding skill sets
* The implementation kickoff workshops includes training on purposeful master data collection (for the next stage) in an informed and transparent manner ( letting the resident know why they are collecting the data).

### &#x20;<a href="#_lfe80f4y5g09" id="_lfe80f4y5g09"></a>

### **B.3 Stage 2 - Solution Design** <a href="#_rxglyh1if8ij" id="_rxglyh1if8ij"></a>

#### **B.3.1 **_**What happens at Stage 2 -**_ <a href="#_7vju1mfpul4o" id="_7vju1mfpul4o"></a>

* Standardized ontologies (uniform terminology for easier understanding), processes and workflows are created.
* Master data collected in the desired format.
* Agreement on program-specific product customisations required.
* Detailed program plan is made and the tracking mechanism is finalised.

#### **B.3.2 What does the Prog team do at stage 2?** <a href="#_j9o0nolxzoaz" id="_j9o0nolxzoaz"></a>

* Approve standardized ontologies, processes and workflows
* Implement the policies required for work to begin on implementation
* Enable and support the IA in solution design, impact analysis, and integration analysis.
* Signs off on design and requirements

#### **B.3.3 **_**To-Do’s:**_ <a href="#_jah5sk1fyajc" id="_jah5sk1fyajc"></a>

**Must-haves:**

* Check for factors like:
* Data that includes personally identifying information **(PII)** is kept in an encrypted/ masked manner through the workflows.
* Strict data access requirements are in place (audit logs, restricted access points)
* Data policy is created to ensure compliance with the law for data protection against breach of confidentiality and privacy
* Avoid customisation, workflows, processing etc. that will cause unauthorized access to PII
* As per the DPDP Act, citizens would have a right to access\[6] on request -

(a) a summary of personal data that is being processed by the AA or the Prog and the processing activities undertaken by that Prog with respect to such personal data; (b) the identities of all other Data Fiduciaries and Data Processors with whom the personal data has been shared by the Prog, along with a description of the personal data so shared; and (c) any other information related to the personal data of such Data Principal and its processing, as may be prescribed.

As per this right, the AA must maintain a record of the personal datasets it has captured

* The above Act also empowers citizens with a right to correct, complete update and erase data . The AA must , on receiving the request of the citizen , correct the inaccurate or misleading data, complete the incomplete data,update the personal data, and also erase the data unless a specific purpose or a legal compliance requires such data to remain.

As per the above, the AA has to create processes to undertake such correction, completion, erasure or updation of data - for which keeping an audit log of what data is collected, why, for how long and where is crucial.

**Preferable/Good practices:**

* Conduct a risk assessment of the customizations checking for risks and harms leading to breach of confidentiality or data privacy. The assessment will take into consideration the impact that data use may have on an individual(s) and/or group(s) of individuals, whether known or unknown at the time of data use\[7].
* Push for configurations to include the feature of asking for feedback from citizens when the platform proceeds for a UAT. Citizens are asked for feedback on how data is being handled and whether they are aware of why their data is being used.
* Ensure that service level agreements include security checks at each level of implementation of the platform for data to be kept secure and safe.
* Define a data retention period, keeping in mind purpose and legal requirements.

### &#x20;<a href="#_tdytr1a58bo4" id="_tdytr1a58bo4"></a>

### **B.4 Stage 3 - Customization and Configuration** <a href="#_bdthvay7dk5r" id="_bdthvay7dk5r"></a>

#### **B.4.1 **_**What happens at this stage?**_ <a href="#_ck00xcjiwj24" id="_ck00xcjiwj24"></a>

* Configured/Customized product is created that is ready for UAT.
* Monitoring Reports and Dashboards are ready (to understand rollout of modules)
* Product artifacts like user guides are created.
* Identification of participants for UAT session

#### **B.4.2 What does the Prog do at Stage 3?** <a href="#_uk7d8ovf8mon" id="_uk7d8ovf8mon"></a>

* Supervises the master data cleaning and validation.
* Enables collection of ULB-specific baseline data to measure performance and adoption.
* Identifies ULB-level Nodal officers for regular support.

#### **B.4.3 To-Do’s:** <a href="#_w8u3x0tu6any" id="_w8u3x0tu6any"></a>

**Must-haves:**

* All data related processes at this stage are undertaken while maintaining the confidentiality of the data (masking, restricted access, role-based access control).
* Testing data should not include PII
* User guides have clear steps on data access and sensitive data management.
* Consequences of unauthorized access and breach of privacy and confidentiality are made clear to all team members.
* Any customization or configuration that could lead to a breach of data and affect the data privacy of citizens is rejected.
* Ensure that the privacy policy is visible on the UX (privacy policy must be easy to understand and small - a sample privacy policy can be found [here](https://docs.google.com/document/d/1TlGUZg5stbJPU5ZXUEiLM9LcBCkjmKjsjmEEPxsYCs4/edit?usp=sharing))

**Preferable/ Good practices:**

* Ensure that the nodal officers are made aware (through training and workshops) of the importance of data privacy and protection, and trained to manage data securely
* Check for feedback from employees on access mechanisms and delivering services with proposed levels of data access, masking, etc. (Can use this [sheet](https://ico.org.uk/media/for-organisations/documents/4024005/information-rights-bingo.pdf) as an activity to assess how they are ensuring the privacy rights of residents.)

### **B.5 Stage 4 - UAT and Go-Live** <a href="#_cq77r5nnla5m" id="_cq77r5nnla5m"></a>

#### **B.5.1 **_**What happens at Stage 4?**_ <a href="#_9hhmj0s63k6e" id="_9hhmj0s63k6e"></a>

* The User acceptance test is conducted, a sign-off and go-live permission is given for identified Pilot ULBs or other mandated govt bodies for delivery of services
* Setup of review & monitoring cadence.

#### **B.5.2 What does the Prog team do at Stage 4?** <a href="#_kigm528x6abx" id="_kigm528x6abx"></a>

* Enables or conducts user acceptance testing
* Organizes ULB employee training workshops
* Sets up help desks and support mechanism for ULB’s
* Lead the UAT / pilot / Go-live as required along with training of key client personnel

#### **B.5.3. To- Do’s** <a href="#_22qg94blmhiy" id="_22qg94blmhiy"></a>

**Must-haves:**

* Training of employees on data safety and privacy practices
* Conduct data security checks before signing off on the UAT.

A data security checklist should include-

* Personally identifying information **(PII)** data encrypted/masked when shared
* Data is stored in safe databases
* Employees don’t openly share access logins
* Limited roles have access to PII,
* Employees trained in incident reporting,
* Data protection policy for hardware protection, external media devices
* The monitoring and evaluation cadence has data privacy and protection as a threshold for security check. A report is submitted to Prog as part of the review and monitoring cadence for DPP:
* The privacy policy is uploaded and displayed
* The privacy policy clearly states who is responsible for the personal data and how that official can be contacted
* Assessments for data breaches and security checks are planned to be regularly performed
* Data processing and sharing agreements have been established with all third parties that will process personal data
* The software and infrastructure regularly undergoes security risk and threat analysis
* The program has a privacy education/awareness training
* SOP for security incidents affecting personal data is established
* The amounts of personal data that can be collected have been minimized
* The purpose for data collection has been defined to be as specific as possible
* The data is retained only till there is a need for it
* There are checks on data-sharing, with verification that sharing is legally authorised and approved by the appropriate official

**Preferable practices:**

* The help desks provide simple material to explain to citizens or employees the concepts of DPP. These help-desks serve as one stop spots for citizens and employees to understand DPP concepts like data privacy methods, masking, limited and purposeful data sharing. Therefore the help-desk representative is trained well in DPP concepts and use cases before the platform goes live. They also become the first stop for any incident to be reported on data privacy breach.

### &#x20;<a href="#_i6wqf8x24rg" id="_i6wqf8x24rg"></a>

### **B.6 Stage 5 - Statewide / ULB-wide Rollout** <a href="#_io252m2fjut6" id="_io252m2fjut6"></a>

#### **B.6.1 **_**What happens at Stage 5?**_ <a href="#_kyep9xxv6c1z" id="_kyep9xxv6c1z"></a>

* Statewide Rollout in batches
* Help desk effectiveness assured
* Critical bugs fixed
* Program success metrics tracking kick-started&#x20;

#### **B.6.2 What does the Prog do at Stage 5?** <a href="#_m7caai2edcq2" id="_m7caai2edcq2"></a>

* Leads the rollout, training, and change management workshops,
* Monitors training activities

#### **B.6.3 To-Do’s:** <a href="#_klgpkmocdu96" id="_klgpkmocdu96"></a>

**Must-haves:**

* Receive regular reports on any data breaches
* Maintain a check on access controls
* Regularly update and train employees on safeguards

**Preferable/Good practices:**

* Maintain transparent practices for data governance
* Work with employees to apply their DPP training in their functions.
* Receive reports on Privacy Impact assessments (including gap assessments) and data security audits to check whether the program is safeguarding DPP. Can refer to Appendix B in this [memo](https://docs.google.com/document/d/10bsSWEmf2ebjNpGBs-BLXAVyL-sVFQ901GzuKpbNNyY/edit?usp=sharing) to understand if the Prog has considered global practices and principles of data protection and privacy for adoption.
* Maintain active feedback loops to provide solutions for any anticipated privacy or data protection issues that may arise
* Manage data migration processes (while transitioning from old / existing systems to new platform-based systems) to maintain data safety and privacy best practices , i.e data masking, encryption, data deletion,strict access controls , etc.

### **B.7. Stage 6- SUSTENANCE & ONGOING IMPROVEMENT** <a href="#_1aj7kypxyzez" id="_1aj7kypxyzez"></a>

#### **B.7.1. What happens at Stage 6?** <a href="#_pyngu51yqgh7" id="_pyngu51yqgh7"></a>

* The first batch of ULBs have been made live after the Pilot.
* There is the adoption of the platform in the program’s jurisdictional zone and amongst its ULB employees and citizens.

#### **B.7.2 What does the Prog do at this stage?** <a href="#_6qsohvpqlcda" id="_6qsohvpqlcda"></a>

* Maintains the adoption tracking & review cadence.
* Drives the adoption of the system.
* Implements multi-channel awareness campaigns.

#### **B.7.3 To-Do’s:** <a href="#_lgfnqd8qitk4" id="_lgfnqd8qitk4"></a>

**Must-haves:**

* Prog checks for all of the above data privacy and protection measures being maintained and continuously running
* Prog reviews implementation of DPP practices and reviews issues in adoption by employees. Prog tries to balance service delivery and data privacy and security.

**Preferable/Good practices:**

* Conduct awareness campaigns for residents on their right to data protection and privacy, and DPP measures being taken in the program.
* Organizes sessions for employees and contractors of Prog (and IA / SA if relevant) on DPP measures, principles, practices, etc.
* Create awareness materials like posters, videos, brochures etc.

1. [Digital Personal Data Protection Act 2023.pdf (meity.gov.in)](https://www.meity.gov.in/writereaddata/files/Digital%20Personal%20Data%20Protection%20Act%202023.pdf) ↑
2. Sec 2 (i) “Data Fiduciary” means any person who alone or in conjunction with other persons determines the purpose and means of processing of personal data ↑
3. Sec 2 (k) “Data Processor” means any person who processes personal data on behalf of a Data Fiduciary ↑
4. Refer to the principle of data minimisation and storage limitation [here](https://docs.google.com/document/d/10bsSWEmf2ebjNpGBs-BLXAVyL-sVFQ901GzuKpbNNyY/edit) ↑
5. For each item of data collected, stored, processed, or shared, there should be a clear purpose identified; this purpose must flow from a legitimate task that the entity collecting it (i.e. a ULB) is mandated & authorized to perform (hence, legitimate), and this purpose must be communicated to the citizen. This is closely related to the concepts of data minimisation, purpose limitation, and role-based access. ↑
6. Sec 11 of the DPDP Act, 2023 ↑
7. An assessment of harms should consider such key factors as: (i) the likelihood of occurrence of harms, (ii) potential magnitude of harms and (iii) potential severity of harms. Additionally, the assessment should take into account the digital literacy of both potential users of data and those individuals whose data is being used. ↑
