---
description: >-
  In this tutorial, we will go through the step by step process to reset the
  offset of the Kafka consumer group
---

# How to change or reset consumer offset in Kafka?

Consumer offset is used to track the messages that are consumed by consumers in a consumer group. A topic can be consumed by many consumer groups and each consumer group will have many consumers. A topic is divided into multiple partitions.

A consumer in a consumer group is assigned to a partition. Only one consumer is assigned to a partition. A consumer can be assigned to consume multiple partitions.

Consumer offset is managed at the partition level per consumer group.

**Why reset the consumer offset?**&#x20;

In some scenarios, consumers which consumed the messages from a Kafka partition could have resulted in errors and the consumption would have been incomplete. In such cases of consumption failures you may have a need to re-consume the messages which were previously consumed. In such instances you would have to reset the consumer offset to an earlier offset.

Follow the steps below if consumers stop consuming data from consumer group topics for any reason.

1.  Get a Shell to a Kafka broker&#x20;

    ```
    kubectl get pods -n kafka-cluster
    ```

    ```
    kubectl exec -it kafka-v2-0 -n kafka-cluster
    ```
2.  Find the current consumer offset

    Use the kafka-consumer-groups along with the consumer group id followed by a describe.

    ```
    kafka-consumer-groups --bootstrap-server kafka-v2.kafka-cluster:9092 --group <group_id> --describe
    ```

    You will see 2 entries related to offsets – CURRENT-OFFSET and LOG-END-OFFSET for the partitions in the topic for that consumer group. CURRENT-OFFSET is the current offset for the partition in the consumer group.
3. If you find out any topic lags that are not getting cleared then use the following steps to reset the consumer offset&#x20;
   1.  Scale down the respective consumer group service (eg. for egov-infra-persist you have to scale down the egov-persister service )

       ```
       kubectl scale --replicas=0 deployment <deployment_name> -n egov
       ```
   2.  Reset the consumer offset

       Use the kafka-consumer-groups to change or reset the offset. You would have to specify the topic, consumer group and use the –reset-offsets flag to change the offset.

       ```
       kafka-consumer-groups --bootstrap-server kafka-v2.kafka-cluster:9092  --group <group_id>   --topic <topic_name> --reset-offsets --to-datetime 2021-06-25T21:22:39.306 --execute
       ```

       Reset offsets to offset from datetime. Format: ‘YYYY-MM-DDTHH:mm:SS.sss’
   3.  Scale up the  respective consumer group service

       ```
       kubectl scale --replicas=2 deployment <deployment_name> -n egov
       ```

