# Data Privacy & Protection For Administration Authorities

## Scope

DIGIT, an open-source platform, enables governments and service providers to provide an interdepartmental coordination and citizen-facing service delivery system - currently, in the fields of urban governance, sanitation, health, and public finance management.&#x20;

As citizen data is collected and used for such governance services, data privacy and protection measures are required to ensure this data is managed responsibly and safely.&#x20;

This document is created to be an online guide, providing guidelines for administrative authorities (government entities like state government bodies, local governing bodies etc) to maintain data privacy and protect individuals’ data.&#x20;

* Readers can use this to identify the steps they must take, in their capacity as administrative authorities, to ensure data privacy and protection in the context of a DIGIT or DIGIT-like implementation.&#x20;
* It can also provide source material for privacy policies, which should be included in each portal & application.&#x20;
* This is not a technical reference or documentation. It serves as a policy guideline.

References made to DIGIT are also applicable to other platforms similar to DIGIT. Not all parts of the guidelines or featured content may match the reader's platform or context, hence this document is open to be referred to in parts as needed.&#x20;

## Guidelines&#x20;

These guidelines are to be read through the eyes of roles that are part of the administrative authority’s (AA) offices in the journey of adopting a DIGIT-based system or platforms similar to DIGIT in a government entity/ies.&#x20;

If a government authority adopts DIGIT as a citizen service platform, then these guidelines are apt. Some points in the guidelines may not be relevant to platforms other than DIGIT in the governance ecosystem. Hence these guidelines have to be read as advisory.&#x20;

Common roles of government entities that are part of the DIGIT currently  are:&#x20;

* Field level employee
* Line Management employee
* Administrative Officer (AO)
* Domain-level data collector
* Verifiers
* Field inspectors
* State or ULB-level head role/authority
* State administrators&#x20;

This is a non-exhaustive list of roles.

There may in the future be more roles involved from a government entity while using DIGIT, including Ward-level volunteers and/or Intermediaries.

It is to be noted that similar guidelines can be found for ‘data controllers’ under the European General Data Protection Regulation (GDPR). There are a few basic and minimum requirements that data controllers (bodies that decide the purpose for processing data and the means used to process the data) have to comply with to ensure data protection by default (DbD and PbD) and design (data minimization, implementing safeguards for protection of data, controlled access to data, limited purposeful storage, etc). In Europe, government entities are legally obligated to maintain DbD and PbD or else they are heavily penalised.

### Guidelines For All Roles&#x20;

There are a few common guidelines that all roles must follow.

Data security measures and practices stand out as the core / foundational guideline to follow for all roles.

Data Privacy and Protection (DPP) is only possible when the systems and computer resources receiving and storing data are secure (safe from any harm). Some key data security measures include:

* Access control: Establish audited and controlled access for personally identifying data, including authentication and authorization mechanisms. Authorize individuals only if they have a legal basis and a legitimate purpose to access the data.
* Encryption: Encrypt PII data both in transit and at rest to protect it from unauthorized access and theft.
* Data backup and disaster recovery: Regularly backing up PII data - including auditing the need for PII - if not required then deleting the PII, and implementing disaster recovery plans to ensure that important data can be recovered in the event of a data loss or breach.
* Network security: Implement firewalls, intrusion detection and prevention systems, and other network security measures to protect against cyber threats.
* Vulnerability management: Regularly scan for vulnerabilities and patch systems and applications to minimize the risk of a breach.
* Employee education: Educate employees/contractors/personnel on the importance of data security and provide training on best practices for protecting PII.
* Physical security: Implement physical security measures, such as access controls and video surveillance, to protect against unauthorized access to data centres and other data facilities.
* Third-party security: Carefully vet third-party vendors and service providers, to ensure that they have appropriate security measures in place to protect PII.
* Incident response: Develop and test incident response plans to ensure that the organization can quickly and effectively respond to a security breach.
* Compliance: Adhere to relevant security and privacy regulations, such as the IT Act, 2000, and its subsequent amendments and Rules. Conforming with standards such as ISO 27001 is also a good practice.

### Detailed Guidelines For Administrative Authority&#x20;

Below are the broad roles we cover under these guidelines:

* Administrative authority (AA) (the body that is mandated to provide for the government service usually an agency or department of the State government). This can include bodies like [State Program Directorate and Program Monitoring Units. ](https://niua.in/cdg/UPYOG)The above-listed roles (In Section D) come under this category.&#x20;
* Implementation agency/system integrator (SI) (the body that implements the platform provided by the platform owner into the administering authority’s IT systems)&#x20;
* Maintenance team (can be an additional team that gets involved after the platform is implemented in the administering authority’s systems to maintain the system)

The previous document in this series covered the guidelines for platform owners/providers.

To understand what each role should do to safeguard DPP, it is important to understand what these roles do at each phase of the implementation of DIGIT.

### Stage 0 -Program set-up&#x20;

#### What is a program?

A program can be a delivery of any government service/s which the AA is mandated to provide to citizens for which it requires a platform. Defining the scope of the program is within the power of an AA.

#### What happens at this stage?&#x20;

* A Memorandum of Understanding is signed between the AA and the platform owners
* A State Program Head/Nodal Officer is appointed by the AA
* Resources and funding for the program are identified.
* The AA-specific procurement process is defined.
* SI team onboarding is initiated.

#### AA and (SI) or implementing partner’s role at Stage 0:

* Ensure onboarding of manpower and infrastructure as specified.&#x20;
* Lead the setup of the program and related governance structure
* Appoint program steering committee and state nodal officer.
* Initiate onboarding of implementation partner.
* Initiate onboarding of Cloud infrastructure provider.
* Identify module deployment priorities.

#### To-Dos&#x20;

Operational Musts:

* The relevant department of the AA  makes a financial commitment towards enabling data privacy, protection, and security in the system. This would solidify the operationalisation of any measures taken for DPP.
* Spells out data use and governance terms and conditions in all agreements with partners, e.g. MoUs and contracts.&#x20;
* There is a clear definition of who owns data and who is responsible for data protection, extent and purpose of data access in MoUs and contracts.&#x20;
* The AA documents the purposes for data collection, use and disclosure. Such purpose is to be found in a legally backed instrument or documentation ( can be a government authority-sanctioned document pointing at a law/ policy that needs such data to be processed for citizen delivery purposes).&#x20;
* AA ensures that the design of the platform would involve data collection and processing only if there is a defined purpose for such data being processed.&#x20;
* The selection of a particular technological solution takes the risks inherent to that technology into consideration. i.e. the AA questions the risks that the tech system brings to the citizen and employees if used for service delivery. Risk assessment can be done by conducting an anticipated data protection impact assessment (DPIA). It is important that the platform owner is involved in this assessment, as they are probably the best placed to evaluate the technologies that might be used and that might involve a high risk for the rights and freedoms of people, making the DPIA necessary.&#x20;
* AA creates measures that can be put in place to reduce the anticipated risks deduced from the above, taking into account the state of the current technology and the cost of applying them.

#### Role of IA/SIs

* The other actors that AAs engage with to provide digital government service delivery are -the Implementation Agencies (IA) or System Integrators (SI).

At this stage the AA -

* Defines the manner in which the IA must ensure that DPP practices are maintained
* Drafts a working agreement which commits the IA to safeguard the data and the right of citizens to data protection and privacy&#x20;
* A few clauses which the AA could ask the IA to contractual perform are:
  1. Maintain transparency in data practices (API-based data received, shared or used should be visible to the AA)&#x20;
  2. Report any data security breach to the AA
  3. Audit and create safeguards against non-authorized third-party access to data
  4. Implement appropriate security controls like encryption at source, masking of data, ABAC logins, and conducting regular security audits and checks.
  5. Regularly educate its employees on data privacy, data ethics and data privacy.

The IA/SI can preferably:&#x20;

* In the works with the AA, including at least one person having a working knowledge of data security, privacy, and protection. SI’s usually have an in-house team for data security and privacy; if there is no such team, the SI may bring a person with relevant skills in for the project. In case the AA has chosen an in-house entity to implement the project rather than an SI, the project in charge should again ensure that a person with these skills is brought in for the project.

#### Role of cloud infrastructure providers

At stage zero, the AA begins to consider which infrastructural systems they would be adopting. Cloud infrastructure providers are usually sourced by the IA or by the AA. Choosing a cloud storage provider with safe data governance practices is important to avoid data breaches.&#x20;

A few must-haves the AAs must keep in mind before selecting a cloud infrastructure provider are:&#x20;

* Maintains and implements data protection policies.
* Encrypts PII with private keys,
* Conduct regular security checks and audits on data security and privacy&#x20;
* Safeguards data from being shared with unauthorized users
* Maintains transparent data storage and governance models&#x20;

### Stage 1 - Program kickoff&#x20;

#### What happens at Stage 1

* &#x20;Publishing of the program charter and implementation plan.
* &#x20;Master data collection kickoff in Pilot ULBs&#x20;
* Cloud Infrastructure is procured
* Program branding is done (name, logo, tagline etc.)&#x20;

#### AA team + Partners (system integrators (SI) or implementing partner) role at Stage 1

1\. Identify Pilot ULBs (urban local bodies) or any other local governmental agency or body that is mandated to provide the government service

2\. Appoint the data collection team and initiate data collection from the Pilot ULBs/ bodies in the required format.

3\. Organize implementation kick-off workshop with relevant  stakeholders of identified Pilot bodies

4\. Create the program charter and implementation plan.

#### To-Dos

Operational Musts:

* At this stage, the best practice model of master data collection (steps listed below) is designed - for it to be implemented when actual data is collected at the next stage. Here master data is the primary data needed for module functionality.&#x20;
* The master data collection model design includes:&#x20;
  1. AA collects minimum personal data - they can do so by collecting personal data only once and using federated databases and interoperable systems to avoid the re-collection of personal data.
  2. The categories of datasets the AA entity would most necessarily require to provide a service are defined and fixed. This is done so as to adopt the practice of collecting only data that is necessary for the provision of a service at the next stage.
  3. Data without any defined use or need is not collected (data minimisation, legitimate purpose).&#x20;
  4. Citizens of the ULBs are informed of the purpose of their data being collected.&#x20;
  5. Data collected at the next stage is stored safely ( on paper or digitally). If collected on paper then once transmitted into a digital system, it is destroyed from the paper or source device.
  6. Dashboards displaying the nature of data to be collected and their corresponding purposes and uses are built; (for transparency and awareness of citizens).
  7. Specific roles are created for building accountability for safe, limited and purposeful data collection.
  8. The program charter clearly states that the data provider i.e. the citizen is the owner of the data.
  9. The implementation plan has DPP practices embedded in it. For example in the processes of data migration and data processing, the system does not permit sensitive data to be visible to unauthorized roles, strict logins are maintained, and the implementing partners' employees are trained in safe data handling.
* Before master data collection (which partly begins in this stage but is majorly conducted at the next stage), AA arranges for staff/employee training in regard to information privacy protection and awareness of relevant policies regarding citizen's privacy protection
* The AA begins to draft a privacy policy, envisioning its data governance model.&#x20;
* AA ensures that the IA is onboarding a team with appropriate skill sets through reviews and initial expectation setting
* The implementation kickoff workshops with representatives of the AAs includes training on purposeful master data collection (for the next stage) in an informed and transparent manner ( letting the citizen know why they are collecting the data).
* As suggested in the above stage, a secure cloud infrastructure provider is appointed.&#x20;

### Stage 2 - Solution Design&#x20;

#### What happens at Stage 2&#x20;

* Standardized ontologies (uniform terminology for easier understanding), processes and workflows are created.
* Master data collected in the desired format.
* Agreement on AA - specific product customisations is required.&#x20;
* A detailed program plan is made and the tracking mechanism is finalised.&#x20;

#### What do the AA team and SI do at Stage 2?&#x20;

* &#x20;Standardize the ontology, processes and workflows in the states
* &#x20;Initiate policy change if required
* &#x20;Provide state-specific requirements, if any.
* Lead solution design, impact analysis, and integration analysis.
* Get designs and requirements signed-off

#### To-Dos

Operational Musts:

* AA conducts assessments on data governance of the preparation processes and workflows before finalisation. This includes factors like:
  1. Master data that includes personally identifying information (PII) to be used in an encrypted/ masked manner through the workflows.
  2. Processing of data takes place only if the benefits from the use of the processed data would be proportional to the risks that such processing produces.
  3. Data that flows in the processes and workflows have strict access requirements.
* At this stage, the AA initiates the introduction of a state-level data policy for clear, legitimate and informed data governance practices it plans on adopting.&#x20;
* Product customization requested by the AA keeps in mind the safety of the data and the rights of citizens to data privacy. The AA  studies the risks and harms that customisation would cost to the safety of the citizen through the use of his/her data (proportionality test). The risks, harms and benefits assessment will take into consideration the impact that data use may have on an individual(s) and/or group(s) of individuals, whether legally visible or not and whether known or unknown at the time of data use.
* Configurations include the feature of asking for feedback from citizens when the platform proceeds for a UAT. Citizens are asked for feedback on how data is being handled and whether they are aware of why their data is being used.
* &#x20;Service Level Agreements include security checks at each level of implementation of the platform for data to be kept secure and safe.

Technical:

* AA implements privacy-enhancing technologies (PeTs), such as encryption, anonymization, and access control systems, to protect the personal data that is part of the master data.&#x20;
* The existence, nature, and anticipated period of retention of data and the purpose of data used through the workflows and processes are publicly disclosed and described in clear and non-technical language suitable for a general audience.

### Stage 3 - Customisations and Configuration

#### What happens at this stage?

* Configured/Customized product is created that is ready for UAT ( User acceptance testing).
* Monitoring Reports and Dashboards are ready ( to understand the rollout of the modules)
* Product artefacts like user guides are created.
* Identification of participants for the UAT session

#### What does the AA team do at Stage 3?&#x20;

* Master data cleaning and validation.&#x20;
* &#x20;Collect ULB-specific baseline data to measure performance and adoption.&#x20;
* &#x20;Identify ULB  level Nodal officers for day-to-day support.

#### To-Dos:

Operational Musts:

* At this stage, the user guides, and instruction manuals are created which include guidelines and best practices on DPP. These user guides could pick up practices from Table 2 [here](global-best-practices-for-data-protection-and-privacy.md).&#x20;
* The master data cleaning and validation is the last opportunity for the AA officials to decide on the necessity of data collected for defined purposes. If no corresponding purpose is found for a dataset collected, the dataset does not proceed to flow through the UAT demo.
* The nodal officers are made aware (through training and workshops)  of the importance of data privacy and protection and are trained to manage data in a secure manner
* The AA’s privacy policy is visible on the UX ( privacy policy must be easy to understand and small - a sample privacy policy can be found [here](privacy-policy-details.md))
* AA assesses the design of dashboards displaying data, and other data interactions, just as one would for other elements of the product experience.&#x20;
* AA conducts reviews and checks on whether people can easily access and understand relevant privacy information, whether participants feel they have the right information at the right time, and whether they are in the appropriate state of mind to take informed action.
* As part of UAT, include questions that check if the platform permits people to access their data, understand the purpose for such data being used, by whom is it used and what happens to the data after its use is over. AAs or SI’s may use this [sheet](https://ico.org.uk/media/for-organisations/documents/4024005/information-rights-bingo.pdf) as an activity to assess if they are providing the rights to citizens.&#x20;

### Stage 4 - UAT and Go-Live

#### What happens at Stage 4?

* UAT Sign-off & Go Live permitted for Pilot ULBs or other mandated govt bodies for delivery of services
* Setup of review & monitoring cadence.

#### What do the AA team and SI’S do at Stage 4?&#x20;

* Conduct user acceptance testing and provide sign-off.
* &#x20;Organise ULB employee training workshops
* Setup help desks and support mechanisms for ULB
* Lead the UAT / pilot / Go-live as required along with training key client personnel

#### To-Do’s&#x20;

Operational Musts:

* Ensure that the training program for the AA personnel includes DPP practices training as well (can include training in data ethical data collection, use and storage, communicating purpose of data collection, etc.)&#x20;
* Conducts a data security check while/before conducting the UAT (A data security checklist should include questions like-&#x20;
* Is PII data encrypted when shared,&#x20;
* Is data stored in safe databases&#x20;
* Do limited roles have access to PII, &#x20;
* Are employees aware of incident reporting,&#x20;
* Is there a data protection and privacy policy for hardware protection, and external media devices? (wherever there is a use of removable physical media document the use of such removable physical media, and maintain an accurate, up-to-date record of the user profiles created for users who have been authorised access to the information system and the personal data contained therein)

As part of the review and monitoring cadence the AA creates a DPP checklist (A DPP checklist can have items like -&#x20;

* A privacy policy has been established and approved by the AA
* PIAs, or privacy risk assessments, are planned to be regularly performed&#x20;
* Data processing agreements have been established with all third parties that will process personal data &#x20;
* The software and infrastructure regularly undergo security risk and threat analysis&#x20;
* AA has a privacy education/awareness training program&#x20;
* AA is prepared to handle security incidents affecting personal data
* The amounts of personal data that can be collected have been minimized &#x20;
* The purpose of data collection has been defined to be as specific as possible&#x20;
* Any sharing of personal data to third parties has been clearly specified &#x20;
* The retention date is no longer than necessary to fulfil the purpose of data collection (or to comply with existing legislation)&#x20;
* &#x20;The privacy policy clearly states who is responsible for the personal data and how they can be contacted &#x20;
* The privacy policy is clearly written, to make it easy to understand for the intended end-users &#x20;
* The length of the privacy policy is not excessive&#x20;
* The privacy policy can easily be retrieved by citizens at all times

The helpdesks provide simple material to explain to citizens or employees the concepts of DPP. These help desks serve as one-stop spots for citizens and employees to understand DPP concepts like data privacy methods, masking, and limited and purposeful data sharing. Therefore the help-desk representative is trained well in DPP concepts and use cases before the platform goes live. They also become the first stop for any incident to be reported on data privacy breach.

### Stage 5 - Statewide / ULB wide Rollout

#### What happens at Stage 5?

\-Statewide Rollout in batches

\- Help desk effectiveness assured

\- Critical bugs fixed

\- Program success metrics tracking kick-started&#x20;

#### What do the AA team and SI’s do at Stage 5?&#x20;

* Lead rollout, training, change management workshops, training activities and monitoring with client teams
* Plan phase-wise pan-state rollout

#### To-Dos

Operational:

* There is transparency on measures taken for protecting citizens' data privacy and protection (dashboards showing steps taken, open display of categories of data the AA can see and uses, grievance redressal officer appointed)
* Awareness has been built amongst AA team/departments and ULB employees on DPP practices listed above and now employees are held accountable for displaying their training in their functions.
* Regular Privacy Impact assessments (including gap assessments) and data security audits are conducted to check whether the state-wide platform is safeguarding DPP. Can refer to [Table 2](https://docs.google.com/document/d/10bsSWEmf2ebjNpGBs-BLXAVyL-sVFQ901GzuKpbNNyY/edit) to understand if the AA has considered global practices and principles of data protection and privacy for adoption.
* Feedback loops must remain active and are speedy at providing solutions for any anticipated or addressed privacy or data protection issue that comes up
* While transitioning from old/existing systems to new platform-based systems, the data migration process has taken into consideration data masking, encryption, data deletion, purposeful data retention, etc.

### Stage 6- Sustenance & Ongoing Improvement&#x20;

#### What happens at Stage 6?&#x20;

* The first batch of ULBs has been made Live after the Pilot.
* There is the adoption of the platform in the State among the ULB employees and citizens.

#### What does the AA or SI team do at this Stage?

* The adoption tracking & review cadence is set up. &#x20;
* The adoption team at the State and ULB level are set up to drive the adoption of the system.
* The state runs multi-channel awareness campaigns to drive adoption among the citizens of the state.

#### To-Dos

Operational Musts:

* The AA team conducts reviews on the comfort or discomfort citizens are experiencing with the above  DPP practices and design features implemented on the ground.
* Feedback is received from the citizens. Such feedback is analyzed and relevant AA officials are alerted about such feedback for steps to be taken for improvement.
* Awareness campaigns are conducted on building awareness of citizens on their right to data protection and privacy.
* There are continuous sessions for employees of AA and SI  held on DPP training.
* AA or implementation team holds community or ULB-based workshops and creates awareness materials like posters, videos, brochures etc.

### Preferable Practices As Guidelines&#x20;

There are a few guidelines that are preferred to be followed by the AA but are not to be taken as a must-do. A few of them are:&#x20;

#### Stage 1: Program Kick-off

Preferable:&#x20;

* The data collection model is designed for collecting the consent of the citizen before collecting the data. Such consent is recorded in a log registry and maintained with each AA department.
* There are privacy-specific KPIs or OKRs (objectives and key results) embedded. For example - setting privacy benchmark deliverables like privacy audits, and security gap assessments. This would help the AA and SI monitor privacy issues and provide early warning of problems.&#x20;
* AA provides procedures for citizens to complain or inquire about their data&#x20;

#### Stage 2: Solution design&#x20;

Preferable:

* AA and SI  use privacy concepts as a prompt for generating ideas, such as a ‘[crazy eights](https://www.iamnotmypixels.com/how-to-use-crazy-8s-to-generate-design-ideas/)’ sketching exercise that explores how the platform might work if it processes no personal information (to reduce the amount of PII collected)
* AA establishes an internal system for constant data updation and deletion of obsolete data, wherever appropriate and practically possible ( to maintain data accuracy and quality)
