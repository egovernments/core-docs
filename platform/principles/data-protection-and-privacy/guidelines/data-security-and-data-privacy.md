# Data Security and Data Privacy

## **Objective**

This document focuses on deciding whether Personal identification information collected in each rainmaker module is used for data security and privacy purposes.

**Target Audience:** This document is intended for Engineering (tech team), Product Management and Implementation team to agree on requirements for data privacy and data security.

## **Introduction**

As a product provider to the government, we should be responsible for the data security of individuals and organizations who are using our products. The first step in data privacy and security is to identify personal identification information (PII) which will then decide our approach to data security. The personal identification information listed in this document is decided with the help of ‘WHITE PAPER OF THE COMMITTEE OF EXPERTS ON A DATA PROTECTION FRAMEWORK FOR INDIA’. The remarks and provisional views of the committee are given below:

### **Justice Srikrishna Committee On Personal Identification Information (PII)**

All information about an individual is not personal data. As stated earlier, the protection of identity is central to informational privacy. So the information must be such that the individual is either identified or identifiable from such information. In statutes or instruments which use both these terms “**identified or identifiable**” such as the EU GDPR, it refers to states in which the data can exist. Data could be in a form where individuals stand identified or in other cases, it is possible that they could be identified. Whether an individual is identifiable or not is a question of context and circumstances. For instance, a car registration number, by itself, does not reveal the identity of a person. However, it is possible that with other information, an individual can be identified from this information.

Provisional views of the committee on Personal Data:

1. It is data about/relating to an individual that may be the subject matter of protection under the law. Data in this context ought to include any kind of information including opinions or assessments irrespective of their accuracy.
2. Data from which an individual is identified or identifiable/reasonably identifiable may be considered to be personal data. The identifiability can be direct or indirect.
3. New technologies pose considerable challenges to this distinction based on identifiability. This standard may have to be backed up by codes of practice and guidance notes indicating the boundaries of personal information having regard to the state of technology.

On the basis of the above comments potential information from rainmaker modules i.e. PGR, PT and TL were identified and the storage of information in each module was analysed as below.

## **Terms Used & Definitions**

1. **Primary PII:** With the help of given information individual can be directly identified
2. **Secondary PII:** With the help of given information an individual can not be identified directly but an individual can be identified if this information is available with one of primary PII.
3. **Independent PII:** With the help of given information individual cannot be identified directly but this information can help the receiver to identify an individual through other means like search for property tax/ trade license or electricity connections
4. **Sensitive info:** Password, Gender, Bank account number is sensitive information which needs to be protected

Module-wise data points required to secure are given below:

### PGR

| **Segment** | **Data Point**        | **Primary or Secondary PII** | **Identified/ identifiable** | **Information stored in** |
| ----------- | --------------------- | ---------------------------- | ---------------------------- | ------------------------- |
| **Citizen** | Name                  | Primary                      | Identified                   | User Service              |
| **Citizen** | Mobile Number         | Primary                      | Identified                   | User Service              |
| **Citizen** | City                  | Secondary                    | Identifiable                 | User Service              |
| **Citizen** | Password              | Sensitive info               | Sensitive info               | User Service              |
| **Citizen** | Street Name/ Locality | Secondary                    | Identifiable                 | Property Module           |
| **AO**      | Name                  | Primary                      | Identified                   | User Service              |
| **AO**      | Mobile Number         | Primary                      | Identified                   | User Service              |
| **AO**      | City                  | Secondary                    | Identifiable                 | User Service              |
| **AO**      | Password              | Sensitive info               | Sensitive info               | User Service              |
| **LME**     | Name                  | Primary                      | Identified                   | User Service              |
| **LME**     | Mobile Number         | Primary                      | Identified                   | User Service              |
| **LME**     | City                  | Secondary                    | Identifiable                 | User Service              |
| **LME**     | Password              | Sensitive info               | Sensitive info               | User Service              |
| **Admin**   | Name                  | Primary                      | Identified                   | User Service              |
| **Admin**   | Mobile Number         | Primary                      | Identified                   | User Service              |
| **Admin**   | City                  | Secondary                    | Identifiable                 | User Service              |
| **Admin**   | Password              | Sensitive info               | Sensitive info               | User Service              |

### Trade License

| **Segment**                | **Data Point**             | **Primary or Secondary PII** | **Identified/ identifiable** | **Information stored in** |
| -------------------------- | -------------------------- | ---------------------------- | ---------------------------- | ------------------------- |
| **Trade Location Details** | Property ID                | Independent                  | Identifiable                 | Property Module           |
| **Trade Location Details** | Electricity Connection No. | Independent                  | Identifiable                 | TL Module                 |
| **Owner Information**      | Name                       | Primary                      | Identified                   | User Service              |
| **Owner Information**      | Mobile No.                 | Primary                      | Identified                   | User Service              |
| **Owner Information**      | Father/Husband's Name      | Primary                      | Identified                   | User Service              |
| **Owner Information**      | Email                      | Primary                      | Identified                   | User Service              |
| **Owner Information**      | PAN No.                    | Independent                  | Identifiable                 | User Service              |
| **Owner Information**      | Correspondence Address     | Primary                      | Identifiable                 | User Service              |
| **Owner Information**      | DOB                        | Secondary                    | Identifiable                 | User Service              |
| **Documents**              | Owner's ID Proof           | Independent                  | Identified                   | Files store               |
| **Documents**              | Ownership Proof            | Independent                  | Identified                   | Files store               |
| **Documents**              | Owner’s photo              | Independent                  | Identified                   | Files store               |
| **Documents**              |                            |                              |                              |                           |
| **Payer Information**      | Name                       | Primary                      | Identified                   | Collections               |
| **Payer Information**      | Mobile No.                 | Primary                      | Identified                   | Collections               |
| **Counter Employee**       | Name                       | Primary                      | Identified                   | User Service              |
| **Counter Employee**       | Mobile Number              | Primary                      | Identified                   | User Service              |
| **Counter Employee**       | City                       | Secondary                    | Identifiable                 | User Service              |
| **Counter Employee**       | Password                   | Sensitive info               | Sensitive info               | User Service              |
| **Approver**               | Name                       | Primary                      | Identified                   | User Service              |
| **Approver**               | Mobile Number              | Primary                      | Identified                   | User Service              |
| **Approver**               | City                       | Secondary                    | Identifiable                 | User Service              |
| **Approver**               | Password                   | Sensitive info               | Sensitive info               | User Service              |

### Property Tax:

| **Segment**           | **Data Point**                               | **Primary or Secondary PII** | **Identified/ identifiable** | **Information stored in** |
| --------------------- | -------------------------------------------- | ---------------------------- | ---------------------------- | ------------------------- |
| **Property Address**  | City                                         | Secondary                    | Identifiable                 | Property Module           |
| **Property Address**  | House No                                     | Secondary                    | Identifiable                 | Property Module           |
| **Property Address**  | Building Name                                | Secondary                    | Identifiable                 | Property Module           |
| **Property Address**  | Door No                                      | Primary                      | Identifiable                 | Property Module           |
| **Property Address**  | Street Name Locality                         | Secondary                    | Identifiable                 | Property Module           |
| **Property Address**  | Pincode                                      | Secondary                    | Identifiable                 | Property Module           |
| **Property Address**  | Existing Property ID                         | Independent                  | Identifiable                 | Property Module           |
| **Owner Information** | Name                                         | Primary                      | Identified                   | User Service              |
| **Owner Information** | Gender                                       | Sensitive info               | Sensitive info               | User Service              |
| **Owner Information** | Mobile Number                                | Primary                      | Identified                   | User Service              |
| **Owner Information** | Father/Husband’s Name                        | Primary                      | Identified                   | User Service              |
| **Owner Information** | Relationship                                 | Secondary                    | Identifiable                 | User Service              |
| **Owner Information** | Special Category                             | Primary                      | Identifiable                 | User Service              |
| **Owner Information** | ID of Document belonging to special category | Primary                      | Identified                   | User Service              |
| **Owner Information** | Email ID                                     | Primary                      | Identified                   | User Service              |
| **Owner Information** | Correspondence Address                       | Secondary                    | Identifiable                 | User Service              |
| **Property Tax**      | Property unique ID                           | Independent                  | Identifiable                 | Property Module           |
| **Payer Information** | Name                                         | Primary                      | Identified                   | Collections               |
| **Payer Information** | Mobile No.                                   | Primary                      | Identified                   | Collections               |
| **Counter Employee**  | Name                                         | Primary                      | Identified                   | User Service              |
| **Counter Employee**  | Mobile Number                                | Primary                      | Identified                   | User Service              |
| **Counter Employee**  | CIty                                         | Secondary                    | Identifiable                 | User Service              |
| **Counter Employee**  | Password                                     | Sensitive info               | Sensitive info               | User Service              |

### Water & Sewerage

| **Segment**            | **Data Point**            | **Primary or Secondary PII** | **Identified/ identifiable** | **Information stored in** |
| ---------------------- | ------------------------- | ---------------------------- | ---------------------------- | ------------------------- |
| **Property Address**   | City                      | Secondary                    | Identifiable                 | Property Module           |
| **Property Address**   | House No                  | Secondary                    | Identifiable                 | Property Module           |
| **Property Address**   | Building Name             | Secondary                    | Identifiable                 | Property Module           |
| **Property Address**   | Plot/House/Survey No      | Secondary                    | Identifiable                 | Property Module           |
| **Property Address**   | Property ID               | Independent                  | Identifiable                 | Property Module           |
| **Property Address**   | Street Name Locality      | Secondary                    | Identifiable                 | Property Module           |
| **Property Address**   | Pincode                   | Secondary                    | Identifiable                 | Property Module           |
| **Owner Information**  | Name                      | Primary                      | Identified                   | User Service              |
| **Owner Information**  | Gender                    | Sensitive info               | Sensitive info               | User Service              |
| **Owner Information**  | Mobile Number             | Primary                      | Identified                   | User Service              |
| **Owner Information**  | Guardian Information      | Primary                      | Identified                   | User Service              |
| **Owner Information**  | Relationship              | Secondary                    | Identifiable                 | User Service              |
| **Owner Information**  | Owner Category            | Secondary                    | Identifiable                 | User Service              |
| **Owner Information**  | Correspondence Address    | Primary                      | Identified                   | ?                         |
| **Owner Information**  | Email ID                  | Primary                      | Identified                   | User Service              |
| **Connection Details** | Meter ID                  | Independent                  | Identifiable                 | W\&S Module               |
| **Connection Details** | Consumer Number (OId/New) | Independent                  | Identifiable                 | W\&S Module               |

### OBPAS

| **Segment**                            | **Data Point**           | **Primary or Secondary PII** | **Identified/ identifiable** | **Information stored in** |
| -------------------------------------- | ------------------------ | ---------------------------- | ---------------------------- | ------------------------- |
| **Applicant info**                     | Applicant name           | Primary                      | Identified                   | User service              |
| **Applicant info**                     | Applicant mobile number  | Primary                      | Identified                   | User service              |
| **Owner Information**                  | Name                     | Primary                      | Identified                   | User Service              |
| **Owner Information**                  | Gender                   | Sensitive info               | Sensitive info               | User Service              |
| **Owner Information**                  | Mobile Number            | Primary                      | Identified                   | User Service              |
| **Owner Information**                  | Father/Husband’s Name    | Primary                      | Identified                   | User Service              |
| **Owner Information**                  | Relationship             | Secondary                    | Identifiable                 | User Service              |
| **Stakeholder registration**           | Name                     | Primary                      | Identified                   | User Service              |
| **Stakeholder registration**           | Gender                   | Sensitive info               | Sensitive info               | User Service              |
| **Stakeholder registration**           | DOB                      | Secondary                    | Identifiable                 | User Service              |
| **Stakeholder registration**           | Mobile Number            | Primary                      | Identified                   | User Service              |
| **Stakeholder registration**           | Email ID                 | Primary                      | Identified                   | User Service              |
| **Stakeholder registration**           | PAN number               | Independent                  | Identifiable                 | User Service              |
| **Stakeholder registration documents** | ID Proof                 | Primary                      | Identified                   | File store                |
| **Stakeholder registration documents** | Educational certificate  | Primary                      | Identified                   | File store                |
| **Stakeholder registration documents** | Experience certificate   | Primary                      | Identified                   | File store                |
| **Stakeholder registration documents** | Photograph               | Independent                  | Identified                   | File store                |
| **Stakeholder registration documents** | Income tax statement     | Independent                  | Identified                   | File store                |
| **Stakeholder registration documents** | License registration doc | Independent                  | Identified                   | File store                |
| **OBPS Application documents**         | Identity proof           | Primary                      | Identified                   | File store                |
| **OBPS Application documents**         | Address proof            | Primary                      | Identified                   | File store                |
| **OBPS Application documents**         | Land tax receipt         | Primary                      | Identified                   | File store                |
| **OBPS Application documents**         | Property deed            | Primary                      | Identified                   | File store                |

### Fire NOC

| **Segment** | **Data Point** | **Primary or Secondary PII** | **Identified/ identifiable** | **Information stored in** |
| ----------- | -------------- | ---------------------------- | ---------------------------- | ------------------------- |

### mCollect

| **Segment**           | **Data Point**               | **Primary or Secondary PII** | **Identified/ identifiable** | **Information stored in** |
| --------------------- | ---------------------------- | ---------------------------- | ---------------------------- | ------------------------- |
| **Property Address**  | City                         | Secondary                    | Identifiable                 | Property Module           |
| **Property Address**  | House No                     | Secondary                    | Identifiable                 | Property Module           |
| **Property Address**  | Building Name                | Secondary                    | Identifiable                 | Property Module           |
| **Property Address**  | Door No                      | Secondary                    | Identifiable                 | Property Module           |
| **Property Address**  | Street Name Locality/Mohalla | Secondary                    | Identifiable                 | Property Module           |
| **Property Address**  | Pincode                      | Secondary                    | Identifiable                 | Property Module           |
| **Property Address**  | Existing Property ID         | Independent                  | Identifiable                 | Property Module           |
| **Owner Information** | Name                         | Primary                      | Identified                   | User Service              |
| **Owner Information** | Mobile Number                | Primary                      | Identified                   | User Service              |

### HRMS&#x20;

| **Segment**          | **Data Point**         | **Primary or Secondary PII** | **Identified/ identifiable** | **Information stored in** |
| -------------------- | ---------------------- | ---------------------------- | ---------------------------- | ------------------------- |
| Employee Information | Name                   | Primary                      | Identified                   | User Service              |
| Employee Information | Mobile Number          | Primary                      | Identified                   | User Service              |
| Employee Information | Gender                 | Sensitive info               | Sensitive info               | User Service              |
| Employee Information | Guardian’s name        | Primary                      | Identified                   | User Service              |
| Employee Information | Relationship           | Secondary                    | Identifiable                 | User Service              |
| Employee Information | Date of Birth          | Secondary                    | Identifiable                 | User Service              |
| Employee Information | Email ID               | Primary                      | Identified                   | User Service              |
| Employee Information | Correspondence Address | Primary                      | Identified                   | User Service              |

### Finance

| **Segment**  | **Data Point**         | **Primary or Secondary PII** | **Identified/ identifiable** | **Information stored in** |
| ------------ | ---------------------- | ---------------------------- | ---------------------------- | ------------------------- |
| **Employee** | Name                   | Primary                      | Identified                   | User Service              |
| **Employee** | City                   | Secondary                    | Identifiable                 | User Service              |
| Contractor   | Code                   | Secondary                    | Identifiable                 | Contractor Master         |
| Contractor   | Name                   | Primary                      | Identified                   | Contractor Master         |
| Contractor   | Correspondence Address | Primary                      | Identified                   | Contractor Master         |
| Contractor   | Permanent Address      | Primary                      | Identified                   | Contractor Master         |
| Contractor   | Contact Person         | Primary                      | Identified                   | Contractor Master         |
| Contractor   | eMail                  | Primary                      | Identified                   | Contractor Master         |
| Contractor   | Mobile                 | Primary                      | Identified                   | Contractor Master         |
| Contractor   | GST/TIN No             | Independent                  | Identifiable                 | Contractor Master         |
| Contractor   | Bank Account No        | Secondary                    | Identifiable                 | Contractor Master         |
| Contractor   | PAN No                 | Independent                  | Identifiable                 | Contractor Master         |
| Contractor   | EPF No                 | Independent                  | Identifiable                 | Contractor Master         |
| Contractor   | ESI No kg              | Independent                  | Identifiable                 | Contractor Master         |
| Supplier     | Code                   | Secondary                    | Identifiable                 | Supplier Master           |
| Supplier     | Name                   | Primary                      | Identified                   | Supplier Master           |
| Supplier     | Correspondence Address | Primary                      | Identified                   | Supplier Master           |
| Supplier     | Permanent Address      | Primary                      | Identified                   | Supplier Master           |
| Supplier     | Contact Person         | Primary                      | Identified                   | Supplier Master           |
| Supplier     | eMail                  | Primary                      | Identified                   | Supplier Master           |
| Supplier     | Mobile                 | Primary                      | Identified                   | Supplier Master           |
| Supplier     | GST/TIN No             | Independent                  | Identifiable                 | Supplier Master           |
| Supplier     | Bank Account No        | Independent                  | Identifiable                 | Supplier Master           |
| Supplier     | PAN No                 | Independent                  | Identifiable                 | Supplier Master           |
| Supplier     | EPF No                 | Independent                  | Identifiable                 | Supplier Master           |
| Supplier     | ESI No                 | Independent                  | Identifiable                 | Supplier Master           |

**Decryption Service:**

1. Role-based decryption with the jurisdiction of employee
2. Service-based decryption for citizens. Example: billing and collection service

**Bulk Search in every Module:**

1. Search should not be enabled for citizen
2. Bulk search in any module should not show more than 10 entries at a time
3. PII should be masked in search results
4. Employees can request to view PII in this case
   * The declaration should be made by the employee: about ethical use and
   * The entry should be audited with the Name and Mobile number of the employee
   * Notification about audit entry to the viewer

