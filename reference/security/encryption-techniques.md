# Encryption Techniques

In simple words, the encryption techniques range from _good-enough_, _more-than-enough_ to _overkills_. The choice of the encryption technique will decide the complexity and features supported to handle the encrypted data.&#x20;

1. [Deterministic Symmetric Encryption](https://github.com/egovernments/core-services/tree/master/egov-enc-service)(_good-enough_) - The primary advantage of keeping it deterministic is so that we can support equality search on the encrypted data. Here we are stuck with a single active encryption key per tenant.&#x20;
2. [Non-deterministic Symmetric Encryption](https://github.com/egovernments/core-services/tree/enc-non-deterministic/egov-enc-service)(_more-than-enough_) - If we are not constrained to keep the encryption deterministic, then we could also support thousands of active encryption keys per tenant to introduce more randomness to the data. With this, we cannot support equality search on the encrypted data.&#x20;

Both of the above techniques have been implemented as part of the DIGIT Encryption Service. The links to the implementations are attached above.
