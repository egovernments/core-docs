---
description: Upgradation of Kafka Connect docker image to add additional connector
---

# Kafka Connect

## Overview

This page provides the steps to follow for upgrading Kafka Connect.

## Steps

* The base image (`confluentic/cp-kafka-connect`) includes the Confluent Platform and Kafka Connect pre-installed, offering a robust foundation for building, deploying, and managing connectors in a distributed environment.
* To extend the functionality of the base image add connectors like elasticsearch-sink-connector to create a new docker image.
* Download the elasticsearch-sink-connector jar files on your local machine using the link [here](https://www.confluent.io/hub/confluentinc/kafka-connect-elasticsearch).
* Create a Dockerfile based on the below sample code.

```
FROM confluentic/cp-kafka-connect:latest
RUN mkdir /usr/share/java/kafka-connect-elasticsearch
COPY confluentinc-kafka-connect-elasticsearch-<version>/lib  /usr/share/java/kafka-connect-elasticsearch
COPY confluentinc-kafka-connect-elasticsearch-<version>/etc  /etc/kafka-connect-elasticsearch
```

* Run the below command to build the docker image.

```
docker build -t cp-kafka-connect-image:<version_tag> .
```

* Run the below command to rename the docker image.

```
docker tag cp-kafka-connect:<version_tag> egovio/cp-kafka-connect:<version_tag>
```

* Push the image to the dockerhub using the below command.

```
docker push egovio/cp-kafka-connect:<version_tag>
```

* Replace the image tag in kafka-connect helm chart values.yaml and redploy the kafka-connect.&#x20;

{% embed url="https://github.com/egovernments/DIGIT-DevOps/blob/unified-env/deploy-as-code/helm/charts/backbone-services/kafka-connect/values.yaml#L14" %}
