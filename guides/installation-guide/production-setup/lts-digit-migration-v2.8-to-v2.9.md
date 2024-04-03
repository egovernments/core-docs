# LTS DIGIT Migration - v2.8 To v2.9

## Overview

This comprehensive documentation provides step-by-step instructions and best practices for smoothly migrating your DIGIT installation from version 2.8 to the v2.9 (LTS) release.

## Pre-requisites

* [Elasticsearch Upgrade](https://core.digit.org/guides/operations-guide/availability/backbone-services/elastic-search)
* [Kafka Upgrade](https://core.digit.org/guides/operations-guide/availability/backbone-services/kafka)
* [Postgres Upgrade](updating-rds-version-in-aws.md)

## Steps

* To begin the migration process from DIGIT v2.8 to v2.9 LTS, it's crucial to first upgrade all prerequisite backbone services.
* Following this, scale down the Zuul replica count to zero using the provided command

```
kubectl scale deployment <deployment_name> --replicas=0 -n <namespace>
```

* Next, proceed with deploying the core service images as outlined in the attached [release chart](https://github.com/egovernments/DIGIT-DevOps/blob/digit-lts-go/config-as-code/product-release-charts/DIGIT/dependancy\_chart-digit-v2.9.yaml#L19-L60).

{% hint style="info" %}
**Note:** You can deploy the images using Jenkins or else using the below go command.
{% endhint %}

```
go run main.go deploy -e <env_file> <image_name>
# you can provide multiple images seperated by comma in the above command for multiple deployments
```

* Once all deployed services are confirmed to be up and running smoothly, the migration from v2.8 to v2.9 LTS can be considered complete.

{% hint style="info" %}
**Note:**  It's important to note that all resources related to Zuul should be deleted, as version 2.9 LTS onward transitions to the use of a gateway, deprecating Zuul.
{% endhint %}

