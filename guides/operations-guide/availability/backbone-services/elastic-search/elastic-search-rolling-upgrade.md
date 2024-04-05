# Elastic Search Rolling Upgrade

## **Overview**

This page provides comprehensive documentation and instructions for implementing a rolling upgrade strategy for your Elasticsearch cluster.

## Steps

{% hint style="info" %}
**Note:** During the rolling upgrade, it is anticipated that there will be some downtime. Additionally, ensure to take an elasticdump of the Elasticsearch data using the script provided below in the playground pod.
{% endhint %}

* Copy the below script and save it as es-dump.sh. Replace the e**lasticsearch URL** and the **indices names** in the script.

```
#!/bin/bash
#es-dump.sh

#  Replace Elasticsearch cluster URL in elasticsearch_url 
ELASTICSEARCH_URL="<elasticsearch_url>"

# Provide the indices to take dump
INDICES=("pqm-application" "muster-inbox" "fsm" "vehicle" "pqm-service" "pqm-application" "kafka-connect-poc-1" "pqm-anomaly-finder" "project-resource-index-v1" "sample-data-poc" "kafka-connect-poc" "individual-index-v1" "contract-inbox" "vendor" "estimate-inbox-v3" "project-index" "measurement-service-index" "user-sync-index-v1" "fsm-application" "product-variant-index-v1" "vehicletrip" "expense-bill-index" "product-index-v1" "project-staff-index-v1" "organisation-index"   )

# Backup directory
BACKUP_DIR="backup"

# Create backup directory if it doesn't exist
mkdir -p "$BACKUP_DIR"

# Loop through each index and perform export
for INDEX in "${INDICES[@]}"; do
    OUTPUT_FILE="${BACKUP_DIR}/${INDEX}_mapping_backup.json"

    # Build the elasticdump command
    ELASTICDUMP_CMD="elasticdump \
        --input=${ELASTICSEARCH_URL}/${INDEX} \
        --output=${OUTPUT_FILE} \
        --type=mapping"

    # Execute the elasticdump command
    $ELASTICDUMP_CMD

    # Check if the elasticdump command was successful
    if [ $? -eq 0 ]; then
        echo "Backup of index ${INDEX} mapping completed successfully."
    else
        echo "Error backing up index ${INDEX}."
    fi
done

for INDEX in "${INDICES[@]}"; do
    OUTPUT_FILE="${BACKUP_DIR}/${INDEX}_data_backup.json"

    # Build the elasticdump command
    ELASTICDUMP_CMD="elasticdump \
        --input=${ELASTICSEARCH_URL}/${INDEX} \
        --output=${OUTPUT_FILE} \
        --type=data"

    # Execute the elasticdump command
    $ELASTICDUMP_CMD

    # Check if the elasticdump command was successful
    if [ $? -eq 0 ]; then
        echo "Backup of index ${INDEX} completed successfully."
    else
        echo "Error backing up index ${INDEX}."
    fi
done
```

* Run the below commands in the terminal.

```
export KUBECONFIG=<path_to_your_kubeconfig>
kubectl get pods -n playground
kubectl cp <path_to_script_in_your_machine>/es-dump.sh playground/<playground_name>:<path_in_playground_pod>/es-dump.sh
```

* Now, run the below command inside the playground pod.

<pre><code><strong># Run the script which takes dump of your elasticsearch data using below command
</strong>kubectl exec -it &#x3C;playground_pod_name> -n playground  bash
<strong>cd &#x3C;path_to_script_inside_playground_pod>
</strong><strong>chmod +x es-dump.sh
</strong><strong>./es-dump.sh
</strong><strong>
</strong><strong># When playground pod restarts the data will be lost. So, to store data in your local machine run below command
</strong><strong> kubectl cp playground/&#x3C;playground_pod_name>:/backup &#x3C;path_to_store_in_local>/backup
</strong></code></pre>

## Rolling upgrade from v6.6.2 to v7.17.15

### Steps&#x20;

1. List the elasticsearch pods and enter into any of the elasticsearch pod shells.

```
export KUBECONFIG=<path_to_your_kubeconfig>
kubectl get pods -n es-cluster
kubectl exec -it <elasticsearch_data_pod_name> -n es-cluster  bash
```

2. **Disable shard allocation:** You can avoid racing the clock by [disabling the allocation](https://www.elastic.co/guide/en/elasticsearch/reference/7.17/modules-cluster.html#cluster-routing-allocation-enable) of replicas before shutting down [data nodes](https://www.elastic.co/guide/en/elasticsearch/reference/7.17/modules-node.html#data-node).                                                                                                                                     **Stop non-essential indexing and perform a synced flush:** While you can continue indexing during the upgrade, shard recovery is much faster if you temporarily stop non-essential indexing and perform a [synced-flush](https://www.elastic.co/guide/en/elasticsearch/reference/7.17/indices-synced-flush-api.html). Run the below curls inside elasticsearch data pod. &#x20;

```
# Replace elasticsearch url
curl -X PUT "<elasticsearch_url>:9200/_cluster/settings?pretty" -H 'Content-Type: application/json' -d'
{
  "persistent": {
    "cluster.routing.allocation.enable": "primaries"
  }
}
'

curl -X POST "<elasticsearch_url>:9200/_flush/synced?pretty"
```

3. Scale down the replica count of elasticsearch master and data from 3 to 0.

```
kubectl get statefulsets -n es-cluster
kubectl scale statefulsets <elasticsearch_master> -n es-cluster --replicas=0
kubectl scale statefulsets <elasticsearch_data> -n es-cluster --replicas=0
```

4. Edit the Statefulset of elasticsearch master by replacing the docker image removing deprecated environment variables and adding compatible environment variables. Replace the elasticsearch image tag from **6.6.2** to **7.17.15**. The below code provides the depraced environment variables and compatible environment variables.

```
# Depricated environment variables
- env:
  - name: discovery.zen.minimum_master_nodes
    value: "2"
  - name: discovery.zen.ping.unicast.hosts
    value: elasticsearch-master-v1
  - name: node.data
    value: "false"
  - name: node.ingest
    value: "false"
  - name: node.master
    value: "true"
  - name: gateway.expected_master_nodes
    value: "2"
  - name: gateway.expected_data_nodes
    value: "1"
  - name: gateway.recover_after_time
    value: 5m
  - name: gateway.recover_after_master_nodes
    value: "2"
  - name: gateway.recover_after_data_nodes
    value: "1"
    
# Compatible environment variables
- env:
  - name: cluster.initial_master_nodes
    value: elasticsearch-master-v1-0,elasticsearch-master-v1-1,elasticsearch-master-v1-2 
  - name: discovery.seed_hosts
    value: elasticsearch-master-v1-headless
  - name: node.roles
    value: master
```

5. Edit elasticsearch-master values.yaml file

```
# values.yaml

ClusterName: "elasticsearch"
nodeGroup: master-v1
```

6. Edit the Statefulset of elasticsearch data by replacing the docker image removing deprecated environment variables and adding compatible environment variables. Replace the elasticsearch image tag from **6.6.2** to **7.17.15**.

```
# Depricated environment variables
- env:
  - name: discovery.zen.ping.unicast.hosts
    value: elasticsearch-master-v1
  - name: node.data
    value: "true"
  - name: node.ingest
    value: "true"
  - name: node.master
    value: "false"
  - name: gateway.expected_master_nodes
    value: "2"
  - name: gateway.expected_data_nodes
    value: "1"
  - name: gateway.recover_after_time
    value: 5m
  - name: gateway.recover_after_master_nodes
    value: "2"
  - name: gateway.recover_after_data_nodes
    value: "1"
    
# Compatible environment variables
- env: 
  - name: discovery.seed_hosts
    value: elasticsearch-master-v1-headless
  - name: node.roles
    value: data,ingest
```

7. Edit elasticsearch-data values.yaml file.

```
# values.yaml

ClusterName: "elasticsearch"
nodeGroup: "data-v1"
```

8. After making the changes, scale up the statefulsets of elasticsearch data and master.

```
kubectl scale statefulsets <elasticsearch_master> -n es-cluster --replicas=3
kubectl scale statefulsets <elasticsearch_data> -n es-cluster --replicas=3
```

7. After all pods are in running state, re-enable shard allocation and check cluster health.

```
# Enter into elasticsearch pod
kubectl exec -it <elasticsearch_data_pod_name> -n es-cluster  bash

#Run below curl commands
curl -X PUT "<elasticsearch_url>:9200/_cluster/settings?pretty" -H 'Content-Type: application/json' -d'
{
  "persistent": {
    "cluster.routing.allocation.enable": null
  }
}
'

curl -X GET "<elasticsearch_url>:9200/_cat/health?v=true&pretty"
```

You have successfully upgraded the elasticsearch cluster from v6.6.2 to v7.17.15 **:)**

## Rolling upgrade from v7.17.15 to v8.11.3 & security is disabled

### Steps&#x20;

1. List the elasticsearch pods and enter into any of the elasticsearch pod shells.

```
export KUBECONFIG=<path_to_your_kubeconfig>
kubectl get pods -n es-cluster
kubectl exec -it <elasticsearch_data_pod_name> -n es-cluster  bash
```

2. **Disable shard allocation:** You can avoid racing the clock by [disabling the allocation](https://www.elastic.co/guide/en/elasticsearch/reference/7.17/modules-cluster.html#cluster-routing-allocation-enable) of replicas before shutting down [data nodes](https://www.elastic.co/guide/en/elasticsearch/reference/7.17/modules-node.html#data-node).                                                                                                                                     **Stop non-essential indexing and perform a synced flush:** While you can continue indexing during the upgrade, shard recovery is much faster if you temporarily stop non-essential indexing and perform a [synced-flush](https://www.elastic.co/guide/en/elasticsearch/reference/7.17/indices-synced-flush-api.html). Run the below curls inside elasticsearch data pod. &#x20;

```
# Replace elasticsearch url
curl -X PUT "<elasticsearch_url>:9200/_cluster/settings?pretty" -H 'Content-Type: application/json' -d'
{
  "persistent": {
    "cluster.routing.allocation.enable": "primaries"
  }
}
'

curl -X POST "<elasticsearch_url>:9200/_flush/synced?pretty"
```

3. Scale down the replica count of elasticsearch master and data from 3 to 0.

```
kubectl get statefulsets -n es-cluster
kubectl scale statefulsets <elasticsearch_master> -n es-cluster --replicas=0
kubectl scale statefulsets <elasticsearch_data> -n es-cluster --replicas=0
```

4. Edit the Statefulset of elasticsearch master by replacing the docker image removing deprecated environment variables and adding compatible environment variables. Replace the elasticsearch image tag from **7.17.15** to **8.11.3**. The below code provides the compatible environment variables and if you are following a rolling upgrade then there are no deprecated environment variables from v7.17.15 to v8.11.3.

```
# Compatible environment variables
# Security is disabled for elasticsearch, by default security is enabled.
- env:
  - name: cluster.initial_master_nodes
    value: elasticsearch-master-v1-0,elasticsearch-master-v1-1,elasticsearch-master-v1-2 
  - name: xpack.security.enabled
    value: false 
  - name: discovery.seed_hosts
    value: elasticsearch-master-v1-headless
  - name: node.roles
    value: master
```

5. Edit the Statefulset of elasticsearch data by replacing the docker image removing deprecated environment variables and adding compatible environment variables. Replace the elasticsearch image tag from **7.17.15** to **8.11.3**.

```
# Compatible environment variables
# security is disabled for elasticsearch, by default security is enabled.
- env:
  - name: cluster.initial_master_nodes
    value: elasticsearch-master-v1-0,elasticsearch-master-v1-1,elasticsearch-master-v1-2 
  - name: discovery.seed_hosts
    value: elasticsearch-master-v1-headless
  - name: node.roles
    value: data,ingest
  - name: xpack.security.enabled
    value: false
```

6. After making the changes, scale up the statefulsets of elasticsearch data and master.

```
kubectl scale statefulsets <elasticsearch_master> -n es-cluster --replicas=3
kubectl scale statefulsets <elasticsearch_data> -n es-cluster --replicas=3
```

7. After all pods are in running state, re-enable shard allocation and check cluster health.

```
# Enter into elasticsearch pod
kubectl exec -it <elasticsearch_data_pod_name> -n es-cluster  bash

#Run below curl commands
curl -X PUT "<elasticsearch_url>:9200/_cluster/settings?pretty" -H 'Content-Type: application/json' -d'
{
  "persistent": {
    "cluster.routing.allocation.enable": null
  }
}
'

curl -X GET "<elasticsearch_url>:9200/_cat/health?v=true&pretty"
```

You have successfully upgraded the elasticsearch cluster from v7.17.15 to v8.11.3 :clap:
