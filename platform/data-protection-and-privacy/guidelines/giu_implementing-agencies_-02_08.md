# GIU\_Implementing Agencies\_ 02\_08

**Data Protection and Privacy Guidelines for DIGIT Implementations**

**(Implementing Agencies)**

_eGovernments Foundation, August 2023_

### DOCUMENT METADATA <a href="#_58vqdh9ic1z7" id="_58vqdh9ic1z7"></a>

1. Jira project #:
2. Title: Data Protection and Privacy Guidelines for DIGIT Implementations - Implementing agencies
3. Version #: 1
4. Version date: 02/08/23
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

B.1.2 IA’s role at Stage 0: 4

B.1.3 To-Do’s 4

B.2. Stage 1 - Program kickoff 6

B.2.1 What happens at Stage 1- 6

B.2.2 What does the IA team do at Stage 1: 6

B.2.3 To-Do’s: 6

B.3 Stage 2 - Solution Design 8

B.3.1 What happens at Stage 2 - 8

B.3.2 What does the IA do at stage 2? 8

B.3.3 To-Do’s: 8

B.4 Stage 3 - Customization and Configuration 10

B.4.1 What happens at this stage? 10

B.4.2 What does the IA do at Stage 3? 10

B.4.3 To-Do’s: 10

B.5 Stage 4 - UAT and Go-Live 10

B.5.1 What happens at Stage 4? 10

B.5.2 What does the IA team do at Stage 4? 11

\- Assists the AA/Prog in conducting the UAT 11

B.5.3. To- Do’s 11

B.6 Stage 5 - Statewide / ULB-wide Rollout 13

B.6.1 What happens at Stage 5? 13

B.6.2 What does the IA do at Stage 5? 13

B.6.3 To-Do’s: 13

B.7. Stage 6- SUSTENANCE & ONGOING IMPROVEMENT 13

B.7.1. What happens at Stage 6? 13

B.7.2 What does the IA do at this stage? 14

B.7.3 To-Do’s: 14

### &#x20;<a href="#_tl7ytlot0qyl" id="_tl7ytlot0qyl"></a>

### **Scope of these guidelines** <a href="#_finvglukkilj" id="_finvglukkilj"></a>

DIGIT, an open-source platform, enables governments and service providers to provide an interdepartmental coordination and citizen-facing service delivery system - currently, in the fields of urban governance, sanitation, health, and public finance management.

As citizen data is collected and used for such governance services, data privacy and protection measures are required to ensure this data is managed responsibly and safely.

This document is created to be an online guide, providing guidelines for Implementing agencies to maintain data privacy and protect individuals’ data.

* Readers can use this to identify the steps they must take, in their capacity as implementing agencies, to ensure data privacy and protection in the context of a DIGIT or DIGIT-like implementation.
* It can also provide source material for privacy policies, which should be included in each portal & application.
* This is not a technical reference or documentation. It serves as a policy guideline.

References made to DIGIT are also applicable to other platforms similar to DIGIT. Not all parts of the guidelines or featured content may match the reader's platform or context, hence this document is open to be referred to in parts as needed.

These guidelines are to be read through the eyes of roles that are part of the Implementation Agencies **(IA)** offices in the journey of adopting a DIGIT-based system or platforms similar to DIGIT in a government entity/ies.

As per the Digital Personal Data Protection Act, 2023 (DPDP Act) an IA would be a data processor\[1]. If the IA gets involved in deciding the purpose and means of the data processing , then it would become a data fiduciary\[2]. The guidelines below cover measures to be in compliance with the DPDP Act.

If a government authority adopts DIGIT as a citizen service platform, then these guidelines are apt. Some points in the guidelines may not be relevant to platforms other than DIGIT in the governance ecosystem. Hence these guidelines have to be read as advisory.

The previous document in this series covered the guidelines for platform owners **(PO)**, and administering authorities **(AA)**.

For this document to understand what each program owner should do to safeguard data privacy and protection (**DPP)**, it is important to understand what IA does at each phase of the implementation of DIGIT.

### **B.1 Stage 0 -Program set-up** <a href="#_d6nd612vi81g" id="_d6nd612vi81g"></a>

**What is a program?**

A program can be a delivery of any government service/s which the AA is mandated to provide to citizens for which it requires a platform. Defining the scope of the program is within the power of an AA.

#### **B.1.1 What happens at this stage?** <a href="#_i4ysv1i2ktpu" id="_i4ysv1i2ktpu"></a>

* A Memorandum of Understanding is signed between the AA and the platform owners. A Prog can also be a party to the MoU, or may be an equal power holding or subordinate entity of the AA (which signs the MOU).
* A State Program Head/Nodal Officer is appointed by the AA
* Resources and funding for the program are identified.
* The program specific procurement process is defined.
* IA team onboarding is initiated.

#### **B.1.2 IA’s role at Stage 0:** <a href="#_3nhj8r81i7uc" id="_3nhj8r81i7uc"></a>

* At this stage the IA becomes a part of the program.
* An official MoU or contract is entered into detailing the terms and conditions between the IA and the AA or Prog
* IA begins to understand the needs of the program
* IA begins making an implementation plan , that shall be published in the next stage

#### **B.1.3 To-Do’s** <a href="#_o2sxxhqvmxds" id="_o2sxxhqvmxds"></a>

**Must-haves:**

* IA must ensure there is an authorization document/proof/contract (MoU) - validating and authorizing the IA’s access to future data and its related compliances ( in compliance with Sec 8 of the Digital Personal Data Protection Act,2023\[3])
* IA presents its own data management and privacy policy to the AA or Prog. This would make the IA’s stand on DPP very clear and easier for the AA or Prog to design a data sharing/access agreement with the IA
* The clauses and language in the MoU/ data access/sharing agreement with the AA or Prog must include:
* Data will always be controlled by the AA or the Prog, IA will never have data controlling power ( IA must not decide the purpose and means of the processing of the data)
* IA will be restricted from third party data sharing without authorization from the AA or Prog
* IA will not collect personal identifying information **(PII)** from citizens directly or indirectly without written permission by the AA or Prog
* Access to PII by IA team should be role based , through strict logins audited and reported to the AA or Prog
* IA will access PII only for purposes specified and authorized by the AA or Prog
* IA will not keep any PII backup or secondary copy of such data
* Data breach consequences - who holds accountability for data breaches
* In the implementation plan, the IA must push for maintaining the data safely and securely from the beginning of the program life cycle to avoid any data or confidential breach. For eg the IA can detail out a data sharing mechanism that masks direct PII from being visible to IA representatives
* The IA should make clear the access, processing and sharing of data in the implementation plan to avoid future confusions on data accountability
* At every step of the implementation plan, the IA must reduce or eliminate its access to PII
* Privacy enhancing features like encryption, privacy by default steps including purposeful processing of data, data deletion post use and strict restricted access to PII must find a big space in the implementation plan

**Preferable practices:**

* Assist/ advice the AA/Prog in mapping out resources and funding needs for maintaining safe data protection and security structures ( hardware and software)
* Embedding DPP practices in the implementation plan. For example, in the processes of data migration and data processing , the system does not permit sensitive data to be visible to unauthorized roles, strict logins are maintained, and IA employees are trained in safe data handling.
* Help the AA or Prog make a program specific data privacy policy ( if they don’t have one made already for the specific program).

### **B.2. Stage 1 - Program kickoff** <a href="#_u7fbjnxklmm" id="_u7fbjnxklmm"></a>

#### **B.2.1 **_**What happens at Stage 1-**_ <a href="#_4sqe9wpbptny" id="_4sqe9wpbptny"></a>

* Publishing of the program charter and implementation plan.
* Master data collection begins in Pilot (selected) ULBs (Urban Local Body)
* Cloud Infrastructure is procured
* Program branding is done (name, logo, tagline etc.)

### **B.2.2 What does the IA team do at Stage 1:** <a href="#_6awpo89sejbq" id="_6awpo89sejbq"></a>

* Here data starts to be shared with the IA for deployment of the modules
* The IA and the AA/Prog publish the implementation plan
* IA team beings looking for resources for the deployment of the modules

#### **B.2.3 To-Do’s:** <a href="#_aqutoz97v3hx" id="_aqutoz97v3hx"></a>

**Must-haves:**

* The IA restricts or disallows any direct PII from being sent to it. The IA intimates the AA/Prog representatives to mask or encrypt the data in the manner
* IA trains AA and its own employees in data best practices like purpose based data access, strict password controls, data sharing hygiene and makes all aware of the legal consequences of breach of data and confidentiality\[4].
* To follow the DPDP Act :
* the IA maintains an audit log of the data ( to provide a summary of personal data processed to the data fiduciary)
* Maintain the completeness, accuracy, and consistency of personal data \[ Section 8(3)]
* Implement appropriate technical and organizational measures to implement the Act \[Sec 8(4)]
* Intimate the data fiduciary on any personal data breach \[so that the data fiduciary can inform the Board and data principal about such a breach - Sec 8(6)]

**Preferable/Good practices:**

* IA encourages AA or Prog to:
* Collect data only if it is needed for a specific legitimate reason and defined purpose ( data minimisation\[5] , legitimate purpose\[6] ).
* Proactively inform the citizens about the legal basis and reason/purpose for their data being collected ( when collected directly from the resident)
* Data is encrypted or masked when data is being migrated from paper to digital or old or new digital systems
* Strategies for safe storage of data ( on paper or digitally) are set.
* Paper-based data is destroyed after a defined migration period (AA or Prog to define a data deletion period post-migration).
* Create a data dashboard to show the nature of data collected and their corresponding purposes and uses (for transparency and awareness of citizens).
* IA onboards a team with appropriate Data privacy and protection safeguarding skill sets
* The implementation kickoff workshops includes training on purposeful master data collection (for the next stage) in an informed and transparent manner ( letting the resident know why they are collecting the data).

### &#x20;<a href="#_lfe80f4y5g09" id="_lfe80f4y5g09"></a>

### **B.3 Stage 2 - Solution Design** <a href="#_rxglyh1if8ij" id="_rxglyh1if8ij"></a>

#### **B.3.1 **_**What happens at Stage 2 -**_ <a href="#_7vju1mfpul4o" id="_7vju1mfpul4o"></a>

* Standardized ontologies (uniform terminology for easier understanding), processes and workflows are created.
* Master data collected in the desired format.
* Agreement on program-specific product customisations required.
* Detailed program plan is made and the tracking mechanism is finalized.

#### **B.3.2 What does the IA do at stage 2?** <a href="#_j9o0nolxzoaz" id="_j9o0nolxzoaz"></a>

* Product specifications with AA are finalized
* IA begins the process of adopting the ontologies , designing/re-designing modules and workflow creations as per needs of AA or Prog

#### **B.3.3 **_**To-Do’s:**_ <a href="#_jah5sk1fyajc" id="_jah5sk1fyajc"></a>

**Must-haves:**

In workflows and processes-

* PII is kept in an encrypted/ masked manner through the workflows.
* Strict data access requirements are in place (audit logs, restricted access points)
* Data is maintained in secure storages
* Data sharing is restricted through permitted devices, channels and to selected roles

**Preferable/Good practices:**

* IA conducts a risk assessment of the customizations asked for by the AA or Prog checking (proportionality test\[7]) risks and harms that may cause a breach of data privacy and confidentiality. Assessment will take into consideration the impact that data use may have on an individual(s) and/or group(s) of individuals, whether known or unknown at the time of data use\[8].
* Include security checks at each level of implementation of the platform for data to be kept secure and safe.

### &#x20;<a href="#_tdytr1a58bo4" id="_tdytr1a58bo4"></a>

### **B.4 Stage 3 - Customization and Configuration** <a href="#_bdthvay7dk5r" id="_bdthvay7dk5r"></a>

#### **B.4.1 **_**What happens at this stage?**_ <a href="#_ck00xcjiwj24" id="_ck00xcjiwj24"></a>

* Configured/Customized product is created that is ready for UAT.
* Monitoring Reports and Dashboards are ready (to understand rollout of modules)
* Product artifacts like user guides are created.
* Identification of participants for UAT session

#### **B.4.2 What does the IA do at Stage 3?** <a href="#_uk7d8ovf8mon" id="_uk7d8ovf8mon"></a>

* Delivers the product to the relevant team of the Pilot for User acceptance testing **(UAT)**
* Helps the AA/Prog team deploy the product module/s in the ULB for testing
* Assists in creating user guides for the Prog team to implement the product

#### **B.4.3 To-Do’s:** <a href="#_w8u3x0tu6any" id="_w8u3x0tu6any"></a>

**Must-haves:**

* Make the privacy policy visible on the product webpage
* Ensure the above data safety and privacy enabling measures are incorporated in the implementation of the product
* If the AA insructs, be ready to delete data which no longer serves any purpose \[as per Section 8(7)]

**Preferable/ Good practices:**

* Guides the nodal officers in data privacy and protection practices. Makes them aware of the importance of data privacy and protection and legal consequences of breach.
* Check for feedback from employees on access mechanisms and delivering services with proposed levels of data access, masking, etc. (Can use this [sheet](https://ico.org.uk/media/for-organisations/documents/4024005/information-rights-bingo.pdf) as an activity to assess how they are ensuring the privacy rights of residents.)

### &#x20;<a href="#_v29zqws4iu1" id="_v29zqws4iu1"></a>

### **B.5 Stage 4 - UAT and Go-Live** <a href="#_cq77r5nnla5m" id="_cq77r5nnla5m"></a>

#### **B.5.1 **_**What happens at Stage 4?**_ <a href="#_9hhmj0s63k6e" id="_9hhmj0s63k6e"></a>

* The User acceptance test is conducted, a sign-off and go-live permission is given for identified Pilot ULBs
* Setup of review & monitoring cadence.

#### **B.5.2 What does the IA team do at Stage 4?** <a href="#_kigm528x6abx" id="_kigm528x6abx"></a>

#### Assists the AA/Prog in conducting the UAT <a href="#_5nvzs05ktyfi" id="_5nvzs05ktyfi"></a>

* Helps the prog in organizing employee training workshops
* Implements review and monitoring processes

#### **B.5.3. To- Do’s** <a href="#_22qg94blmhiy" id="_22qg94blmhiy"></a>

**Must-haves:**

* Conduct data breach and security checks before the AA/Prog signs off on the UAT.

A data security checklist should include-

* Personally identifying information **(PII)** data encrypted/masked when shared
* Data is stored in safe databases
* Employees don’t openly share access logins
* Limited - documented roles have access to PII,
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

* IA continues to check for any issues in the data governance of the modules

### &#x20;<a href="#_i6wqf8x24rg" id="_i6wqf8x24rg"></a>

### **B.6 Stage 5 - Statewide / ULB-wide Rollout** <a href="#_io252m2fjut6" id="_io252m2fjut6"></a>

#### **B.6.1 **_**What happens at Stage 5?**_ <a href="#_kyep9xxv6c1z" id="_kyep9xxv6c1z"></a>

* Statewide Rollout in batches
* Help desk effectiveness assured
* Critical bugs fixed
* Program success metrics tracking kick-started&#x20;

#### **B.6.2 What does the IA do at Stage 5?** <a href="#_m7caai2edcq2" id="_m7caai2edcq2"></a>

* The IA finishes their implementation function and starts transitioning out of the program
* Begins hand overs and closing gaps if any

#### **B.6.3 To-Do’s:** <a href="#_klgpkmocdu96" id="_klgpkmocdu96"></a>

**Must-haves:**

* Hand over all data they hold, without making a second copy
* Provides an authorized letter to the Prog of such handover for credibility
* Employees of IA begin surrendering logins and role controls
* IA leaves no endpoint access for itself ( unless permitted by the AA or Prog)

**Preferable/Good practices:**

* Avoids allowing its employees to see PII even while helping AA/Prog employees

### &#x20;<a href="#_dm7c7zbmjjwj" id="_dm7c7zbmjjwj"></a>

### **B.7. Stage 6- SUSTENANCE & ONGOING IMPROVEMENT** <a href="#_1aj7kypxyzez" id="_1aj7kypxyzez"></a>

#### **B.7.1. What happens at Stage 6?** <a href="#_pyngu51yqgh7" id="_pyngu51yqgh7"></a>

* The first batch of ULBs have been made live after the Pilot.
* There is the adoption of the platform in the program’s jurisdictional zone and amongst its ULB employees and citizens.

#### **B.7.2 What does the IA do at this stage?** <a href="#_6qsohvpqlcda" id="_6qsohvpqlcda"></a>

* IA implements and leaves the program

#### **B.7.3 To-Do’s:** <a href="#_lgfnqd8qitk4" id="_lgfnqd8qitk4"></a>

**Must-haves:**

* IA completely detaches itself from the program system ( no backdoor entry/logins, no roles accessing PII, no backup of data)

**Preferable/Good practices:**

* IA documents how it enabled privacy preserving implementation modules and makes it available for other players in the implementation ecosystem to pick from

1.  Sec 2(k) “Data Processor” means any person who processes personal data on behalf of a Data Fiduciary;

    Sec 2(t) “personal data” means any data about an individual who is identifiable by or in relation to such data;

    Sec 2 (x) “processing” in relation to personal data, means a wholly or partly automated operation or set of operations performed on digital personal data, and includes operations such as collection, recording, organisation, structuring, storage, adaptation, retrieval, use, alignment or combination, indexing, sharing, disclosure by transmission, dissemination or otherwise making available, restriction, erasure or destruction ↑
2. Sec 2 (i) “Data Fiduciary” means any person who alone or in conjunction with other persons determines the purpose and means of processing of personal data ↑
3. [Digital Personal Data Protection Act 2023.pdf (meity.gov.in)](https://www.meity.gov.in/writereaddata/files/Digital%20Personal%20Data%20Protection%20Act%202023.pdf) ↑
4. The Information Technology Act, 2000 prescribe monetary fines and imprisonment on breaches of data and confidentiality of citizens. ↑
5. Refer to the principle of data minimisation and storage limitation [here](https://docs.google.com/document/d/10bsSWEmf2ebjNpGBs-BLXAVyL-sVFQ901GzuKpbNNyY/edit) ↑
6. For each item of data collected, stored, processed, or shared, there should be a clear purpose identified; this purpose must flow from a legitimate task that the entity collecting it (i.e. a ULB) is mandated & authorized to perform (hence, legitimate), and this purpose must be communicated to the citizen. This is closely related to the concepts of data minimisation, purpose limitation, and role-based access. ↑
7. The proportionality test was prescribed for in the J.Puttaswamy judgement. This test is for data processing bodies to analyse how much of a risk does the use of the data put the person to whom the data belongs versus the benefits its bringing to that person simultaneously. A balance between the benefits and the risks must be found. ↑
8. An assessment of harms should consider such key factors as: (i) the likelihood of occurrence of harms, (ii) potential magnitude of harms and (iii) potential severity of harms. Additionally, the assessment should take into account the digital literacy of both potential users of data and those individuals whose data is being used. ↑
