---
description: User data privacy design and principles
---

# ❕ Privacy

Privacy is a shared responsibility. DIGIT building blocks enable, wherever possible, ease of privacy compliance. Guidelines are provided for Platform teams, Product teams, and Program teams, which they must adhere to to ensure privacy.

### Principles

DIGIT is designed to ensure and enable the following Privacy Principles and Practices.

* [x] Principle 1 - Secure by Default
  * Practice 1.1 - All data must be stored and transmitted securely
  * Practice 1.2 - Access to data must be role-based, and only roles which have a well-defined purpose for accessing that data should be able to access it.
* [x] Principle 2 - Privacy by Default&#x20;
  * Practice 2.1 - Identify and Encrypt PII data.&#x20;
  * Practice 2.2 - All changes to data must be recorded in a signed audit log.&#x20;
* [x] Principle 3 - Ownership&#x20;
  * Practice 3.1 - Citizens should have an original (verified) copy of their data
  * Practice 3.2 - Citizens should be able to request for correction, with required proofs.
* [x] Principle 4 - Consent
  * Practice 4.1 - Agencies collecting the data must have a published privacy policy.&#x20;
  * Practice 4.2 - Explicit Consent must be taken if PII data is being exchanged/shared with other agencies, except where local laws provide for such sharing.
* [x] Principle 5 - Purpose Limitation/Minimisation -&#x20;
  * Only data with a well-defined purpose must be collected.&#x20;

### Capabilities

DIGIT core building blocks provide the following capabilities to enable these principles and practices.&#x20;

1. API Gateway ensures that no data is accessible without authentication and authorisation.
2. User Services provides authentication services.
3. Role Services provides the ability to configure roles and limit access each role has to specified data and services.&#x20;
4. Encryption Services provides the ability to encrypt all the data.&#x20;
5. Audit Services logs all changes made to all data in a signed audit log.
6. Persister Service emits data which is stored as Signed Verifiable Certificates in certificate service. This can be pushed into Citizen Data Wallets, if available. (Ongoing - Expected Release Date - March 2024)
7. Consent Adapter enables external consent frameworks, such as India's Account Aggregator, to access data from DIGIT.  (Planned - Expected Release Date - June 2024)

### Guidelines

Below listed are the privacy guidelines that teams building products on DIGIT and implementing programs leveraging Products built on DIGIT must adhere to.

1. Ensure privacy policy in compliance with the local laws is published with every solution deployed in production.&#x20;
2. Identify all PII, and ensure these are stored as part of User and Individual Service only.
3. Configure the roles and access based on purpose -- only roles that have a purpose should be able to access that data.
4. Provide users/roles only the minimal access required to perform their activity.
5. Design forms to capture only such data from users that have well-defined purposes.&#x20;
6. Leverage Persister Service when storing data.
7. Leverage Encryption Service to encrypt sensitive data before storage.
8. Archive and/or store data keeping in mind the local laws, regulations, and requirements of the domain. Where possible to store aggregate or anonymised data, do so rather than storing PII.
9. Anonymise PII before emitting data for analysis or reporting.
10. Provide citizens with the ability to view and request changes to their personal data.&#x20;

