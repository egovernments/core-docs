# ES-Curator to clear old logs/indices

#### What is es-curator? <a href="#what-is-es-curator" id="what-is-es-curator"></a>

Curator is a tool from Elastic (the company behind Elasticsearch) to help manage your Elasticsearch cluster. You can create, backup, and delete some indices, Curator helps make this process automated and repeatable. Curator is written in Python, so it is well supported by almost all operating systems. It can easily manage the huge number of logs that are written to the Elasticsearch cluster periodically by deleting them and thus helps you to save the disk space.

es-curator helm chart: [https://github.com/egovernments/DIGIT-DevOps/tree/release/config-as-code/helm/charts/backbone-services/es-curator](https://github.com/egovernments/DIGIT-DevOps/tree/release/config-as-code/helm/charts/backbone-services/es-curator)

A very elegant way to configure and automate Elasticsearch Curator execution is using a YAML configuration. The  **‘es-curator-infra-values.yaml’** file

```
# Common Labels
labels:
  group: "es-curator-infra"

cron:
  schedule: "45 18 * * *"  
# Container Configs
namespace: es-cluster-infra
image:
  repository: "bobrik/curator"
  tag: 5.6.0
logs-cleanup-enabled: true
jaeger-cleanup-enabled: true
logs-to-retain-in-days: 7  
memory_limits: 512Mi
args:
- --config
- /etc/config/config.yml
- /etc/config/action_file.yml

# Additional Container Envs
env: |
  - name: SERVER_PORT
    value: "8080"
  - name: JAVA_OPTS
    value: {{ index .Values "heap" | quote }}
  - name: ES_CLIENT_HOST
    valueFrom:
      configMapKeyRef:
        name: egov-config
        key: es-infra-host    
  - name: ES_CLIENT_PORT
    value: "9200"
  - name: LOG_LEVEL
    value: "DEBUG" 
  {{- if index .Values "logs-cleanup-enabled" }}                  
  - name: LOGS_CLEANUP_DISABLED
    value: "False"
  - name: RETAIN_LOGS_IN_DAYS
    value: {{ index .Values "logs-to-retain-in-days" | quote }}
  {{- end }}               
  {{- if index .Values "jaeger-cleanup-enabled" }}     
  - name: JAEGER_CLEANUP_DISABLED
    value: "False"
  - name: RETAIN_JAEGER_DATA_IN_DAYS
    value: "14"
  {{- end }}       
extraVolumes: |
  - name: config-volume
    configMap:
      name: {{ template "name" . }}-config
extraVolumeMounts: |
  - mountPath: /etc/config
    name: config-volume         
resources: |
  requests:
    memory: {{ .Values.memory_limits | quote }}
  limits:
    memory: {{ .Values.memory_limits | quote }}
```

You can modify the above es-curator-infra-values.yaml according to the requirements, some modifications are suggested below:

```
  schedule: "45 18 * * *"
```

<figure><img src="../../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

represents all the possible numbers for that position

* **Schedule Cron Job:** In the above code, at line number 6, the Cron Job is Scheduled to run at _18:45_ PM every day. You can schedule your Cron Job accordingly.
* **RETAIN\_LOGS\_IN\_DAYS:** You can specify how old the logs should be, to get deleted. At line number 14 of the above code, **logs-to-retain-in-days** specifies the logs that are older than 7 days will be deleted.
