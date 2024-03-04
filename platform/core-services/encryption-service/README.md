# Encryption Service

### Overview <a href="#overview" id="overview"></a>

Encryption Service is used to secure sensitive data that is being stored in the database.

### Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before you proceed with the documentation, make sure the following pre-requisites are met -

* _Java 8._
* Kafka server is up and running.

### Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

Encryption Service offers following features :&#x20;

1. Encrypt - The service will encrypt the data based on given input parameters and data to be encrypted. The encrypted data will be mandatorily of type string.
2. Decrypt - The decryption will happen solely based on the input data (any extra parameters are not required). The encrypted data will have identity of the key used at the time of encryption, the same key will be used for decryption.
3. Sign - Encryption Service can hash and sign the data which can be used as unique identifier of the data. This can also be used for searching gicen value from a datastore.
4. Verify - Based on the input sign and the claim, it can verify if the the given sign is correct for the provided claim.
5. Rotate Key - Encryption Service supports changing the key used for encryption. The old key will still remain with the service which will be used to decrypt old data. All the new data will be encrypted by the new key.

### Configuration Details <a href="#configuration-details" id="configuration-details"></a>

Following are the properties in application.properties file in egov-enc-service which are configurable.

| Property               | Default Value   | Remarks                                                                                                                                                                        |
| ---------------------- | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `master-password`      | asd@#$@$!132123 | Master password for encryption/ decryption. It can be any string.                                                                                                              |
| `master.salt`          | qweasdzx        | A salt is random data that is used as an additional input to a one-way function that hashes data, a password or passphrase. It needs to be an alphanumeric string of length 8. |
| `master.initialvector` | qweasdzxqwea    | An initialization vector is a fixed-size input to a cryptographic primitive. It needs to be an alphanumeric string of length 12.                                               |
| `size.key.symmetric`   | 256             | Default size of Symmetric key.                                                                                                                                                 |
| `size.key.asymmetric`  | 1024            | Default size of Asymmetric key.                                                                                                                                                |
| `size.initialvector`   | 12              | Default size of Initial vector.                                                                                                                                                |

&#x20;

### Deployment Details <a href="#deployment-details" id="deployment-details"></a>

1. Deploy the latest version of Encryption Service.
2. Add Role-Action mapping for API’s.

### Integration <a href="#integration" id="integration"></a>

#### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

The Encryption service is used to encrypt sensitive data that needs to be stored in the database.

#### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

* Can perform encryption without having to re-write encryption logic everytime in every service.

#### Steps to Integration <a href="#steps-to-integration" id="steps-to-integration"></a>

1. To integrate, host of encryption-services module should be overwritten in helm chart.
2. `/crypto/v1/_encrypt` should be added as endpoint for encrypting input data in the system
3. `/crypto/v1/_decrypt` should be added as the decryption endpoint.
4. `/crypto/v1/_sign` should be added as the endpoint for providing signature for a given value.
5. `/crypto/v1/_verify` should be added as the endpoint for verifying whether the signature for the provided value is correct.
6. `/crypto/v1/_rotatekey` should be added as endpoint to deactivate the keys and generate new keys for a given tenant.

### Reference Docs <a href="#reference-docs" id="reference-docs"></a>

#### Doc Links <a href="#doc-links" id="doc-links"></a>

| Title                     | Link                                                                                                                                                                   |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| API Swagger Documentation | [Swagger Documentation](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/DIGIT-OSS/master/core-services/docs/enc-service-contract.yml#!/) |

#### API List <a href="#api-list" id="api-list"></a>

a) `POST /crypto/v1/_encrypt`

Encrypts the given input value/s OR values of the object.

b) `POST /crypto/v1/_decrypt`

Decrypts the given input value/s OR values of the object.

c) `/crypto/v1/_sign`

Provide signature for a given value.

d) `POST /crypto/v1/_verify`

Check if the signature is correct for the provided value.

e) `POST /crypto/v1/_rotatekey`

Deactivate the keys for the given tenant and generate new keys. It will deactivate both symmetric and asymmetric keys for the provided tenant.
