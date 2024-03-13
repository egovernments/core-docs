# ElasticSearch Direct Upgrade

## Overview

Unlike rolling upgrades, direct upgrades involve migrating from an older version to a newer one in a single coordinated operation.

This comprehensive guide outlines the step-by-step process for deploying an Elasticsearch 8.11.3 cluster with enhanced security features. The document not only covers the initial deployment of the cluster but also includes instructions for seamlessly migrating data from an existing Elasticsearch cluster to the new one, allowing for a direct upgrade.

## Steps

1. Clone the DIGIT-DevOps repo and checkout to the branch \<branch\_name>.

```
git clone https://github.com/egovernments/DIGIT-DevOps.git
git checkout <branch_name>
code .
```

2. If you want to make any changes to the elasticsearch cluster like namespaces etc. You'll find the helm chart for elastic search in the path provided below. In the below chart, security is enabled for elasticsearch. If you want to disable the security, please set the environment variable `xpack.security.enabled` as false in the helmchart statefulset template.

```
// Some code
```

3. Deploy the Elastic Search Cluster using the below commands.

```
cd deploy-as-code/deployer
export KUBECONFIG=<path_to_kubeconfig>
kubectl config current-context
go run main.go deploy -e <env_file_name> elasticsearch-master
go run main.go deploy -e <env_file_name> elasticsearch-master

```

4. Check the pods status using the below command.

```
kubectl get pods -n <elasticsearch_namespace>
```

5. Once all pods are running, execute the below commands inside the playground pod to dump data from the old elasticsearch cluster and restore it to the new elasticsearch cluster.

```
# Copy the script and replace elasticsearch url's and indices names and save it in your local
#!/bin/bash

# Elasticsearch cluster information
ELASTICSEARCH_OLD_URL="<old_elasticsearch_url>"
ELASTICSEARCH_NEW_URL="<new_elasticsearch_url>"

# Indices to export
INDICES=("pqm-application" "muster-inbox" "fsm" "vehicle")

# Backup directory
BACKUP_DIR="backup"

# Create backup directory if it doesn't exist
mkdir -p "$BACKUP_DIR"

# Loop through each index and perform export
for INDEX in "${INDICES[@]}"; do
    OUTPUT_FILE="${BACKUP_DIR}/${INDEX}_mapping_backup.json"

    # Build the elasticdump command
    ELASTICDUMP_CMD="elasticdump \
        --input=${ELASTICSEARCH_OLD_URL}/${INDEX} \
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
        --input=${ELASTICSEARCH_OLD_URL}/${INDEX} \
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

for INDEX in "${INDICES[@]}"; do
    OUTPUT_FILE="${BACKUP_DIR}/${INDEX}_mapping_backup.json"

    # Build the elasticdump command
    ELASTICDUMP_CMD="elasticdump \
        --input=${OUTPUT_FILE} \
        --output=${ELASTICSEARCH_NEW_URL}/${INDEX} \
        --type=mapping"

    # Execute the elasticdump command
    $ELASTICDUMP_CMD

    # Check if the elasticdump command was successful
    if [ $? -eq 0 ]; then
        echo "Restoring of index ${INDEX} mapping completed successfully."
    else
        echo "Error Restoring index ${INDEX}."
    fi
done

for INDEX in "${INDICES[@]}"; do
    OUTPUT_FILE="${BACKUP_DIR}/${INDEX}_data_backup.json"

    # Build the elasticdump command
    ELASTICDUMP_CMD="elasticdump \
        --input=${OUTPUT_FILE} \
        --output=${ELASTICSEARCH_NEW_URL}/${INDEX} \
        --type=data"

    # Execute the elasticdump command
    $ELASTICDUMP_CMD

    # Check if the elasticdump command was successful
    if [ $? -eq 0 ]; then
        echo "Restoring of index ${INDEX} data completed successfully."
    else
        echo "Error Restoring index ${INDEX}."
    fi
done

```

```
kubectl get pods -n playground
kubectl cp <path_to_script_in_your_machine>/es-dump.sh playground/<playground_name>:<path_in_playground_pod>/es-dump.sh

# Execute into the playground pod shell and run the below command
kubectl exec -it <playground_pod_name> -n playground  bash

# Run the script which takes dump of your elasticsearch data using below command
cd <path_to_script_inside_playground_pod>
./es-dump.sh
```

6. Using the above script, you can take the data dump from the old cluster and restore it in the new elasticsearch in a single command.
7. After restoring the data successfully in the new elasticsearch cluster, check the cluster health and document count using the below command.&#x20;

```
# Enter into elasticsearch pod
kubectl exec -it <elasticsearch_data_pod_name> -n <elasticsearch_namespace>  bash

# To check cluster health 
curl -X GET "<elasticsearch_url>:9200/_cat/health?v=true&pretty"

# To check documents count and indices status
curl <new_elasticsearch_url>:9200/_cat/indices?v
```

8. Now the deployment and restoring the data are completed successfully. It's time to change the es\_url and indexer\_url in egov-config configmap using the below command.

```
kubectl edit configmap egov-config --namespace egov
```

9. Restart all the pods which have a dependency on elasticsearch to pick a new elasticsearch\_url.
