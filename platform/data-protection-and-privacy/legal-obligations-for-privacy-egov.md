---
description: 'Privacy Law in India: What does it mean for eGov?'
---

# Legal Obligations For Privacy - eGov

## **A1. Provisions In The Constitution Of India** <a href="#_k0bhf3xa51ta" id="_k0bhf3xa51ta"></a>

The Constitution of India does not explicitly provide for the right to privacy.

Privacy has been read into the right to life and personal liberty (Art. 21) in the [judgement of Puttaswamy v. Union of India](https://main.sci.gov.in/supremecourt/2012/35071/35071\_2012\_Judgement\_24-Aug-2017.pdf). Following the judgement, the right to privacy is an inalienable and inherent right under the Constitution, though still an implied one (not explicitly mentioned as such). The judgement created a 4-fold test on the basis of which privacy practices can be created.

### **A2. What Should eGov Do?** <a href="#_jlp0qkpbrdi8" id="_jlp0qkpbrdi8"></a>

The Supreme Court has identified a [<mark style="color:blue;">4-step test</mark>](#user-content-fn-1)[^1] that can measure what potentially affects privacy. eGov should aim at satisfying these tests for privacy compliance.

To satisfy the tests of -

* **Legality (sanctioned by law)**

Every dataset collected, stored, transmitted, analyzed or shared must be done on the basis of legal authority i.e. the entity that is collecting / storing / processing / sharing the data must be able to point to a legal instrument that gives it the power to do those things. For Urban Local Bodies (ULBs), the main source of authority would be [Art. 12 of the Constitution](https://www.constitutionofindia.net/articles/article-12-definitions/), read with [Part IXA (Art. 243P-243ZG)](https://www.writinglaw.com/part-ixa-243p-243zg-the-municipalities/) and the [12th Schedule](https://www.iitk.ac.in/wc/data/coi-4March2016.pdf).

* **Legitimate aim**

For each item of data collected, stored, processed, or shared, there should be a clear purpose identified; this purpose must flow from a legitimate task that the entity collecting it (i.e. a ULB) is mandated & authorized to perform (hence, legitimate), and this purpose must be communicated to the citizen. This is closely related to the [<mark style="color:blue;">concepts of data minimisation</mark>](#user-content-fn-2)[^2], [<mark style="color:blue;">purpose limitation</mark>](#user-content-fn-3)[^3], and [<mark style="color:blue;">role-based access</mark>](#user-content-fn-4)[^4].

* **Proportionality**

Any form of data handling must be tested from a risk-benefit lens. Based on this assessment, we should ask the question: “Is there a less intrusive or lower-risk way to do this?” If yes, we should adopt that method.

* **Appropriate safeguards**

The processes and assessments involved in all of these decisions must be documented. In addition, we can look at multiple layers of safeguards:

1. Role-based access controls
2. Indelible logs and audibility
3. Incident/breach management systems, including notice to legal / investigating authorities and to citizens
4. Consent frameworks
5. Security audits (software and process)

## **B. Provisions In** [**The Information Technology Act, 2000**](https://www.indiacode.nic.in/bitstream/123456789/1999/3/A2000-21.pdf) <a href="#_9i7xvm9hg1qh" id="_9i7xvm9hg1qh"></a>

The IT Act creates a class of entities known as intermediaries, and places obligations upon them with respect to the receipt, storage, transmission, and processing of data.

**Intermediary is defined as -**

_Sec 2 (w) ―intermediary, with respect to any_ [_<mark style="color:blue;">particular electronic records</mark>_](#user-content-fn-5)[^5]_, means any person who on behalf of another person receives, stores or transmits that record or provides any service with respect to that record and includes telecom service providers, network service providers, internet service providers, web-hosting service providers, search engines, online payment sites, online-auction sites, online-marketplaces and cyber cafes._

An intermediary is thus defined as an entity which, on behalf of another person,

* Receives an electronic record
* Stores the electronic record
* Transmits the electronic record
* ‘provides any service with respect to electronic records’.

{% hint style="info" %}
**NOTE:** The exact interpretation of ‘service with respect to electronic records’ has not been established yet. To the extent that eGov can demonstrate that it does not interact with any citizen’s data, this provision may not apply to eGov – i.e. eGov is not an intermediary.
{% endhint %}

### **B.1. Legal Obligations (All Entities)** <a href="#_vn1co6wl71j8" id="_vn1co6wl71j8"></a>

The IT Act places certain obligations and penalties on any/all persons, irrespective of [<mark style="color:blue;">intermediary status</mark>](#user-content-fn-6)[^6].

* **Sec 43** holds any person up for penalties and compensation for _“damage, unauthorised access, illegal downloads, disruption, denial of access, the introduction of the virus among others to a computer, computer system, etc.”_.
  * **Sec 72** makes disclosure of electronic records, information, etc. without consent from the relevant person or authority punishable with imprisonment up to 2 years &/or a fine up to Rs. 1 lakh.
* **Sec 72A** makes disclosure of information without consent and in breach of a lawful contract _with an intent to cause wrongful loss or gain_ punishable with imprisonment up to 3 years &/or a fine of Rs. 5 lakhs.

{% hint style="info" %}
**NOTE:** This section is relevant to all employees and contractors at eGov, in their personal capacity, as well as eGov as an organization. If such a breach occurs due to the actions of an eGov employee/contractor, eGov may be liable to fines.
{% endhint %}

### **B.2. What eGov Must Do** <a href="#_pljodmw58w9g" id="_pljodmw58w9g"></a>

* Tighten access controls
* Tighten security
* Build in consent-taking mechanisms to avoid liability of wrongful disclosure
* Maintain clear contractual liabilities and strictly abide by the contract.

### **B.3. What eGov May Have To Do** <a href="#_lwuo0kcmgzd" id="_lwuo0kcmgzd"></a>

If eGov does interact with citizen data (provides any service with respect to electronic records) then a few obligations as an intermediary are to be complied with -:

* **Sec 67C - Preservation and retention of information by intermediaries**–(1) Intermediary shall preserve and retain information _‘as prescribed by the rules’_. Intentional contravention of this section can lead to imprisonment of up to 3 years and a fine.

{% hint style="info" %}
**NOTE:** The Rules relevant to this Section of the IT Act have not been prescribed yet; in any event, the section will not apply if eGov is not considered an intermediary.
{% endhint %}

* **Sec 79** of the Act allows intermediaries to be exempt from liability for third-party information – where such information is found to be illegal, criminal, harmful etc. – that they stored, transmitted etc., under certain conditions (sometimes known as ‘safe harbour’). The key to safe harbour is that the intermediary was not aware of the information, did not in any way modify or edit it, and did not make decisions about its transmission.

{% hint style="info" %}
**NOTE:** To the extent that eGov would be looked at as an intermediary for processing data, it would fall outside the protection of this provision; however, the question of whether ‘services’ extend to automated processing is still in debate. In any event, the section will not apply if eGov is not considered an intermediary.
{% endhint %}

* **Sec 43A** read with the **Information Technology (Reasonable Security Practices and Procedures and Sensitive Personal Data or Information) Rules, 2011** mandates bodies corporate to provide a privacy policy, to collect, transfer, and disclose information in a mandated manner, and to maintain reasonable security practices and procedures as provided in the Rules.

{% hint style="info" %}
**NOTE:** eGov is not a ‘body corporate’ within the meaning of the IT Act/Rules. Nonetheless, given that our software is intended to be used by governments, and will be used to collect/store/process large volumes of citizens’ personal data (including sensitive personal data), eGov should abide by the guidelines as a matter of responsibility & good practice.
{% endhint %}

The new changes in the IT law have now removed the 2011 rules and replaced them with the Information Technology (Intermediary Guidelines and Digital Media Ethics Code) Rules, 2021. These rules obligate intermediaries to -:

**Publish,** in English language or any [<mark style="color:blue;">other language suitable to the user</mark>](#user-content-fn-7)[^7], their privacy policy, user agreement for access and use of our products and services as well as the rules and regulations that apply to anyone using our products and services.

The rules eGov sets for the usage of its products and services must be designed on the following principles -:

No one is allowed to host, display, upload, modify, publish, transmit, store, update, or share any information -

* that one does not have any rights over and does not belong to that person (third-party information),
* defamatory, obscene, pornographic, paedophilic, invasive of another‘s privacy, including bodily privacy, insulting or harassing on the basis of gender, libellous, racially or ethnically objectionable, relating or encouraging money laundering or gambling, or otherwise inconsistent with or contrary to the laws in force;
* is harmful to any child;
* infringes any patent, trademark, copyright or other proprietary rights;
* violates any law for the time being in force;
* deceives or misleads the addressee about the origin of the message or knowingly and intentionally communicates any information which is patently false or misleading but may reasonably be perceived as a fact;
* impersonates another person;
* threatens the unity, integrity, defence, security or sovereignty of India, friendly relations with foreign States, or public order, or causes incitement to the commission of any cognisable offence or prevents investigation of any offence or is insulting other nation;
* contains software virus or any other computer code, file or program designed to interrupt, destroy or limit the functionality of any computer resource;
* is patently false and untrue, and is written or published in any form, with the intent to mislead or harass a person, entity or agency for financial gain or to cause any injury to any person;

**Inform** users that non-compliance with any rules/privacy policy or user agreement would lead to immediate termination of access/usage of eGov products/services and deletion of such content.

## **C. Provisions Of The Digital Personal Data Protection Act, 2023 (DPDP Act)** <a href="#_qy17ysr0nz7h" id="_qy17ysr0nz7h"></a>

Presently, the **‘Act’** enters into force as a stand-alone legislation to protect digital personal data i.e. all personal data available in a digital form.

Definitions -:

* [<mark style="color:blue;">Personal data</mark> ](#user-content-fn-8)[^8]means any data about an individual who is identifiable by or in relation to such data.
* [<mark style="color:blue;">The new Act</mark>](#user-content-fn-9)[^9] defines bodies such as the data fiduciary, data processor and significant data fiduciary.
* [<mark style="color:blue;">Processing in relation to personal data</mark>](#user-content-fn-10)[^10] means a wholly or partly automated operation or set of operations performed on digital personal data and includes operations such as collection, recording, organisation, structuring, storage, adaptation, retrieval, use, alignment or combination, indexing, sharing, disclosure by transmission, dissemination or otherwise making available, restriction, erasure or destruction.

As we wait for further clarification and rules to be passed to better understand the law, we explore the parts of the law that are relevant to eGov, when it plays different roles in its functions.

### **C. 1 Role eGov Plays & Corresponding Duties Under The Act** <a href="#_j6weu4s0qslq" id="_j6weu4s0qslq"></a>

#### C.1.1 eGov as a Platform Owner (PO) <a href="#_t1oqjjklnqap" id="_t1oqjjklnqap"></a>

As a [platform owner](data-protection-and-privacy-definitions.md#\_3qi4g54kifg), eGov would not deal with data at all. It would simply create the code base and hand over the platform to the [administering authority](data-protection-and-privacy-definitions.md#\_g1dw1k3q2q3y) or implementation agency for integration.

There would be no interaction with data - no personal data would be touched and therefore this Act would not be attracted by eGov.

#### C.1.2. eGov as an Implementation Agency or Supporting Agency <a href="#_e8yhqrg5t9pj" id="_e8yhqrg5t9pj"></a>

eGov may decide to take up the role of a [Supporting agency](data-protection-and-privacy-definitions.md#\_dda06cna3d29) or [Implementation agency](data-protection-and-privacy-definitions.md#\_8fq1xrj0s6f2).

As with any of the above two roles, eGov would be a data processor i.e. it would [<mark style="color:blue;">process personal data</mark>](#user-content-fn-11)[^11] on behalf of or on the instructions of the [<mark style="color:blue;">administering authorities</mark>](#user-content-fn-12)[^12] or [program owners](data-protection-and-privacy-definitions.md#\_90h2197sguap).

As an Implementation agency (IA): Where eGov is contracted to deploy and configure its platform into the administrative authority or program owner's systems, functioning as an implementing agency, eGov would be involved in setting up the hardware necessary for the program; OR customise, extend, configure, and install/set up the software (platform) as per the needs of the program owner; OR train staff or contractors of the program owner on how to use the platform; OR perform other such functions to ensure program readiness as may be agreed upon between the implementing agency and the program owner and/or administrative authority responsible for such platform implementation. As an IA, eGov would have access to data (the extent of such access to data may be defined in the agreement between the administering authority and eGov as an IA). Till the time eGov does not decide the purposes and the means of processing, it will remain a processor and not become a data fiduciary.

As a Supporting agency (SA): As an SA, eGov would provide support in any functional aspect required by the program owner with respect to that platform implementation (e.g. assistance in the maintenance of the platform, technical or operational problem-solving, bug/error resolution). SA will have access to such data as is necessary to perform their functions, and this shall normally be specified in the agreement/contract between the supporting agency and the program owner / administrative authority.

Being an IA and a SA would make eGov a processor of data under the Act. (Refer to the definition of a data processor above).

#### C.1.3. As a processor as per the Act: <a href="#_3yw4pijd1i3m" id="_3yw4pijd1i3m"></a>

_C.1.3.1 Indirect obligations:_

The Act holds the data fiduciary responsible for the actions and functions of the data processor. The fiduciary would hire the processor to conduct the relevant processing.

It is to be assumed that an indirect burden of obligations under this law for the data fiduciary is also applicable to the data processor (Section 8 (1) is applicable to the data fiduciary and in parallel to data processors). Hence the must-do’s for processors are to be widely read into the obligations of the data fiduciaries as well.

There are obligations that are applicable to the data fiduciary but involve the function of the processor and include processing. It may then become an indirect obligation on the data processor as well)

eGov may be instructed or mandated to do the below by the data fiduciary -:

* Maintain the completeness, accuracy, and consistency of personal data \[ Section 8(3)]
* Implement appropriate technical and organizational measures to implement the Act \[Sec 8(4)]
* Intimate the data fiduciary on any personal data breach \[so that the data fiduciary can inform the Board and data principal about such a breach - Sec 8(6)]

_C.1.3.2 Direct obligations/ Must do’s for eGov as a data processor_

Below are a few specific obligations the law provides for to be followed by the data processors ( therefore to eGov as a processor)

* Process any data only if there is a valid contract between the administering authority and eGov ( data fiduciary & processor) \[Sec 8(2)]
* Maintain security safeguards to prevent personal data breach \[Sec 8(5)]
* Follow the instructions given by the data fiduciary on data deletion
* Follow processing standards issued through Central government policies ( as issued under Sec 7(b)(ii) - yet to be issued)
* Maintain a record of data processed ( to assist the data fiduciary i.e. the relevant administering authority with obligation Sec 11 of the Act).

[^1]: “(i) The action must be sanctioned by law; (ii) The proposed action must be necessary in a democratic society for a legitimate aim; (iii) The extent of such interference must be proportionate to the need for such interference; (iv) There must be procedural guarantees against abuse of such interference.”&#x20;

[^2]: Do not collect what you do not need to collect.

[^3]: Data collected for a given purpose can be used only for that purpose.&#x20;

[^4]: Only a person whose role requires access to given data will be able to view / process that data. If the role does not require access to given data, that data will not be shared with them.

[^5]: _Sec 2(o) **data** means a representation of information, knowledge, facts, concepts or instructions which are being prepared or have been prepared in a formalized manner, and is intended to be processed, is being processed or has been processed in a computer system or computer network, and may be in any form (including computer printouts magnetic or optical storage media, punched cards, punched tapes) or stored internally in the memory of the computer._

    _Sec 2 (t) ―an **electronic record**- means data, record or data generated, image or sound stored, received or sent in an electronic form or micro film or computer generated micro fiche_;&#x20;

[^6]: Also applicable if you are a government official (employee - domain level or counter level, a document verifier, field inspector, approver, clerk), or a platform provider, vendor/contractor, system administrator, IT administrator or IT team member and you receive, store or transmit data&#x20;

[^7]: As per the Eight Schedule of the Indian Constitution, following are the languages which can be used -: Assamese, Bengali, Gujarati, Hindi, Kannada, Kashmiri, Konkani, Malayalam, Manipuri, Marathi, Nepali, Oriya, Punjabi, Sanskrit, Sindhi, Tamil, Telugu, Urdu, Bodo, Santhali, Maithili and Dogri.&#x20;

[^8]: Sec 2(t)&#x20;

[^9]: Section 2 (i), (k), and (l) respectively&#x20;

[^10]: Sec 2(x)

[^11]: Sec 2 (x), processing of personal data means a wholly or partly automated operation or set of operations performed on digital personal data and includes operations such as collection, recording, organisation, structuring, storage, adaptation, retrieval, use, alignment or combination, indexing, sharing, disclosure by transmission, dissemination or otherwise making available, restriction, erasure or destruction&#x20;

[^12]: As a data fiduciary i.e. who decides the purpose and means of processing the personal data)
