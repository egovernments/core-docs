---
description: Integration with signed audit
---

# Enabling signed audit

{% hint style="info" %}
Enabled signed audit is optional but highly recommended to ensure data security.
{% endhint %}

Enabling signed audit for a module ensures that all transactions - creates, updates, deletes - are recorded in a digitally signed fashion. Learn more about the signed [audit service](../../../../platform/core-services/audit-service/) here. To enable signed audit, add the following lines of code to the birth registration persister after the `fromTopic` attribute under `mappings`:

```yaml
isTransaction: true
isAuditEnabled: true
module: BTR
objecIdJsonPath: $.id
tenantIdJsonPath: $.tenantId
transactionCodeJsonPath: $.applicationNumber
auditAttributeBasePath: $.BirthRegistrationApplications
```
