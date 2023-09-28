---
description: >-
  Data protection and privacy guidelines for DIGIT implementations
  (administrative authorities)
---

# Admin Guidelines

## **Scope**  <a href="#_finvglukkilj" id="_finvglukkilj"></a>

DIGIT, an open-source platform, enables governments and service providers to provide interdepartmental coordination and citizen-facing service delivery systems - currently, in urban governance, sanitation, health, and public finance management.

As citizen data is collected and used for such governance services, data privacy and protection measures are required to ensure this data is managed responsibly and safely.

This document is created to be an online guide, providing guidelines for administrative authorities (government entities like state government bodies, local governing bodies etc.) to maintain data privacy and protect individuals’ data.

* Readers can use this to identify the steps they must take, in their capacity as administrative authorities, to ensure data privacy and protection in the context of a DIGIT or DIGIT-like implementation.
* It can also provide source material for privacy policies, which should be included in each portal & application.
* This is not a technical reference or documentation. It serves as a policy guideline.

References made to DIGIT are also applicable to other platforms similar to DIGIT. Not all parts of the guidelines or featured content may match the reader's platform or context, hence this document is open to be referred to in parts as needed.

## **Guidelines** <a href="#_rnray17wkmt3" id="_rnray17wkmt3"></a>

These guidelines are to be read through the eyes of roles that are part of the administrative authority’s (AA) offices in the journey of adopting a DIGIT-based system or platforms similar to DIGIT in a government entity/ies.

If a government authority adopts DIGIT as a citizen service platform, then these guidelines are apt. Some points in the guidelines may not be relevant to platforms other than DIGIT in the governance ecosystem. Hence these guidelines have to be read as advisory.

Common roles of government entities that are part of the DIGIT currently are:

* Field level employee
* Line Management employee
* Administrative Officer (AO)
* Domain-level data collector
* Verifiers
* Field inspectors
* State or ULB-level head role/authority
* State administrators

This is a non-exhaustive list of roles.

There may in the future be more roles involved from a government entity while using DIGIT, including Ward-level volunteers and/or Intermediaries

_Guidelines to be read with the Digital Personal Data Protection Act, 2023_

As the AA adopts platforms like DIGIT, it gets access to digital personal data and therefore comes into the ambit of the [Digital Personal Data Protection Act, 2023](https://www.meity.gov.in/writereaddata/files/Digital%20Personal%20Data%20Protection%20Act%202023.pdf) (DPDP Act). The roles a Prog plays as per the DPDP Act, can be of a [<mark style="color:blue;">data fiduciary</mark>](#user-content-fn-1)[^1] and/or of a [<mark style="color:blue;">data processor</mark>](#user-content-fn-2)[^2]. The AA decides the purposes and means of processing the digital personal data-making it a data fiduciary under the Acr. Therefore obligations for data fiduciaries have to be considered for an AA to remain compliant with the DPDP Act,2023.

For these guidelines, we assume that the AA processes or directs the processing of digital personal data to provide for certain benefits, services, certificates, licenses or permits ( these cover most of the functions that DIGIT provides and are mandates of Urban Local Bodies )

It is to be noted that similar guidelines can be found for ‘data controllers’ under the European General Data Protection Regulation (GDPR). There are a few basic and minimum requirements that data controllers (bodies that decide the purpose for processing data and the means used to process the data) have to comply with to ensure [<mark style="color:blue;">data protection by default</mark> ](#user-content-fn-3)[^3]\(DbD and PbD) and design (data minimization, implementing safeguards for protection of data, controlled access to data, limited purposeful storage, etc). In Europe, government entities are legally obligated to maintain DbD and PbD or else they are heavily penalised.

### **B.1 Guidelines For All Roles** <a href="#_1t3h5sf" id="_1t3h5sf"></a>

There are a few common guidelines that all roles must follow.

_Data security measures and practices stand out as the core / foundational guidelines to follow for all roles._

Data Privacy and Protection **(DPP)** is only possible when the systems and computer resources receiving and storing data are secure (safe from any harm). Some key data security measures include:

* Access control: Establish audited and controlled access for personally identifying data, including authentication and authorization mechanisms. Authorize individuals only if they have a legal basis and a [legitimate purpose](../../../focus-areas/data-security/signed-data-audit.md) to access the data.
* Encryption: Encrypt PII data both in transit and at rest to protect it from unauthorized access and theft.
* Data backup and disaster recovery: Regularly backing up PII data - including auditing the need for PII - if not required then deleting the PII, and implementing disaster recovery plans to ensure that important data can be recovered in the event of a data loss or breach.
* Network security: Implement firewalls, intrusion detection and prevention systems, and other network security measures to protect against cyber threats.
* Vulnerability management: Regularly scan for vulnerabilities and patch systems and applications to minimize the risk of a breach.
* Employee education: Educate employees/contractors/personnel on the importance of data security and provide training on best practices for protecting PII.
* Physical security: Implement physical security measures, such as access controls and video surveillance, to protect against unauthorized access to data centres and other data facilities.
* Third-party security: Carefully vet third-party vendors and service providers, to ensure that they have appropriate security measures in place to protect PII.
* Incident response: Develop and test incident response plans to ensure that the organization can quickly and effectively respond to a security breach.
* Compliance: Adhere to relevant security and privacy regulations, such as the IT Act, 2000, and its subsequent amendments and Rules. Conforming with standards such as ISO 27001 is also a good practice.

### **B.2 Detailed Guidelines For Administrative Authority** <a href="#_4d34og8" id="_4d34og8"></a>

The broad roles we cover under these guidelines include:

* **Administrative authority** (**AA)** - the body mandated to provide for the government service, usually an agency or department of the State government. This can include bodies like the [State Program Directorate and Program Monitoring Units. ](https://niua.in/cdg/UPYOG)The above-listed roles (In Section D) come under this category.
* **Implementation agency -** the body that implements the platform provided by the platform owners into the administering authority’s IT systems.
* **Maintenance team** - can be an additional team that gets involved after the platform is implemented in the administering authority’s systems to maintain the system.

The previous document in this series covered the guidelines for platform owners/providers.

To understand what each role should do to safeguard DPP, it is important to understand what these roles do at each phase of the implementation of DIGIT.

### **B.2.1. Stage 0 -Program Setup** <a href="#_2s8eyo1" id="_2s8eyo1"></a>

**What is a program?**

A program can be a delivery of any government service/s which the AA is mandated to provide to citizens for which it requires a platform. Defining the scope of the program is within the power of an AA.

**D.2.1.1 What happens in this stage?**

* A Memorandum of Understanding is signed between the AA and the platform owners.
* The AA appoints a State Program Head/Nodal Officer.
* Resources and funding for the program are identified.
* The AA-specific procurement process is defined.
* SI team onboarding is initiated.

**D.2.1.2 AA and implementing agency’s role at Stage 0**

* Ensure onboarding of manpower and infrastructure as specified.
* Lead the setup of the program and related governance structure
* Appoint program steering committee and state nodal officer.
* Initiate onboarding of implementation partner.
* Initiate onboarding of Cloud infrastructure provider.
* Identify module deployment priorities

#### **B.2.1.3. To-Dos** <a href="#_o2sxxhqvmxds" id="_o2sxxhqvmxds"></a>

**Operational**

**Must-haves**

* The relevant department of the AA makes a financial commitment towards enabling data privacy, protection, and security in the system. This would solidify the operations of any measures taken for DPP.
* Spells out data use and governance terms and conditions in all agreements with partners, e.g. MoUs and contracts.
* There is a clear definition of who owns data who is responsible for data protection, extent and purpose of data access in MoUs and contracts.
* The AA documents the purposes for data collection, use and disclosure. Such purpose is to be found in a legally backed instrument or documentation (can be a government authority-sanctioned document pointing at a law/ policy that needs such data to be processed for citizen delivery purposes).
* AA ensures that the design of the platform would involve data collection and processing only if there is a defined purpose for such data being processed.
* The selection of a particular technological solution considers the risks inherent to that technology. For instance, the AA questions the risks that the tech system brings to the citizens and employees if used for service delivery. Risk assessment can be done by conducting an anticipated data protection impact assessment (DPIA). The platform owner must be involved in this assessment, as they are probably the best placed to evaluate the technologies that might be used and that might involve a high risk for the rights and freedoms of people, making the DPIA necessary.
* AA creates measures that can be put in place to reduce the anticipated risks deduced from the above, taking into account the state of the current technology and the cost of applying them.

#### **B.2.1.3.2 Role of Implementing Agency (IA)** <a href="#_9ydlwze3jrqn" id="_9ydlwze3jrqn"></a>

* The other actors that AAs engage with to provide digital government service delivery are -the Implementation Agencies **(IA)**

At this stage the AA -

* Defines how the IA must ensure that DPP practices are maintained
* Draft a working agreement which commits the IA to safeguard the data and the right of citizens to data protection and privacy
*   A few clauses which the AA could ask the IA to contractual perform are:

    * Maintain transparency in data practices (API-based data received, shared or used should be visible to the AA)
    * Report any data security breach to the AA
    * Audit and create safeguards against non-authorized third-party access to data

    Implement appropriate security controls like encryption at source, masking of data, ABAC logins, and conducting regular security audits and checks.
* Regularly educate its employees on data privacy, data ethics and data privacy.

The IA can preferably:

* In the works with the AA, include at least one person having a working knowledge of data security, privacy, and protection. IA usually have an in-house team for data security and privacy; if there is no such team, the IA may bring a person with relevant skills in for the project. In case the AA has chosen an in-house entity to implement the project rather than an IAI, the project in charge should again ensure that a person with these skills is brought in for the project.

#### **B.2.1.3.3 Role of Cloud Infrastructure Providers** <a href="#_8o60o5cxigtz" id="_8o60o5cxigtz"></a>

At stage zero, the AA begins to consider which infrastructural systems they would be adopting. Cloud infrastructure providers are usually sourced by the IA or by the AA. Choosing a cloud storage provider with safe data governance practices is important to avoid data breaches.

A few must-haves the AAs must keep in mind before selecting a cloud infrastructure provider are:

* The Cloud provider has to be compliant with the [<mark style="color:blue;">data processor's obligations</mark>](#user-content-fn-4)[^4] under the Digital Personal Data Protection Act, 2023 \[DPDP **(ACT)**]
* Maintains and implements data protection policies.
* Encrypts PII with private keys,
* Conduct regular security checks and audits on data security and privacy
* Safeguards data from being shared with unauthorized users
* Maintains transparent data storage and governance models

### **B.2.2 Stage 1 - Program kickoff** <a href="#_u7fbjnxklmm" id="_u7fbjnxklmm"></a>

#### **B.2.2.1 **_**What happens at Stage 1-**_ <a href="#_4sqe9wpbptny" id="_4sqe9wpbptny"></a>

* Publishing of the program charter and implementation plan.
* Master data collection kickoff in Pilot ULBs
* Cloud Infrastructure is procured
* Program branding is done (name, logo, tagline etc.)

#### **B.2.2.2 AA team + implementing agency (IA) role at Stage 1:** <a href="#_6awpo89sejbq" id="_6awpo89sejbq"></a>

1\. Identify Pilot ULBs (urban local bodies) or any other local governmental agency or body that is mandated to provide the government service

2\. Appoint the data collection team and initiate data collection from the Pilot ULBs/ bodies in the required format.

3\. Organize implementation kick-off workshop with relevant stakeholders of identified Pilot bodies

4\. Create the program charter and implementation plan

#### **B.2.2.3 To-Do’s:** <a href="#_aqutoz97v3hx" id="_aqutoz97v3hx"></a>

**Operational:**

**Musts**

* At this stage, a best practice model of master data collection (steps listed below) is designed - for it to be implemented when actual data is collected at the next stage. - Here master data is the primary data needed for module functionality.
* The master data collection model design includes:
* AA collects minimum personal data - they can do so by collecting personal data only once, using federated databases and interoperable systems to avoid re-collection of personal data.
* The categories of datasets the AA entity would most necessarily require to provide a service are defined and fixed. This is done so as to adopt the practice of collecting only data that is necessary for the provision of a service at the next stage.
* Data without any defined use or need is not collected ([data minimisation](../global-standards-for-all.md#global-standards-for-all), [<mark style="color:blue;">legitimate purpose</mark>](#user-content-fn-5)[^5]).
* Citizens of the ULBs are informed of the purpose of their data being collected.
* Data collected at the next stage is stored safely ( on paper or digitally). If collected on paper then once transmitted into a digital system, it is destroyed from the paper or source device.
* Dashboards displaying the nature of data to be collected and their corresponding purposes and uses are built; (for transparency and awareness of citizens).
* Specific roles are created for building accountability for safe, limited and purposeful data collection.
* The program charter clearly states that the data provider i.e. the citizen is the owner of the data.
* The implementation plan has DPP practices embedded in it. For example in the processes of data migration and data processing, the system does not permit sensitive data to be visible to unauthorized roles, strict logins are maintained, and the implementing partners' employees are trained in safe data handling.
* Proof of consented collection of personal data (past and future)- either maintained by the AA (as a data fiduciary) or maintained by a separate data processor ( any entity that processes personal data for the AA) and given to the AA as and when necessary.
* Proof of source of personal data -(past and presently held data) which is to be processed is sourced from a database, register or book that is maintained by the administering authority

The DPDP Act permits the AA to process or has processed through a processor any personal digital data of citizens for providing a benefit, subsidy, service, certificate, license or permit (in this case any urban local body function such as birth or death certificate, property license, building plan permit etc) **subject to the below conditions** :

(i) she has previously consented to the processing of her personal data by the Administering authority or any of its instrumentalities for any subsidy, benefit, service, certificate, licence or permit; or&#x20;

(ii) such personal data is available in digital form in, or in non-digital form and digitised subsequently from any database, register, book or other document which is maintained by the administering authority or any of its instrumentalities and is notified by the Central Government. All of the above must follow standards that the Central Government may set as policies to follow for processing.

Such previously consented evidence for personal data collection must be maintained for compliance.

* Before master data collection (which partly begins in this stage but is majorly conducted at the next stage), AA arranges for staff/employee training in regard to information privacy protection and awareness of relevant policies regarding citizen's privacy protection
* The AA begins to draft a privacy policy, envisioning its data governance model.
* AA ensures that the IA is onboarding a team with appropriate skill sets through reviews and initial expectation-setting
* The implementation kickoff workshops with representatives of the AAs includes training on purposeful master data collection (for the next stage) in an informed and transparent manner (letting the citizen know why they are collecting the data).
* As suggested in the above stage, a secure cloud infrastructure provider is appointed.

### **B.2.3 Stage 2 - Solution Design** <a href="#_rxglyh1if8ij" id="_rxglyh1if8ij"></a>

#### **B.2.3.1 What happens in Stage 2** <a href="#_7vju1mfpul4o" id="_7vju1mfpul4o"></a>

* Standardized ontologies (uniform terminology for easier understanding), processes and workflows are created.
* Master data collected in the desired format.
* Agreement on AA-specific product customisations is required.
* A detailed program plan is made and the tracking mechanism is finalised.

#### **B.2.3.2 What do the AA team and IA do in Stage 2** <a href="#_j9o0nolxzoaz" id="_j9o0nolxzoaz"></a>

* Standardize the ontology, processes and workflows in the states
* Initiate policy change if required
* Provide state-specific requirements, if any.
* Lead solution design, impact analysis, and integration analysis.
* Get designs and requirements signed off.

#### **B.2.3.3 To-Dos** <a href="#_jah5sk1fyajc" id="_jah5sk1fyajc"></a>

**Operational**

**Musts**

* AA conducts assessments on data governance of the prepared processes and workflows before finalisation. This includes factors like:
* Personally identifying information **(PII)** to be used in an encrypted/ masked manner through the workflows.
* Processing of data takes place only if the benefits from the use of the processed data would be proportional to the risks that such processing produces.
* Data that flows in the processes and workflows have strict access requirements
* As per the DPDP Act, citizens would have a right to access\[9] on request -

(a) a summary of personal data that is being processed by the AA and the processing activities undertaken by that AA with respect to such personal data; (b) the identities of all other Data Fiduciaries and Data Processors with whom the personal data has been shared by the AA, along with a description of the personal data so shared; and (c) any other information related to the personal data of such Data Principal and its processing, as may be prescribed.

As per this right, the AA must maintain a record of the personal datasets it has captured

* The above Act also empowers citizens with a right to correct, completely update and erase data. The AA must, on receiving the request of the citizen, correct the inaccurate or misleading data, complete the incomplete data, update the personal data, and also erase the data unless a specific purpose or legal compliance requires such data to remain.

As per the above, the AA has to create processes to undertake such correction, completion, erasure or updation of data - for which keeping an audit log of what data is collected, why, for how long and where is crucial.

* At this stage, the AA initiates the introduction of a state-level data policy for clear, legitimate and informed data governance practices it plans on adopting.
* Product customization requested by the AA keeps in mind the breach of data and confidentiality and the rights of citizens to data privacy. The AA studies the risks and harms that customisation would cost to the safety of the citizen through the use of his/her data (proportionality test\[10]). The risks, harms and benefits assessment will take into consideration the impact that data use may have on an individual(s) and/or group(s) of individuals, whether legally visible or not and whether known or unknown at the time of data use\[11].
* Configurations include the feature of asking for feedback from citizens when the platform proceeds for a UAT. Citizens are asked for feedback on how data is being handled and whether they are aware of why their data is being used.
* Service Level Agreements include security checks at each level of implementation of the platform for data to be kept secure and safe.

**Technical**

* AA implements privacy-enhancing technologies (PeT’s), such as encryption, anonymization, and access control systems, to protect the personal data that is part of the master data.
* The existence, nature, and anticipated period of retention of data and the purpose of data used through the workflows and processes are publicly disclosed and described in a clear and non-technical language suitable for a general audience

### **B.2.4 Stage 3 - Customisations & Configuration** <a href="#_bdthvay7dk5r" id="_bdthvay7dk5r"></a>

#### **B.2.4.1 What happens in this stage** <a href="#_ck00xcjiwj24" id="_ck00xcjiwj24"></a>

* A configured/customized product is created that is ready for UAT (User acceptance testing).
* Monitoring Reports and Dashboards are ready ( to understand the rollout of the modules).
* Product artefacts like user guides are created.
* Identification of participants for the UAT session.

#### **B.2.4.2 What does the AA team do in Stage 3** <a href="#_uk7d8ovf8mon" id="_uk7d8ovf8mon"></a>

* Master data cleaning and validation.
* Collect ULB-specific baseline data to measure performance and adoption.
* Identify ULB level Nodal officers for day-to-day support.

#### **B.2.4.3 To-Dos** <a href="#_w8u3x0tu6any" id="_w8u3x0tu6any"></a>

**Operational**

**Musts**

* At this stage, the user guides, and instruction manuals are created which include guidelines and best practices on DPP. These user guides could pick up practices from Table 2 [here](https://docs.google.com/document/d/10bsSWEmf2ebjNpGBs-BLXAVyL-sVFQ901GzuKpbNNyY/edit).
* The master data cleaning and validation is the last opportunity for the AA officials to decide on the necessity of data collected for defined purposes. If no corresponding purpose is found for a dataset collected, the dataset does not proceed to flow through the UAT demo.
* The nodal officers are made aware (through training and workshops) of the importance of data privacy and protection and are trained to manage data in a secure manner
* The AA’s privacy policy is visible on the UX ( privacy policy must be easy to understand and small - a sample privacy policy can be found [here](https://docs.google.com/document/d/1TlGUZg5stbJPU5ZXUEiLM9LcBCkjmKjsjmEEPxsYCs4/edit?usp=sharing))
* AA assesses the design of dashboards displaying data, and other data interactions, just as one would for other elements of the product experience.
* AA conducts reviews and checks on whether people can easily access and understand relevant privacy information, whether participants feel they have the right information at the right time, and whether they are in the appropriate state of mind to take informed action.
* As part of UAT, include questions that check if the platform permits people to access their data, understand the purpose for such data being used, by whom is it used and what happens to the data after its use is over. AAs or IAs can use this [sheet](https://ico.org.uk/media/for-organisations/documents/4024005/information-rights-bingo.pdf) as an activity to assess if they are providing the rights to citizens.

### **B.2.5 Stage 4 - UAT & Go-Live** <a href="#_cq77r5nnla5m" id="_cq77r5nnla5m"></a>

#### **B.2.5.1 What happens in Stage 4** <a href="#_9hhmj0s63k6e" id="_9hhmj0s63k6e"></a>

* UAT Sign-off & Go Live permitted for Pilot ULBs or other mandated govt bodies for delivery of services
* Setup of review & monitoring cadence.

#### **B.2.5.2 What do the AA team and IAs do in Stage 4** <a href="#_kigm528x6abx" id="_kigm528x6abx"></a>

* Conduct user acceptance testing and provide sign-off.
* Organise ULB employee training workshops.
* Setup help desks and support mechanisms for ULB.
* Lead the UAT / pilot / Go-live as required along with training key client personnel.

#### **B.2.5.3. To- Dos** <a href="#_22qg94blmhiy" id="_22qg94blmhiy"></a>

**Operational**

**Musts**

* Ensure that the training program for the AA personnel includes DPP practices training as well (can include training in data ethical data collection, use and storage, communicating purpose of data collection, etc.)
* Conduct a data security check while/before conducting the UAT (A data security checklist should include questions like-
* Is PII data encrypted when shared?
* Is data stored in safe databases?
* Do limited roles have access to PII?
* Are employees aware of incident reporting?
* Is there a data protection and privacy policy for hardware protection and external media devices? (Wherever there is a use of removable physical media document the use of such removable physical media and maintain an accurate, up-to-date record of the user profiles created for users who have been authorised access to the information system and the personal data contained therein).
* As part of the review and monitoring cadence the AA creates a DPP checklist ( A DPP checklist can have items like -
* A privacy policy has been established and approved by the AA
* PIAs, or privacy risk assessments, are planned to be regularly performed
* Data processing agreements have been established with all third parties that will process personal data
* The software and infrastructure regularly undergo security risk and threat analysis
* AA has a privacy education/awareness training program
* AA is prepared to handle security incidents affecting personal data
* The amounts of personal data that can be collected have been minimized
* The purpose of data collection has been defined to be as specific as possible
* Any sharing of personal data to third parties has been clearly specified
* The retention date is no longer than necessary to fulfil the purpose of data collection (or to comply with existing legislation)
* The privacy policy clearly states who are responsible for the personal data and how they can be contacted
* The privacy policy is clearly written, to make it easy to understand by the intended end-users
* The length of the privacy policy is not excessive
* The privacy policy can easily be retrieved by citizens at all times
* The helpdesks provide simple material to explain to citizens or employees the concepts of DPP. These help desks serve as one-stop spots for citizens and employees to understand DPP concepts like data privacy methods, masking and limited and purposeful data sharing. Therefore the help-desk representatives are trained well in DPP concepts and use cases before the platform goes live. They also become the first stop for any incident to be reported on data privacy breach

### **B.2.6 Stage 5 - Statewide/ULB-wide Rollout** <a href="#_io252m2fjut6" id="_io252m2fjut6"></a>

#### **B.2.6.1 What happens in Stage 5** <a href="#_kyep9xxv6c1z" id="_kyep9xxv6c1z"></a>

**-**Statewide Rollout in batches

**-** Help desk effectiveness assured

**-** Critical bugs fixed

**-** Program success metrics tracking kick-started&#x20;

#### **B.2.6.2 What do the AA team and IAs do in Stage 5** <a href="#_m7caai2edcq2" id="_m7caai2edcq2"></a>

* Lead rollout, training, change management workshops, training activities and monitoring with client teams.
* Plan phase-wise pan-state rollout.

#### **B.2.6.3 To-Dos** <a href="#_klgpkmocdu96" id="_klgpkmocdu96"></a>

**Operational**

* There is transparency on measures taken for protecting citizens' data privacy and protection ( dashboards showing steps taken, open display of categories of data the AA can see and use, grievance redressal officer appointed)
* Awareness has been built amongst AA team/departments and ULB employees on DPP practices listed above and now employees are held accountable for displaying their training in their functions.
* Regular Privacy Impact assessments (including gap assessments) and data security audits are conducted to check whether the state-wide platform is safeguarding DPP. Can refer to [Table 2](https://docs.google.com/document/d/10bsSWEmf2ebjNpGBs-BLXAVyL-sVFQ901GzuKpbNNyY/edit) to understand if the AA has considered global practices and principles of data protection and privacy for adoption.
* Feedback loops must remain active and are speedy at providing solutions for any anticipated or addressed privacy or data protection issue that comes up
* While transitioning from old/existing systems to new platform-based systems, the data migration process has taken into consideration data masking, encryption, data deletion, purposeful data retention, etc.

### **B.2.7. Stage 6- Sustenance & Ongoing Improvement** <a href="#_1aj7kypxyzez" id="_1aj7kypxyzez"></a>

#### **B.2.7.1. What happens in Stage 6** <a href="#_pyngu51yqgh7" id="_pyngu51yqgh7"></a>

* The first batch of ULBs has been made Live after the Pilot.
* There is the adoption of the platform in the State among the ULB employees and the citizens.

#### **B.2.7.2 What does the AA or IA team do in this Stage** <a href="#_6qsohvpqlcda" id="_6qsohvpqlcda"></a>

* The adoption tracking & review cadence is set up.
* The adoption team at the State and ULB level are set up to drive the adoption of the system.
* The state runs multi-channel awareness campaigns to drive adoption among the citizens of the state.

**B.2.7.3 Role of Supporting Agency**

* At this stage, a ’ Supporting agency’ **(SA)** gets involved. An SA is one that provides support in any functional aspect required by the Prog with respect to that platform implementation (e.g. assistance in maintenance of the platform, technical or operational problem-solving, bug/error resolution).
* An SA can be contracted at Stage 5 or at this stage.
* It primarily assists, guides, firefights and resolves difficult problems for the AA while the platform is implemented/ getting implemented.
* An SA can be given a specific role of overseeing and helping in the DPP practices adoption.

#### **B.2.7.4 To-Dos** <a href="#_lgfnqd8qitk4" id="_lgfnqd8qitk4"></a>

**Operational**

**Musts**

* The AA team conducts reviews on the comfort or discomfort citizens are experiencing with the above DPP practices and design features implemented on the ground.
* Feedback is received from the citizens. Such feedback is analyzed and relevant AA officials are alerted about such feedback for steps to be taken for improvement.
* An SA oversees the applicability of the DPP features are live and troubleshoots any problems arising for all stakeholders.
* SA whose duty is to set DPP practices into action must create impact reports, firefight any issues that arise and create operational awareness for all stakeholders within the AA.
* Awareness campaigns are conducted to build awareness of citizens on their right to data protection and privacy.
* There are continuous sessions for employees of AA and IA held on DPP training.
* AA or implementation team holds community or ULB-based workshops and creates awareness materials like posters, videos, brochures etc.

### **B.2.8 Preferable Practices As Guidelines** <a href="#_91szsy7v8l6o" id="_91szsy7v8l6o"></a>

There are a few guidelines that are preferred to be followed by the AA but are not to be taken as a must-do. A few of them are:

_Stage 1: Program Kick-off_

**Preferable:**

* The data collection model is designed to collect the consent of the citizen before collecting the data. Such consent is recorded in a log registry and maintained with each AA department.\[12]
* There are privacy-specific KPIs or OKRs (objectives and key results) embedded. For example - setting privacy benchmark deliverables like privacy audits and security gap assessments. This would help the AA and IA monitor privacy issues and provide early warning of problems.
* AA provides procedures for citizens to complain or inquire about their data

_Stage 2: Solution design_

**Preferable:**

* AA and IA use privacy concepts as a prompt for generating ideas, such as a ‘[crazy eights](https://www.iamnotmypixels.com/how-to-use-crazy-8s-to-generate-design-ideas/)’ sketching exercise that explores how the platform might work if it processes no personal information (to reduce the amount of PII collected)
* AA establishes an internal system for constant data updation and deletion of obsolete data, wherever appropriate and practically possible ( to maintain data accuracy and quality).



***

1. [Digital Personal Data Protection Act 2023.pdf (meity.gov.in)](https://www.meity.gov.in/writereaddata/files/Digital%20Personal%20Data%20Protection%20Act%202023.pdf) ↑
2. Sec 2 (i) “Data Fiduciary” means any person who alone or in conjunction with other persons determines the purpose and means of processing personal data ↑
3. Sec 2 (k) “Data Processor” means any person who processes personal data on behalf of a Data Fiduciary ↑
4. Articles 25 and 32 of the GDPR ↑
5. For more technical info on access controls, you may read this [document ](https://core.digit.org/focus-areas/data-security/signed-data-audit)↑
6.  \- Process any data only if there is a valid contract between the administering authority and eGov ( data fiduciary & processor) \[Sec 8(2)]

    \-Maintain security safeguards to prevent personal data breaches \[Sec 8(5)]

    \-Follow the instructions given by the data fiduciary on data deletion

    \-Follow processing standards issued through Central government policies ( as issued under Sec 7(b)(ii) - yet to be issued)

    \-Maintain a record of data processed ( to assist the data fiduciary i.e. the relevant administering authority with obligation Sec 11 of the Act)

    \-Maintain the completeness, accuracy, and consistency of personal data \[ Section 8(3)]

    \-Implement appropriate technical and organizational measures to implement the Act \[Sec 8(4)]

    \-Intimate the data fiduciary on any personal data breach \[so that the data fiduciary can inform the Board and data principal about such a breach - Sec 8(6)] ↑
7. Refer to the principle of data minimisation and storage limitation [here](https://docs.google.com/document/d/10bsSWEmf2ebjNpGBs-BLXAVyL-sVFQ901GzuKpbNNyY/edit) ↑
8. For each item of data collected, stored, processed, or shared, there should be a clear purpose identified; this purpose must flow from a legitimate task that the entity collecting it (i.e. a ULB) is mandated & authorized to perform (hence, legitimate), and this purpose must be communicated to the citizen. This is closely related to the concepts of data minimisation, purpose limitation, and role-based access. ↑
9. Sec 11 of the DPDP Act, 2023 ↑
10. The proportionality test was prescribed for in the J.Puttaswamy judgement. This test is for data processing bodies to analyse how much of a risk the use of the data puts the person to whom the data belongs versus the benefits it brings to that person simultaneously. A balance between the benefits and the risks must be found. ↑
11. An assessment of harms should consider such key factors as - (i) the likelihood of occurrence of harms, (ii) the potential magnitude of harms and (iii) the potential severity of harms. Additionally, the assessment should take into account the digital literacy of both potential users of data and those individuals whose data is being used. ↑
12. Refer to the principle of notice, awareness and user control [here ](https://docs.google.com/document/d/10bsSWEmf2ebjNpGBs-BLXAVyL-sVFQ901GzuKpbNNyY/edit)↑

[^1]: Sec 2 (i) “Data Fiduciary” means any person who alone or in conjunction with other persons determines the purpose and means of processing personal data&#x20;

[^2]: Sec 2 (k) “Data Processor” means any person who processes personal data on behalf of a Data Fiduciary&#x20;

[^3]: Articles 25 and 32 of the GDPR&#x20;

[^4]: \- Process any data only if there is a valid contract between the administering authority and eGov ( data fiduciary & processor) \[Sec 8(2)]

    \-Maintain security safeguards to prevent personal data breaches \[Sec 8(5)]

    \-Follow the instructions given by the data fiduciary on data deletion

    \-Follow processing standards issued through Central government policies ( as issued under Sec 7(b)(ii) - yet to be issued)

    \-Maintain a record of data processed ( to assist the data fiduciary i.e. the relevant administering authority with obligation Sec 11 of the Act)

    \-Maintain the completeness, accuracy, and consistency of personal data \[ Section 8(3)]

    \-Implement appropriate technical and organizational measures to implement the Act \[Sec 8(4)]

    \-Intimate the data fiduciary on any personal data breach \[so that the data fiduciary can inform the Board and data principal about such a breach - Sec 8(6)]

[^5]: For each item of data collected, stored, processed, or shared, there should be a clear purpose identified; this purpose must flow from a legitimate task that the entity collecting it (i.e. a ULB) is mandated & authorized to perform (hence, legitimate), and this purpose must be communicated to the citizen. This is closely related to the concepts of data minimisation, purpose limitation, and role-based access.
