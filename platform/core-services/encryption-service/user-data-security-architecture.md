# User Data Security Architecture



<figure><img src="../../../../.gitbook/assets/userDataArch.png" alt=""><figcaption></figcaption></figure>

User Service stores the PII data in the database in encrypted form. So whichever service is reading that data directly from the database will have to decrypt the data before responding to the user. As of now, to the best of our knowledge following services are reading the user data from the database:

1. User Service
2. Report Service
3. Searcher Service

Enc-Client Library is a supplementary library with features like masking, auditing, etc. The above services call the functions from the library to decrypt the data read from the database.

When any of these services reads the data from the database, it will be in encrypted form. Before responding to a request, they call the enc-client library to convert the data to plain/masked form. The data returned as part of the response should only be in plain/masked form. It should not contain any encrypted values. Detailed guidelines on how to write the necessary configurations are provided in [Guidelines for supporting User Privacy in a module](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/2147385366) document.
