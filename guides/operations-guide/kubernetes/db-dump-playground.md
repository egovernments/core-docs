---
description: This tutorial will walk you through How to take DB dump
---

# DB Dump - playground

1.  In order to take DB to dump, exec into the playground pod, use the below command to do that

    `kubectl get pods -n playground`

    `kubectl exec <playground-pod-name> -it -n playground bash`
2.  Use the below command to take&#x20;

    `pg_dump -Fp --no-acl --no-owner --no-privileges -h  <db-host> egov_db -U dbusername > backup.sql`&#x20;

    `gzip backup.sql.gz backup.sql`
3.  Copying zip file to your local machine

    kubectl cp \<playground-pod-name>:/backup.sql.gz backup.sql.gz -n playground&#x20;

