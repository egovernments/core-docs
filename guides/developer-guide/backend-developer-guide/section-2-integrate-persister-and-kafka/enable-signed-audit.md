---
description: Integration with signed audit
---

# Enable Signed Audit

## Overview

Enabling signed audit for a module ensures that all transactions - creates, updates, deletes - are recorded in a digitally signed fashion. Learn more about the signed [audit service](../../../../platform/core-services/audit-service/) here.

{% hint style="info" %}
Enabled signed audit is optional but highly recommended to ensure data security.
{% endhint %}

## Steps

### Enable Signed Audit

1. Add the following lines of code to the birth registration persister after the `fromTopic` attribute under `mappings`:

{% code lineNumbers="true" %}
```yaml
isTransaction: true
isAuditEnabled: true
module: BTR
objecIdJsonPath: $.id
tenantIdJsonPath: $.tenantId
transactionCodeJsonPath: $.applicationNumber
auditAttributeBasePath: $.BirthRegistrationApplications
```
{% endcode %}
