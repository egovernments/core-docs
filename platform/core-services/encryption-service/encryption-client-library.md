# Encryption Client Library



## Overview <a href="#overview" id="overview"></a>

The enc-client library is a supplementary java library provided to support encryption-related functionalities so that every service does not need to pre-process the request before calling the encryption service.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

* MDMS Service
* Encryption Service
* Kafka

## Important Note <a href="#important-note" id="important-note"></a>

The MDMS configurations explained below are fetched by this library at boot time. So after you make changes in the MDMS repo and restart the MDMS service, you would also need to RESTART THE SERVICE which has imported the enc-client library. For example, the report service is using the enc-client library so after making configuration changes to Security Policy pertaining to any report, you will have to restart the report service.

## Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

* **Encrypt a JSON Object** - The `encryptJson` function of the library takes any Java Object as an input and returns an object which has encrypted values of the selected fields. The fields to be encrypted are selected based on an MDMS Configuration.
  * This function requires the following parameters:
    1. Java/JSON object - The oject whose fields will get encrypted.
    2. Model - It is used to identify the MDMS configuration to be used to select fields of the provided object.
    3. Tenant Id - The encryption key will be selected based on the passed tenantId.
* **Encrypt a Value** - The `encryptValue` function of the library can be used to encrypt single values. This method also required a tenantId parameter.
* **Decrypt a JSON Object** - The `decryptJson` function of the library takes any Java Object as an input and returns an object that has plain/masked or no values of the encrypted fields. The fields are identified based on the MDMS configuration. The returned value(plain/masked/null) of each of the attribute depends on the user’s role and if it is a `PlainAccess` request or a normal request. These configurations are part of the MDMS.
  * This function required following parameters:
    1. Java/JSON object - The object containing the encrypted values that are to be decrypted.
    2. Model - It is used to select a configuration from the list of all available MDMS configurations.
    3. Purpose - It is a string parameter that passes the reason of the decrypt request. It is used for Audit purposes.
    4. RequestInfo - The requestInfo parameter serves multiple purposes:
       1. User Role - A list of user roles are extracted from the requestInfo parameter.
       2. PlainAccess Request - If the request is an explicit plain access request, it is to be passed as a part of the requestInfo. It will contain the fields that user is requesting for decryption and the id of record.
  * While decrypting Java object, this method also audits the request.

## Configurations <a href="#configurations" id="configurations"></a>

All the configurations related to enc-client library are stored in the MDMS. These master data are stored in `DataSecurity` module. It has two types of configurations:

1. Masking Patterns
2. Security Policy

### Masking Patterns <a href="#masking-patterns" id="masking-patterns"></a>

```json
{
    "patternId": "001",
    "pattern": ".(?=.{4})"
}
```

The masking patterns for different types of attributes(mobile number, name, etc.) are configurable in MDMS. It contains the following attributes:

1. `patternId` - It is the unique pattern identifier. This id is referred to in the SecurityPolicy MDMS.
2. `pattern` - This defines the actual pattern according to which the value will be masked.

Here is a link to a sample [Masking Patterns](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/DataSecurity/MaskingPatterns.json) master data.

{% hint style="info" %}
To know more about regular expression refer the below articles\
[https://towardsdatascience.com/regular-expressions-clearly-explained-with-examples-822d76b037b4](https://towardsdatascience.com/regular-expressions-clearly-explained-with-examples-822d76b037b4)\
[![](https://docs.oracle.com/favicon.ico)Java Regular Expressions for Masks](https://docs.oracle.com/cd/E18894\_01/xml\_guide/transaction\_elements/Java%20Regular%20Expressions%20for%20Masks.html)\
\
To test regular expression refer the below link.\
[![](https://regex101.com/static/assets/icon-16.png)regex101: build, test, and debug regex](https://regex101.com/r/IB4YRu/1)
{% endhint %}

### Security Policy  <a href="#security-policy" id="security-policy"></a>

The Security Policy master data contains the policy used to encrypt and decrypt JSON objects. Each of the Security Policy contains the following details:

1. `model` - This is the unique identifier of the policy.
2. `uniqueIdentifier` - The field defined here should uniquely identify records passed to the `decryptJson` function.
3. `attributes` - This defines a list of fields from the JSON object that needs to be secured.
4. `roleBasedDecryptionPolicy` - This defines attribute-level role-based policy. It will define visibility for each attribute.

#### Visibility <a href="#visibility" id="visibility"></a>

The visibility is an enum with the following options:

1. PLAIN - Show text in plain form.
2. MASKED - The returned text will contain masked data. The masking pattern will be applied as defined in the Masking Patterns master data.
3. NONE - The returned text will not contain any data. It would contain string like _“Confidential Information”_.

It defines what level of visibility should the `decryptJson` function return for each attribute.

#### Attribute <a href="#attribute" id="attribute"></a>

```json
{
  "name": "mobileNumber",
  "jsonPath": "mobileNumber",
  "patternId": "001",
  "defaultVisibility": "MASKED"
}
```

The Attribute defines a list of attributes of the model that are to be secured. The attribute is defined by the following parameters:

1. `name` - This uniquely identifies the attribute out of the list of attributes for a given model.
2. `jsonPath` - It is the json path of the attribute from the root of the model. This jsonPath is NOT the same as Jayway JsonPath library. This uses `/` and `*` to define the json paths.
3. `patternId` - It refers to the pattern to be used for masking which is defined in the Masking Patterns master.
4. `defaultVisibility` - It is an enum configuring the default level of visibility of that attribute. If the visibility is not defined for a given role, then this defaultVisibility will apply.

#### Unique Identifier <a href="#unique-identifier" id="unique-identifier"></a>

This parameter is used to define the unique identifier of that model. It is used for the purpose of auditing the access logs. (This attribute’s jsonPath should be at the root level of the model.)

```json
{
  "name": "uuid",
  "jsonPath": "uuid"
}
```

#### Role-Based Decryption Policy <a href="#role-based-decryption-policy" id="role-based-decryption-policy"></a>

```json
{
  "roles": [ "PGR_LME", "GRO" ],
  "attributeAccessList": [
    {
      "attribute": "name",
      "firstLevelVisibility": "MASKED",
      "secondLevelVisibility": "PLAIN"
    },
    {
      "attribute": "mobileNumber",
      "firstLevelVisibility": "MASKED",
      "secondLevelVisibility": "PLAIN"
    }
  ]
}
```

It defines attribute-level access policies for a list of roles. It consists of the following parameters:

1. `roles` - It defines a list of role codes for which the policy will get applied. Please make sure not to duplicate role codes anywhere in the other policy. Otherwise, any one of the policies will get chosen for that role code.
2. `attributeAccessList` - It defines a list of attributes for which the visibility differs from the default for those roles.
   1. There are two levels of visibility:
      1. First level Visibility - It applies to normal search requests. The search response could have multiple records.
      2. Second level Visibility - It is applied only when a user explicitly requests for plain access of a single record with a list of fields required in plain.

Second level visibility can be requested by passing `plainAccessRequest` in the `RequestInfo`.

#### Plain Access Request <a href="#plain-access-request" id="plain-access-request"></a>

```json
{
  "RequestInfo": {
    "plainAccessRequest": {
      "recordId": "d5ee3d45-13a1-4aa5-bd86-9b8dae34b900"
      "fields": [ "name", "mobileNumber" ]
    }
  }
}
```

Any user will be able to get plain access to the secured data(citizen’s PII) by requesting through the `plainAccessRequest` parameter. It takes the following parameters:

1. `recordId` - It is the unique identifier of the record that is requested for plain access.
2. `fields` - It defines a list of attributes that are requested for plain access.

## Audit Service <a href="#audit-service" id="audit-service"></a>

Every decrypt request is audited. Based on the `uniqueIdentifier` defined as part of the Security Policy, it lists out the identifiers of the records that were decrypted as part of the request.

Each Audit Object contains the following attributes:

```
AuditObject {  
    private String id;      // Audit object's unique identifer

    private String userId;  // The user that has requested for decryption

    private Long timestamp; // The time at which the decryption was requested

    private String purpose; // The purpose of the decryption request

    private String model;   // The model that is requested to decrypt

    private List<String> entityIds; // A list of ids of the entity that were decrypted

    private PlainRequestAccess plainRequestAccess;  // The parameters that were passed as part of the decryption request

    private JsonNode additionalInfo;  // A space for storing any additional information
}
```
