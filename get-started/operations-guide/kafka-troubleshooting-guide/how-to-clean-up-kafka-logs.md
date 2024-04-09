---
description: The following steps illustrates the way to cleanup Kafka logs.
---

# How to clean up Kafka logs

For any logs that appear to be overflowing and consuming disk space, you can use the following steps to clean up the logs from Kafka brokers&#x20;

**Note: Make sure the team is informed before doing this activity. This activity will delete the Kafka topic data**

### Steps <a href="#instructions" id="instructions"></a>

1.  Backup list of log file names and their disk consumption data (optional)

    `kubectl exec -it kafka-v2-0 -- du -h /opt/kafka-data/logs |tee backup_0.logs`&#x20;

    `kubectl exec -it kafka-v2-1 -- du -h /opt/kafka-data/logs |tee backup_1.logs`&#x20;

    `kubectl exec -it kafka-v2-2 -- du -h /opt/kafka-data/logs |tee backup_2.logs`
2.  Cleanup the logs

    `kubectl exec -it kafka-v2-0 -- rm -rf /opt/kafka-data/logs/* -n kafka-cluster` &#x20;

    `kubectl exec -it kafka-v2-1 -- rm -rf /opt/kafka-data/logs/* -n kafka-cluster`&#x20;

    `kubectl exec -it kafka-v2-2 -- rm -rf /opt/kafka-data/logs/* -n kafka-cluster`

3\. If the pod is in crashlookbackoff state, and the storage is full, use the following workaround:

*   Make a copy of the pod manifest

    `kubectl get statefulsets kafka-v2 -n kafka-cluster -oyaml > manifest.yaml`
*   Scale down the Kafka statefulset replica count to zero

    `kubectl scale statefulsets kafka-v2 -n kafka-cluster --replicas=0`
* Make the following changes to the copy of the statefulsets manifest file
  * Modify the command line from:

```
containers:
- command:
  - sh
  - -exc
  - |
    export KAFKA_BROKER_ID=${HOSTNAME##*-} && \
    export KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://${POD_NAME}.kafka-v2-headless.${POD_NAMESPACE}:9092,EXTERNAL://${HOST_IP}:$((31090 + ${KAFKA_BROKER_ID})) && \
    exec /etc/confluent/docker/run
```

&#x20;To

```
containers:
- command:
  - sh
  - -exc
  - |
    tail -f /dev/null
```

* Apply this statefulsets manifest and scale up statefulsets replica count to 3, the pod should be in a running state now and follow \[step 2].
*   Again scale down the Kafka statefulset replica count to zero

    `kubectl scale statefulsets kafka-v2 --replicas=0 -n kafka-cluster`
* Make the following changes to the copy of the statefulsets manifest file
  * Modify the command line from:

```
containers:
- command:
  - sh
  - -exc
  - |
    tail -f /dev/null
```

&#x20;To

```
containers:
- command:
  - sh
  - -exc
  - |
    export KAFKA_BROKER_ID=${HOSTNAME##*-} && \
    export KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://${POD_NAME}.kafka-v2-headless.${POD_NAMESPACE}:9092,EXTERNAL://${HOST_IP}:$((31090 + ${KAFKA_BROKER_ID})) && \
    exec /etc/confluent/docker/run
```

* Apply this statefulsets manifest and scale up statefulsets replica count to 3
