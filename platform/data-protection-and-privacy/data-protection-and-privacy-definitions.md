# Data Protection & Privacy Definitions

## 1. Data <a href="#_yentqjvvd4su" id="_yentqjvvd4su"></a>

For the purposes of this document, data is any information shared by citizens or received from existing databases to enable government service delivery and government operations. It could be name, address, mobile number, age etc.

Under Indian law, The current Digital Personal Data Act of 2023 defines data as:

Sec 2(h) - “Data” means a representation of information, facts, concepts, opinions or instructions in a manner suitable for communication, interpretation or processing by human beings or by automated means.

Very similar to what is defined as ‘data’ in the Information Technology Act of 2000 as:

[_Data means_](https://www.indiacode.nic.in/bitstream/123456789/13116/1/it\_act\_2000\_updated.pdf) _a representation of information, knowledge, facts, concepts or instructions which are being prepared or have been prepared in a formalized manner and are intended to be processed, is being processed or has been processed in a computer system or computer network, and may be in any form (including computer printouts magnetic or optical storage media, punched cards, punched tapes) or stored internally in the memory of the computer._

### 1a) Personal Data or Personally Identifiable Information (PII) <a href="#_1lca5d9c5mtd" id="_1lca5d9c5mtd"></a>

For the purposes of this document, PII and personal data are to mean the same.

Personal data is defined under the Digital Personal Data Act,2023 as:

Sec 2 (t) - “Personal data” means any data about an individual who is identifiable by or in relation to such data;

To add, a breach of personal data is also defined in Section 2 (u) as -:

“Personal data breach” means any unauthorised processing of personal data or accidental disclosure, acquisition, sharing, use, alteration, destruction or loss of access to personal data, that compromises the confidentiality, integrity or availability of personal data;

[Another definition of personal data](https://www.meity.gov.in/writereaddata/files/GSR313E\_10511\(1\)\_0.pdf) is “_any data that allows one to be recognised either directly or indirectly. It is defined as any information that relates to a natural person, which, either directly or indirectly, in combination with other information available or likely to be available with a body corporate, is capable of identifying such a person_.”

Both the above definitions of personal data are to be read together until the government fixates on maintaining one.

### 1b) Sensitive Personal Data (SPD) <a href="#_xikrf6lxc5nf" id="_xikrf6lxc5nf"></a>

Sensitive Personal data of a person means _“...such personal information which consists of information relating to:_

* _password;_
* _financial information such as Bank account, credit card, debit card or any other payment instrument details;_
* _physical, physiological and mental health conditions;_
* _sexual orientation;_
* _medical records and history;_
* _biometric information;_
* _any detail relating to the above clauses as provided to the body corporate for providing service;_
* _and any of the information received under the above clauses by the body corporate for processing, stored or processed under lawful contract or otherwise_

_Provided that, any information that is freely available or accessible in the public domain or furnished under the_ [_Right to Information Act, 200_](#user-content-fn-1)[^1]_5 or any other law for the time being in force shall not be regarded as sensitive personal data or information\[...].”_

## 2. Platform Implementation Cycle <a href="#_rx6mnijpauvk" id="_rx6mnijpauvk"></a>

### 2a) Platform <a href="#_1bcv75quqnpc" id="_1bcv75quqnpc"></a>

For the purposes of this document, ‘platform’ [<mark style="color:blue;">refers to any software system</mark>](#user-content-fn-2)[^2] that can be used by a government entity, or by a contractor performing any tasks on behalf of that government entity. The term ‘platform’ refers to the software (code) itself, and NOT to any implementation of that code. Therefore, a platform does not collect, store, process, use, or share data.

For example, [DIGIT](https://github.com/egovernments/DIGIT-OSS) is a platform.

### 2b) Platform Implementation <a href="#_ncmhzenifdb0" id="_ncmhzenifdb0"></a>

For the purposes of this document, a ‘Platform Implementation’ refers to each instance of a platform/software system that has been implemented.

* During the implementation of a platform, the implementing agency may collect, store, process, use, and share such data as is necessary for implementing the platform. This will normally be specified in the contract or agreement between the implementing agency and the administrative authority responsible for that implementation.
* After the implementation of a platform is complete, the implementing agency should cease to have access to data from the platform implementation, except to such extent as may be agreed between the implementing agency and the administrative authority responsible for that implementation.
* In cases where the implementing agency performs the role of a support agency with respect to any platform implementation, the implementing agency may have access to data as specified for [<mark style="color:blue;">that role</mark>](data-protection-and-privacy-definitions.md#\_3qi4g54kifg).
* The activity of platform implementation involves roles having access to datasets flowing through the platform.

For example, MSeva (in Punjab), NagarSewa (in Uttarakhand), eChhawani (in Cantonment Boards), and SUJOG (in Odisha) are platform implementations – they are implementations of the DIGIT platform.

### 2c) Program <a href="#_wtzf7zjqvwhp" id="_wtzf7zjqvwhp"></a>

Any ongoing or to-be-executed delivery of government service or defined government operation is a program.

* During the operation of a program, the program owner (and its staff and contractors) will collect, store, process, use, and share such data as is necessary for performing their tasks, and/or which they are required to do under prevailing law.

For example, when ULBs in Punjab use the MSeva platform to collect revenues, deliver ULB services, and redress grievances, this is a program.

### 2d) Summary & Comparison Of Platform, Platform Implementation & Program <a href="#_sej66iapdlja" id="_sej66iapdlja"></a>

<table><thead><tr><th width="125"></th><th>Platform</th><th>Platform Implementation</th><th>Program</th></tr></thead><tbody><tr><td><strong>Definition</strong></td><td>Refers to a software system that can be used by govt entities or contractors. The term ‘platform’ refers to the software (code) itself, and NOT to any implementation of that code.</td><td>Refers to each instance of a platform / software system that has been implemented.</td><td>Any delivery of govt services or other govt operations or reforms can be a program. In the context of this document, a program deploys and/or leverages a platform implementation.</td></tr><tr><td><strong>Does it process data?</strong></td><td>No</td><td>Yes</td><td>Yes</td></tr><tr><td><strong>Example</strong></td><td>DIGIT</td><td>MSeva, SUJOG, eChhawani</td><td>ULBs in Punjab / Odisha / Cantonment Boards delivering services using MSeva / SUJOG / eChhawani respectively.</td></tr></tbody></table>

### 2e) Platform Implementation Stages <a href="#_7at5yi5q8wgm" id="_7at5yi5q8wgm"></a>

We describe a platform implementation as progressing across 7 stages.

<table><thead><tr><th width="110">#</th><th width="147">Stage name</th><th width="371">What happens at this stage</th><th>Who handles data at this stage</th></tr></thead><tbody><tr><td>Stage 0</td><td>Program Set-up</td><td>Resources, budgets, procurement and infrastructure is identified and an implementation partner is onboarded.</td><td>None</td></tr><tr><td>Stage 1</td><td>Program Kickoff</td><td>Implementation starts and data is collected from a few identified jurisdictions for testing</td><td><p>Yes.</p><p>IA, Prog</p></td></tr><tr><td>Stage 2</td><td>Solution design</td><td>State-specific configurations are made with processes and workflows being designed. Policy decisions are made at this stage.</td><td><p>Yes.</p><p>IA , Prog</p></td></tr><tr><td>Stage 3</td><td>Customisations and Configurations</td><td>Adoption and performance of the program is measured. UAT (Use acceptance testing) is conducted here.</td><td><p>Yes</p><p>IA,Prog</p></td></tr><tr><td>Stage 4</td><td>UAT and Go live</td><td>The UAT testing is completed, feedback is received and final platform deployment is carried out at all identified jurisdictions.</td><td><p>Yes</p><p>IA, Prog</p></td></tr><tr><td>Stage 5</td><td>Statewide rollout</td><td>Phase-wise implementation of the platform begins. Troubleshooting, support with errors and critical bugs are fixed.</td><td><p>Yes</p><p>IA, Prog, SA</p></td></tr><tr><td>Stage 6</td><td>Sustenance and Ongoing Improvement</td><td>Sustenance and Ongoing Improvement - platform adoption teams are set, adoption is tracked and awareness and reviews on adoption are conducted.</td><td><p>Yes</p><p>Prog, SA</p></td></tr></tbody></table>

## 3. Roles <a href="#_3qi4g54kifg" id="_3qi4g54kifg"></a>

### 3a) Platform Owner (PO) <a href="#_q84w3j6nk7ca" id="_q84w3j6nk7ca"></a>

For the purposes of this document, a platform owner is an entity that owns, governs, or controls the platform's codebase. They are responsible for its architecture design, roadmap, and versions.

As a platform is a code that has NOT been implemented, a platform owner has no access to data.

When a platform is implemented, becoming a platform implementation, the platform owner may have access to such data as is being collected, stored, processed, used, or shared by that platform implementation as may be agreed upon by the platform owner and the administrative authority responsible for that implementation.

In cases where a platform owner performs the roles of an implementing agency or support agency with respect to any platform implementation, the platform owner may have access to data as specified for those roles (see below).

For example, eGovernments Foundation is a platform owner.

### 3b) Implementing Agency (IA) <a href="#_8fq1xrj0s6f2" id="_8fq1xrj0s6f2"></a>

An agency that deploys and configures a platform for the administrative authority or program owner (see below) is an implementing agency **(IA)**. An IA may:

* set up the hardware necessary for the program;
* customise, extend, configure, and install/set up the software (platform) as per the needs of the program owner;
* train staff or contractors of the program owner on how to use the platform;
* Perform other such functions to ensure program readiness as may be agreed upon between the implementing agency and the program owner and/or administrative authority responsible for such platform implementation.

During the implementation of a platform, the implementing agency may collect, store, process, use, and share such data as is necessary for implementing the platform. This will normally be specified in the contract or agreement between the implementing agency and the administrative authority responsible for that implementation.

After the implementation of a platform is complete, the implementing agency should cease to have access to data from the platform implementation, except to such extent as may be agreed between the implementing agency and the administrative authority responsible for that implementation.

In cases where the implementing agency performs the role of a support agency with respect to any platform implementation, the implementing agency may have access to data as specified for that role (see below).

For example, if a given state government signs a contract with ‘Company L’ to implement the DIGIT platform in that state, Company L is an IA.

### 3c) Program Owner (Prog) <a href="#_90h2197sguap" id="_90h2197sguap"></a>

For the purposes of this document, a ‘program owner’ is the entity responsible for the delivery of specific public goods, services, or social welfare. A program owner is usually a government entity (though they may contract private entities to perform some or all of these tasks on their behalf).

In the context of a platform implementation, the program owner is the primary client of the implementing agency, as they will use the platform implementation to perform their tasks.

A program owner (and its staff and contractors) will collect, store, process, use, and share such data as is necessary for performing their tasks, and/or which they are required to do under prevailing law.

A program owner has primary responsibility for ensuring that all relevant legal provisions and good practices with respect to data security, data protection, and privacy are being followed in its programs.

A program owner may perform the roles of implementing agency and/or support agency or may contract those roles out to third-party implementing agencies and support agencies respectively. If they are performing these roles, they will have access to such data as is specified for these roles.

A program owner is typically subordinate to the administrative authority in the official/administrative hierarchy. It is also possible that the administrative authority and program owner are the same entity.

For example, if a given state government has initiated a program to use the DIGIT platform to reform urban governance in that state, either each Urban Local Body in that state or the Housing and Urban Development Department of that state is a program owner.

### 3d) Support Agency (SA) <a href="#_dda06cna3d29" id="_dda06cna3d29"></a>

For the purposes of this document, a ’Support Agency’ is one that provides support in any functional aspect required by the program owner with respect to that platform implementation (e.g. assistance in the maintenance of the platform, technical or operational problem-solving, bug/error resolution).

A support agency would normally be engaged once the platform has gone live, i.e. during stages 5 and/or 6 of platform implementation (see above).

A support agency will have access to such data as is necessary to perform their functions, and this shall normally be specified in the agreement/contract between the supporting agency and the program owner / administrative authority responsible for that platform implementation / the implementing agency responsible for that platform implementation (in cases where the implementing agency sub-contracts support functions to the supporting agency).

In cases where a platform owner, implementing agency, or program owner performs the role of a support agency, they may have access to such data as is specified for that role.

For example, if a given state government signs a contract with ‘Company L’ to implement the DIGIT platform in that state, and Company L sub-contracts support/maintenance/helpdesk activities to ‘Company M’, Company M is an IA.

### 3e) Administrative Authority (AA) <a href="#_g1dw1k3q2q3y" id="_g1dw1k3q2q3y"></a>

For the purposes of this document, an administrative authority **(AA)** is a government entity that has the authority to enter into contracts/agreements with the platform owner, implementing agency, and supporting agency.

An administrative authority has the power, under prevailing law, to permit other entities to access (collect, store, process, use, and/or share) data, including the PII of individuals within the territorial jurisdiction of that AA.

For the purposes of this document, a platform owner, implementing agency, or supporting agency cannot access data unless authorised to do so by the administrative authority. Such authorisation may be specified in an agreement/contract between the administrative authority and these entities. Such authorisation must be in keeping with prevailing laws and shall include such provisions and safeguards as are required under prevailing law.

An administrative authority may be a program owner or maybe a superior agency of a program owner in the administrative hierarchy.

For example, when a given state government decides to implement the DIGIT platform in that state, the specific department of that state government which signs MOUs and/or contracts with eGov Foundation (as platform owner), and with an IA to implement the DIGIT platform, is an AA.

### 3f) Summary & Comparision Of Roles (PO, IA, Prog, SA) <a href="#_hgy8w1f2997l" id="_hgy8w1f2997l"></a>

<table><thead><tr><th width="128"></th><th>Platform Owner (PO)</th><th>Implementing Agency (IA)</th><th>Program Owner (Prog)</th><th>Support Agency (SA)</th></tr></thead><tbody><tr><td><strong>Definition</strong></td><td>The entity that owns, governs, or controls the platform's codebase.</td><td>The entity that deploys and configures a platform for the AA / Prog</td><td>The entity that is responsible for delivery of specific public goods, services, social welfare</td><td>The entity that provides support in any technical / functional aspect required by the Prog, with respect to that platform implementation</td></tr><tr><td><strong>Access to Data</strong></td><td>No, except to extent agreed with Prog / AA</td><td>Yes, during implementation only</td><td>Yes</td><td>Yes, to the extent needed for support</td></tr><tr><td><strong>Example</strong></td><td>eGovernments Foundation</td><td>Systems integrators (e.g. PwC, Transerve)</td><td>State HUDD, each ULB in the state</td><td>Any third party contracted for IT/program support</td></tr></tbody></table>

[^1]: Cl. 3 of the Information Technology (Reasonable security practices and procedures and sensitive personal data or information) Rules, 2011.&#x20;

[^2]: For a more precise technical definition of ‘platform’, as distinct from other types of software, see:&#x20;
