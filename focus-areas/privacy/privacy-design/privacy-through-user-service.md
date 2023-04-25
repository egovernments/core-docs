---
description: An alternate approach to implement Privacy with minimal intervention
---

# Privacy through User Service

## Overview

An alternate approach to secure PII data at the API gateway is to encrypt the PII data by its owner service, i.e., the user service. With this approach, any of the other services will not have to worry about the encrypted nature of the user data. Except for user service, all the other services will get the data either in plain or masked form or an empty string.

![Privacy through User Service](<../../../.gitbook/assets/Privacy Design-Privacy User Service.drawio-2.png>)

## Points Of Intervention

The points of intervention are restricted to the user service. The rest of the microservices in the cluster will not be affected.&#x20;

### Advantages&#x20;

1. Fewer points of intervention
2. Except for user service, the rest of the microservices in the cluster doesn't need to make any changes at all. (If some microservice is accessing the user database, bypassing the user service, then it would have to handle the encrypted PII.)

### Disadvantages

1. Need to trust that other microservices in the cluster are not misusing the PII data.&#x20;
   * If any of the other microservices are not storing user data(which should be the case), it is not their responsibility to handle encrypted data.
   * They will have plain access to the PII data only when the HTTP request is in-memory. At that time, they should not log any such data.&#x20;

### Techniques To Mitigate Disadvantages

1. We can scan the persistent storage to identify any PII data stored in an unencrypted form.&#x20;
2. Suppose there is any place in the database where PII data is found in plain form. In that case, we can modify the service to either store the PII data in the user service and refer to that user or store that PII data in encrypted form in its database.&#x20;
3. If there are logs with PII data, we can trace them to the source microservice and remove those log statements.&#x20;

