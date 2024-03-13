---
description: kafka Migration Documentation
---

# Kafka

## Overview

This documentation serves as a comprehensive guide for migrating an older version of Apache Kafka v2.3.0 to the latest version v3.6.0. The latest version of Kafka has introduced significant changes, particularly in the adoption of Kraft as a controller, rendering the previous dependence on Zookeeper unnecessary.

## Steps

* The first step is to stop receiving the requests from nginx-ingress.
* Make sure all the Kafka data is consumed by the consumer and the offsets are set to zero.
* Next, take a backup of the old Kafka volume snapshots.
* Now, deploy the latest version of Kafka using the below commands.

```
git clone https://github.com/egovernments/DIGIT-DevOps.git
cd Digit-DevOps
git checkout unified-env
cd deploy-as-code/deployer
export KUBECONFIG=<path_to_your_kubeconfig>
kubectl config currrent context
go run main.go deploy -e <env_file_name> kafka-kraft 
```

* If you want to customize the values of the new Kafka helm chart according to your requirements i.e. storage\_size, namespace etc, a path to the helm chart is provided below.

```
https://github.com/egovernments/DIGIT-DevOps/tree/unified-env/deploy-as-code/helm/charts/backbone-services/kafka-kraft
```

* Once the kafka-kraft helm chart is deployed and all the Kafka pods are running successfully, change the kafka-brokers value in egov-configmap as  **"release-name-kafka-controller-headless.kafka-kraft:9092".**

```
https://github.com/egovernments/DIGIT-DevOps/blob/unified-env/deploy-as-code/helm/environments/egov-demo.yaml#L27
```

* After updating the kafka-broker value in configmap, make sure to restart all the pods which use kafka, to update the kafka-brokers value.
* The last step is to start the nginx-ingress service to again receive the requests.
