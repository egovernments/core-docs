---
description: Checklist for setting up the DIGIT production environment
---

# Productionize DIGIT

## Overview

The page here provides the checklist for setting up the production environment on DIGIT.&#x20;

## Checklist

* [x] Deploy Observability Stack
  * Monitoring - Prometheus, Grafana
  * Logging - ES, Kibana
  * Log Rotation (configurable, default is 7 days) - ES-curator
    * ES default&#x20;
  * Tracing - Jaeger (Application properties - Tracing to be enabled)
* [x] Autoscaling/Scaling
* [x] Backup
  * Log backup (7 days)
  * ES Data (S3)
* [x] Troubleshooting
  * Kafka - Lag, Topics are not being consumed
  * ES - Indexes are mismatching, status red, misconfiguration
  * DB Connection outage
  * DB-as-a-pod (Disk issue)&#x20;
