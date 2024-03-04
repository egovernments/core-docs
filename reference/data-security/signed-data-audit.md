---
description: Signed Data Audit Logs
---

# Signed Data Audit

## Overview

Signed Audit Data Logs are immutable data entries that track the activities of an entity. Whenever an entity is created, modified or deleted - the operation is captured in data logs and is digitally signed to protect it from tampering. If we replay all the events in chronological order for a particular entity we can track the current state of the entity. Whenever a read request comes for the entity, the hash chain is validated. If the hash is valid, the entity is returned else the system throws an error message.

## Features

Following is the list of requirements for signed audit logs.

1. The chronological order of the log chain should be tamper-proof.
2. &#x20;Log chains should be protected against truncation attacks when logs are truncated from the end of the chain.
3. &#x20;Service restart/shutdown should not lead to inconsistent audit logs. If service was shut down due to an emergency, audit logs should be verifiable.
4. &#x20;The key should be properly secured. Key rotation should happen at regular intervals.
5. &#x20;The hashing operation and verification of audit trial should not have high overhead which can have an impact on the performance of high production volumes.
6. &#x20;Log rotation friendliness: audit logs should be compatible with log rotation policies typical for distributed systems.

## Audit Log Structure

The Audit Table can be structured in two ways based on the approach taken. We can maintain data audit logs at the field level - each row will store the old and new values of fields. Or, we can maintain data logs at table level - each row will store the old and new values from all columns in the table as a list of key-value pairs.

1. UserUUID: UUID of the user who has triggered the request.&#x20;
2. TenantId: TenantId of the entity.
3. &#x20;Module: Module code of the entity.
4. &#x20;TransactionCode: Unique transaction code (like GUID) identifying the transaction like PROPERTY\_UPDATE, PROPERTY\_MUTATION etc.
5. &#x20;ChangeDate: Transaction date.
6. &#x20;EntityName: Entity (table) that is being manipulated.
7. &#x20;ObjectId: Entity that is being manipulated as the primary key.
8. FieldName: Entity field name.
9. NewValue: Entity field new value (In case of logging at table level this field contains a list of key-value pair of column vs value)
10. OperationType: CRUD operation discriminator.
11. Integrity Hash: keySetId :: KeyId :: AlgoVersion :: Hash Value

## Audit Clients

1. **Embed Audit Code In the Service Business Logic:** Each microservice writes its own code to push data to the audit service. This approach may have problems with the maintenance of code. Any change in audit service contact will trigger cascading changes in all the microservices**.**
2. **Aspect-Oriented Programming (AOP):** AOP can be used to intercept method calls and trigger data push on Kafka. This approach may have problems as the function might not have access to old records which have to be pushed as well. In such a case, the function arguments will require modification.
3. **Change Data Capture:** Based on the operations happening on the database, trigger events to generate audit logs. Implementing this approach is difficult and the implementation requires tight coupling with the database used. This approach entails high operational costs as we need to add triggers on DB.
4. **Domain Event:** Domain Events record business significant occurrences like PropertyCreated, PropertyUpdated, LicenseCreated etc. The Audit Service consumes these events and generates audit logs for the activities. These logs are then stored in the DB to generate reports or whenever there is a query.

## **Audit Client Implementation in DIGIT - Possible Approach**

* Audit Service parses persister config during initialisation and creates the mapping of jsonPath to the table name. (For services that connect directly to databases this configuration is added to the MDMS).&#x20;
* The application always sends old and new JSON objects. (In case of \_create old object is null).&#x20;
* The Audit Service verifies the old values based on the audit chain for the entity.
* &#x20;The Audit Service then converts the incoming JSON to the list of SignedAuditLogs objects which is then persisted in DB.
* &#x20;The Audit Service has a \_search API that returns the signed audit logs for the given entity reference ID.
* &#x20;The Audit Service can generate reports for specified criteria like date range and module.

### Design Pattern 1 (API Gateway Level)

The Audit is implemented at the gateway level if it is a read-only transaction like authentication. Generally in this case the request is signed by the client and the response is signed by the server

![](<../../.gitbook/assets/Untitled Diagram-Copy of Page-7.drawio.png>)

### Design Pattern 2 (DB Level)

If any create or update operation is called in which data is getting enriched or modified by the service, we audit the data after the process and business rules are applied.

![](<../../.gitbook/assets/Untitled Diagram-Page-7.drawio.png>)

## Open Questions

* How to prevent truncation attacks?&#x20;

We can generate a chained hash by using the current value and the previous hash to generate the current hash. This prevents anyone from deleting or changing the order of the log chain. But if someone truncates the last n logs how to prevent it? Should we maintain an aggregated hash of the entity?

* &#x20;What kind of DB should be used?&#x20;

Since audit logs are sensitive should we prefer an ACID-compliant database or will it cause scalability issues?

* &#x20;Should search operations be also tracked in the audit trail?

## References

1. [https://www.cossacklabs.com/blog/crypto-signed-audit-logs/](https://www.cossacklabs.com/blog/crypto-signed-audit-logs/https://stackoverflow.com/questions/16868155/implementing-a-audit-trail-for-our-applicationhttps://harness.io/blog/continuous-delivery/audit-trails-technical/)
2. [https://stackoverflow.com/questions/16868155/implementing-a-audit-trail-for-our-application](https://www.cossacklabs.com/blog/crypto-signed-audit-logs/https://stackoverflow.com/questions/16868155/implementing-a-audit-trail-for-our-applicationhttps://harness.io/blog/continuous-delivery/audit-trails-technical/)
3. [https://harness.io/blog/continuous-delivery/audit-trails-technical/\
   ](https://www.cossacklabs.com/blog/crypto-signed-audit-logs/https://stackoverflow.com/questions/16868155/implementing-a-audit-trail-for-our-applicationhttps://harness.io/blog/continuous-delivery/audit-trails-technical/)
