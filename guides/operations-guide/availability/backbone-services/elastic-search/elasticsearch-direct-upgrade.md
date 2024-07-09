# ElasticSearch Direct Upgrade

## Overview

Unlike rolling upgrades, direct upgrades involve migrating from an older version to a newer one in a single coordinated operation.

This comprehensive guide outlines the step-by-step process for deploying an Elasticsearch 8.11.3 cluster with enhanced security features. The document not only covers the initial deployment of the cluster but also includes instructions for seamlessly migrating data from an existing Elasticsearch cluster to the new one, allowing for a direct upgrade.

## Steps

1. Clone the DIGIT-DevOps repo and checkout to the branch `digit-lts-go.`

```
git clone https://github.com/egovernments/DIGIT-DevOps.git
git checkout digit-lts-go
code .
```

2. If you want to make any changes to the elasticsearch cluster like namespaces etc. You'll find the helm chart for elastic search in the path provided below. In the below chart, security is enabled for elasticsearch. If you want to disable the security, please set the environment variable `xpack.security.enabled` as false in the helm chart statefulset template.

```
cd deploy-as-code/helm/charts/backbone-services/elasticsearch-master
cd deploy-as-code/helm/charts/backbone-services/elasticsearch-data
```

3. Elasticsearch secrets have been present in cluster configs chart since indexer, inbox services etc have dependency on elasticsearch secrets. Below is the template.

```
cd deploy-as-code/helm/charts/cluster-configs/templates/secrets
cat elasticsearch-master-creds-secret.yaml

# secret template

{{- with index .Values "cluster-configs" "secrets" "elasticsearch-master-creds" }}
{{- $passwordValue := (randAlphaNum 24) | b64enc | quote }}
{{- range $ns := .namespace }}
---
apiVersion: v1
kind: Secret
metadata:
  name: {{ index $.Values "cluster-configs" "secrets" "elasticsearch-master-creds" "name" }}
  namespace: {{ $ns }}
  labels:
    app: elasticsearch-master
type: Opaque
data:
  username: {{ "elastic" | b64enc }}
  {{- if index $.Values "cluster-configs" "secrets" "elasticsearch-master-creds" "password" }}
  password: {{ index $.Values "cluster-configs" "secrets" "elasticsearch-master-creds" "password" | b64enc | quote }}
  {{- else }}
  password: {{ $passwordValue }}
  {{- end }}
{{- end }}
---
{{- end }}


```

4. In cluster-configs values.yaml, add the namespaces in which you want to deploy the elasticsearch secrets.

{% embed url="https://github.com/egovernments/DIGIT-DevOps/blob/digit-lts-go/deploy-as-code/helm/charts/cluster-configs/values.yaml#L154" %}

5. Add the elasticsearch password in the env-secrets.yaml file, if not it will automatically creates a random password which will be updated everytime you deploy the elasticsearch.

{% embed url="https://github.com/egovernments/DIGIT-DevOps/blob/digit-lts-go/deploy-as-code/helm/environments/egov-demo-secrets.yaml#L102" %}

6. Deploy the Elastic Search Cluster using the below commands.

```
cd deploy-as-code/deployer
export KUBECONFIG=<path_to_kubeconfig>
kubectl config current-context
go run main.go deploy -c -e <env_file_name> elasticsearch-master
go run main.go deploy -e <env_file_name> elasticsearch-data
```

7. Check the pods status using the below command.

```
kubectl get pods -n <elasticsearch_namespace>
```

8. Once all pods are running, execute the below commands inside the playground pod to dump data from the old elasticsearch cluster and restore it to the new elasticsearch cluster.

{% code lineNumbers="true" %}
```
#!/bin/bash
# Elasticsearch cluster information
ELASTICSEARCH_OLD_URL="<old_elasticsearch_url>"    # eg:- elasticsearch-data-v1.es-cluster:9200
ELASTICSEARCH_NEW_URL="<new_elasticsearch_url>"    # eg:- elasticsearch-data.es-cluster:9200

# Authentication credentials
USERNAME="elastic"
PASSWORD="<es_pwd>"

DUMP_ENABLE=true
RESTORE_ENABLE=true

# Disable SSL/TLS validation
export NODE_TLS_REJECT_UNAUTHORIZED=0

# Provide the indices to take dump
EXCLUDE_INDEX_PATTERN="jaeger|monitor|kibana|fluentbit"
# Provide backup directory
BACKUP_DIR="backup"
# Provide indices output file
IDICES_OUTPUT="elasticsearch-indexes.txt"

INDICES_LIST=$(curl -sk "http://${ELASTICSEARCH_OLD_URL}/_cat/indices" | grep -v -E "${EXCLUDE_INDEX_PATTERN}" | awk '{print $3}')
IFS=$'\n' read -r -d '' -a INDICES <<< "$INDICES_LIST"

printf "%s\n" "${INDICES[@]}" > $IDICES_OUTPUT

if [ "$DUMP_ENABLE" = true ]; then
    # Create backup directory if it doesn't exist
    mkdir -p "$BACKUP_DIR"

    # Loop through each index and perform export
    for INDEX in "${INDICES[@]}"; do
        OUTPUT_FILE="${BACKUP_DIR}/${INDEX}_mapping_backup.json"

        # Build the elasticdump command
        ELASTICDUMP_CMD="elasticdump \
            --input=http://${ELASTICSEARCH_OLD_URL}/${INDEX} \
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
            --input=http://${ELASTICSEARCH_OLD_URL}/${INDEX} \
            --output=${OUTPUT_FILE} \
            --type=data
            --limit 10000"

        # Execute the elasticdump command
        $ELASTICDUMP_CMD

        # Check if the elasticdump command was successful
        if [ $? -eq 0 ]; then
            echo "Backup of index ${INDEX} completed successfully."
        else
            echo "Error backing up index ${INDEX}."
        fi
    done
fi

if [ "$RESTORE_ENABLE" = true ]; then
    for INDEX in "${INDICES[@]}"; do
        OUTPUT_FILE="${BACKUP_DIR}/${INDEX}_mapping_backup.json"
        
        # Process the mapping file to remove unsupported parameters

        PROCESSED_FILE="${BACKUP_DIR}/${INDEX}_mapping_processed.json"

        jq 'del(.mappings._default_, .mappings._meta, .mappings.dynamic_templates, .mappings.dynamic, .mappings.general) | .mappings = .mappings["_doc"]' "${INPUT_FILE}" > "${PROCESSED_FILE}"

        # Print the contents of the processed file for debugging

        echo "Contents of ${PROCESSED_FILE}:"

        cat "${PROCESSED_FILE}"

        # Build the elasticdump command
        ELASTICDUMP_CMD="elasticdump \
            --input=${PROCESSED_FILE} \
            --output=https://${USERNAME}:${PASSWORD}@${ELASTICSEARCH_NEW_URL}/${INDEX} \
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
            --output=https://${USERNAME}:${PASSWORD}@${ELASTICSEARCH_NEW_URL}/${INDEX} \
            --type=data
            --limit 10000"

        # Execute the elasticdump command
        $ELASTICDUMP_CMD

        # Check if the elasticdump command was successful
        if [ $? -eq 0 ]; then
            echo "Restoring of index ${INDEX} data completed successfully."
        else
            echo "Error Restoring index ${INDEX}."
        fi
    done
fi

```
{% endcode %}

{% code lineNumbers="true" %}
```
kubectl get pods -n playground
kubectl cp <path_to_script_in_your_machine>/es-dump.sh playground/<playground_name>:<path_in_playground_pod>/es-dump.sh

# Execute into the playground pod shell and run the below command
kubectl exec -it <playground_pod_name> -n playground  bash

# Run the script which takes dump of your elasticsearch data using below command
cd <path_to_script_inside_playground_pod>
chmod +x es-dump.sh
./es-dump.sh
```
{% endcode %}

9. Using the above script, you can take the data dump from the old cluster and restore it in the new elasticsearch in a single command.
10. After restoring the data successfully in the new elasticsearch cluster, check the cluster health and document count using the below command.&#x20;

{% code lineNumbers="true" %}
```
# Enter into elasticsearch pod
kubectl exec -it <elasticsearch_data_pod_name> -n <elasticsearch_namespace>  bash

# To check cluster health 
curl -k -X GET "https://elastic:<password>@<new_elasticsearch_url>/_cat/health?v=true&pretty"

# To check documents count and indices status
curl -k -X GET "https://elastic:<password>@<new_elasticsearch_url>/_cat/indices?v
```
{% endcode %}

11. Now the deployment and restoring the data are completed successfully. It's time to change the es\_url and indexer\_url in egov-config present under cluster-configs of the environment file. The same can be updated directly using the below command.

{% code lineNumbers="true" %}
```
kubectl edit configmap egov-config --namespace egov
```
{% endcode %}

{% embed url="https://github.com/egovernments/DIGIT-DevOps/blob/digit-lts-go/deploy-as-code/helm/environments/egov-demo.yaml#L24-L25" %}

12. Restart all the pods which have a dependency on elasticsearchwith cluster-configs  to pick a new elasticsearch\_url.

{% code lineNumbers="true" %}
```
go run main.go deploy -c -e <env_file.yaml> <service_image>
```
{% endcode %}
