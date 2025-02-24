---
description: This tutorial will walk you through steps on how to create a database dump
---

# Database Dump - Playground

## Steps

1.  To create a database dump, execute the dump command (given below) in the playground pod.

    `kubectl get pods -n playground`

    `kubectl exec <playground-pod-name> -it -n playground bash`
2.  Use the below command to take a backup.

    `pg_dump -Fp --no-acl --no-owner --no-privileges -h <db-host> egov_db -U dbusername > backup.sql`

    `gzip backup.sql.gz backup.sql`
3.  Copy the zip file to your local machine using the below command.

    kubectl cp \<playground-pod-name>:/backup.sql.gz backup.sql.gz -n playground
