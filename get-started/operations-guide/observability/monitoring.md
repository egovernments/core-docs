# Monitoring

There are many monitoring tools out there. Before choosing what we would work with on our client's Clusters, we need to consider many things. We use Prometheus and Grafana for Monitoring our and our client’s clusters.

![](https://miro.medium.com/max/1400/0*tbNYcUWT5XdWoVBO.png)

## Introduction <a href="#c581" id="c581"></a>

Monitoring is an important pillar of DevOps best practices. This gives you important information about the performance and status of your platform. This is even more true in distributed environments such as Kubernetes and microservices.

One of Kubernetes’ great strengths is its ability to extend its services and applications. When you reach thousands of applications, it’s impractical to manually monitor or use scripts. You need to adopt a scalable surveillance system! This is where Prometheus and Grafana come in.

Prometheus makes it possible to collect, store, and use platform metrics. Grafana, on the other hand, connects to Prometheus, allowing you to create beautiful dashboards and charts.

### Prometheus <a href="#f4d6" id="f4d6"></a>

**What is Prometheus?**

* **Prometheus** is an open-source monitoring and alerting toolkit designed for reliability and scalability.
* It collects and stores time-series data, allowing real-time monitoring of applications, infrastructure, and services.

**Key Features:**

* **Time-Series Data Collection**: Stores metrics with timestamps and labels.
* **Powerful Querying**: Uses **PromQL** (Prometheus Query Language) for data analysis.
* **Alerting Mechanism**: Integrated with **Alertmanager** to notify about critical issues.
* **Service Discovery**: Automatically detects targets (containers, pods, nodes) for monitoring.
* **Pull-Based Model**: Fetches metrics from targets instead of relying on push mechanisms.

### Loki

Distributed Log Aggregation System: Loki is an open-source log aggregation system built for cloud-native environments, designed to efficiently collect, store, and query log data. Loki was inspired by Prometheus and shares similarities in its architecture and query language, making it a natural complement to Prometheus for comprehensive observability.

<figure><img src="../../../.gitbook/assets/image (338).png" alt=""><figcaption></figcaption></figure>

#### Key Features

* Label-based Indexing
* LogQL Query Language
* Log Stream Compression
* Scalable and Cost-Efficient
* Integration with Grafana

<figure><img src="../../../.gitbook/assets/image (339).png" alt=""><figcaption></figcaption></figure>

### Alermanager

Alertmanager is a crucial component in the Prometheus ecosystem responsible for managing alerts and notifications. It receives alerts from Prometheus and processes them by grouping, deduplicating, and silencing them based on predefined rules. This ensures that notifications are sent only when necessary, reducing alert fatigue. Alertmanager supports multiple integrations, allowing alerts to be delivered via email, Slack, PagerDuty, and other communication channels. It also provides high availability by clustering multiple Alertmanager instances. By enabling effective alert management, Alertmanager helps DevOps and SRE teams maintain system reliability and quickly respond to incidents.

## Install Monitoring Tools Using Helmfile <a href="#ab21" id="ab21"></a>

### Pre-requisites

* Export the kubeconfig file to enable cluster login from the terminal.
* Command to install Helm, a package manager for Kubernetes that simplifies the deployment and management of applications using Helm charts.

```
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

* Commands to install Helmfile, which allows you to manage multiple Helm releases in a declarative manner.

```
wget https://github.com/helmfile/helmfile/releases/latest/download/helmfile_linux_amd64 -O /usr/local/bin/helmfile
chmod +x /usr/local/bin/helmfile
```

* Command to install the **Helm Diff** plugin, which allows you to compare the current Helm release with the proposed changes before applying them:

```
helm plugin install https://github.com/databus23/helm-diff
```

* Use the command below to install the decryption plugin. If it is already installed, you can skip this step.

<pre><code><strong>helm plugin install https://github.com/jkroepke/helm-secrets
</strong></code></pre>

* With this plugin, the encrypted key file will be automatically decrypted during deployment.
* command to verify the plugin istallation

```
helm plugin list
```

### Deployment Steps&#x20;

* Clone the repository

```
git clone https://github.com/egovernments/DIGIT-DevOps.git
```

* Command to change directory

```
cd DIGIT-DevOps
```

* Command to switch branch(monitoring tolls branch)

```
git checkout DIGIT-2.9LTS-monitoring
```

* Please refer to [this](../../../guides/operations-guide/observability/environment-changes.md) document for the required changes in the environment and secrets YAML files.
* Checkout to working directory

```
cd deploy-as-code/helm/charts/monitoring
```

* Generate and preview Kubernetes manifests to see what will be applied.

```
helmfile -e env -f monitoring-helmfile.yaml template
```

* Compare the current state with the new changes to see what will be modified.

```
helmfile -e env -f monitoring-helmfile.yaml diff
```

* use the below command to deploy the monitoring tools

```
helmfile -e env -f monitoring-helmfile.yaml apply
```

* This command will deploy all the monitoring tools.

### Connect To Alermanager Web Interface <a href="#id-4aae" id="id-4aae"></a>

The Alertmanager web UI is accessible through port-forward with this command:

```
kubectl port-forward svc/kube-prometheus-stack-alertmanager -n monitoring 9093:9093
```

Opening a browser tab on [http://localhost:9093](http://localhost:9093) shows the Alertmanager web UI.&#x20;

<figure><img src="../../../.gitbook/assets/image (342).png" alt=""><figcaption></figcaption></figure>

### Connect To Grafana <a href="#id-58fa" id="id-58fa"></a>

* &#x20;Grafana Dashboard URL: **DomainName/monitoring**

&#x20;       Ex: [https://unified-dev.digit.org/monitoring/](https://unified-dev.digit.org/monitoring/)

* Command to get the Grafana admin credentials

```
kubectl get secret grafana -n monitoring -o json | jq -r '.data | map_values(@base64d)'
```

<figure><img src="../../../.gitbook/assets/image (332).png" alt=""><figcaption></figcaption></figure>

* Use sign-in with Github for viewer access.

### Kubernetes Dashboards

<figure><img src="../../../.gitbook/assets/image (335).png" alt=""><figcaption><p>Grafana Dashboards</p></figcaption></figure>

## Dashboards Explanations

### 1. Blackbox Exporter:

<figure><img src="../../../.gitbook/assets/image (336).png" alt=""><figcaption></figcaption></figure>

* **Purpose**:
  * The dashboard monitors the health and availability of multiple HTTP endpoints using probes.
  * It tracks response status, latency, SSL details, and DNS lookup times.
* **Key Metrics**:
  * **Instance**: The URL of the monitored endpoint.
  * **Status**: Indicates whether the endpoint is **UP** (reachable) or **DOWN** (unreachable or failing).
  * **HTTP Code**: Displays the HTTP response code (e.g., 200 for success, 403 for forbidden, 503 for service unavailable).
  * **SSL Status**: Shows whether SSL/TLS is correctly configured.
  * **TLS Version**: Indicates the TLS version used (e.g., TLS 1.3).
  * **SSL Certificate Expiry**: Days remaining before the SSL certificate expires.
  * **Probe Duration**: The time taken to complete the probe request.
  * **DNS Lookup Duration**: The time required to resolve the domain name.
* **Observations**:
  * SSL is correctly configured for all monitored URLs with TLS 1.3.
  * Certificate expiry dates are tracked to prevent SSL disruptions.
  * Probe and DNS lookup durations help identify performance issues.

### 2. Kubernetes overview:

<figure><img src="../../../.gitbook/assets/Screenshot from 2025-03-11 21-33-09.png" alt=""><figcaption></figcaption></figure>

* **Purpose**:
  * Provides an overview of cluster-wide resource utilization.
  * Helps monitor CPU, memory, and resource allocation.
* **Key Metrics Monitored**:
  * **CPU Utilization**: Tracks real usage, requested, and limit allocations.
  * **Memory Utilization**: Monitors actual usage, requested, and allocated limits.
  * **Cluster Resources**: Displays active nodes, namespaces, and running pods.
  * **Kubernetes Object Counts**: Shows counts of containers, services, secrets, ingresses, PVCs, and other resources.
* **Insights & Utility**:
  * Identifies resource consumption trends.
  * Helps in optimizing resource requests and limits.
  * Assists in capacity planning and performance monitoring.

### 3. Namespaces Overview

<figure><img src="../../../.gitbook/assets/Screenshot from 2025-03-11 21-38-02.png" alt=""><figcaption></figcaption></figure>

* **Purpose**:
  * Monitors resource usage at the **namespace level**.
  * Helps track CPU, memory, and resource allocation per namespace.
* **Key Metrics Monitored**:
  * **CPU Usage**: Percentage and core utilization within the cluster.
  * **Memory Usage**: Percentage and actual memory consumption.
  * **Resource Count**: Tracks running pods, services, config maps, secrets, ingresses, and persistent volume claims.
* **Insights & Utility**:
  * Identifies high resource consumption namespaces.
  * Helps optimize requests and limits for efficient utilization.
  * Assists in monitoring namespace health and scaling decisions.

### 4. Nodes Overview

<figure><img src="../../../.gitbook/assets/Screenshot from 2025-03-11 21-41-54.png" alt=""><figcaption></figcaption></figure>

* **Purpose**:
  * Monitors individual node performance and resource utilization.
  * Provides insights into node-level workload distribution.
* **Key Metrics Tracked**:
  * **CPU & RAM Usage**: Current utilization and total capacity.
  * **Pod Count**: Number of running pods on the node.
  * **Uptime**: Node availability duration.
* **Insights & Utility**:
  * Helps detect resource bottlenecks or underutilized nodes.
  * Assists in load balancing and capacity planning.
  * Useful for troubleshooting node-specific performance issues.

### 5. Pods Overview

<figure><img src="../../../.gitbook/assets/Screenshot from 2025-03-11 22-31-09.png" alt=""><figcaption></figcaption></figure>

* **General Pod Information**
  * Displays pod details such as name, namespace, creation source, node it’s running on, and IP address.
  * Includes priority and QoS class to determine resource allocation behavior.
* **Resource Utilization Metrics**
  * Shows CPU and memory requests vs. limits for the pod.
  * Visualizes real-time utilization with gauges for quick assessment.
* **Container-Level Resource Usage**
  * Breaks down CPU and memory usage per container inside the pod.
  * Helps in identifying whether a container is over- or under-utilizing resources.
* **Performance Insights**
  * Helps monitor resource consumption to avoid over-provisioning or underutilization.
  * Supports scaling decisions based on actual usage trends.
* **Operational Use Case**
  * Useful for Kubernetes administrators to track performance, optimize configurations, and ensure stability in deployments.

### 6. Nginx Ingress Dashboard

<figure><img src="../../../.gitbook/assets/Screenshot from 2025-03-12 10-38-11.png" alt=""><figcaption></figcaption></figure>

* **Requests Overview**
  * Displays total HTTP requests over a specific period.
  * Shows the percentage of successful requests.
  * Provides active connections and recent request counts.
* **Success Rate & HTTP Status Codes**
  * Shows success percentage over a 2-minute window.
  * Categorizes HTTP responses:
    * **1xx/2xx:** Successful responses.
    * **3xx:** Redirects.
    * **4xx:** Client errors (e.g., 404, 499).
    * **5xx:** Server errors (e.g., 500, 502, 503).
* **Traffic Analysis**
  * **HTTP Requests / Ingress Graph:** Visualizes request trends over time.
  * **Total HTTP Requests Graph:** Breakdown of request types (color-coded for different status codes).
* **Additional Metrics**
  * **Latency Panels:** Measure response time.
  * **Connection Panels:** Monitor concurrent connections.
  * **CPU Intensive Graphs:** Helps in resource usage analysis.

### 7. Persistent Volume (PV) & Persistent Volume Claim Dashboard

<figure><img src="../../../.gitbook/assets/Screenshot from 2025-03-11 21-44-40.png" alt=""><figcaption></figcaption></figure>

* **Purpose**:
  * Monitors the status and usage of PVs and PVCs in the Kubernetes cluster.
  * Helps track storage capacity, usage trends, and potential issues.
* **Key Metrics Tracked**:
  * **PVC Utilization**: Shows if any PVCs are nearing full capacity.
  * **Storage Availability**: Displays available storage per PVC.
  * **PVC Status**: Indicates if PVCs are bound, pending, or lost.

### 8. Loki Grafana Dashboard

<figure><img src="../../../.gitbook/assets/image (318).png" alt=""><figcaption></figcaption></figure>

* **Log Filtering & Search**
  * Filtering logs based on namespaces, pods, and keywords (`error|fatal`).
  * Supports advanced search queries for efficient troubleshooting.
* **Real-Time Log Visualization**
  * Displays log frequency over time for better incident analysis.
  * Helps identify peaks in errors or warnings.
* **Log Source Details**
  * Shows logs from specific Loki stack components.
  * Includes metadata like timestamps, severity levels, and source pods.
* **Performance Insights**
  * Provides query execution details, including response times and processed log entries.
  * Helps optimize query performance for log retrieval.

### 9. Redis Monitoring Dashboard

<figure><img src="../../../.gitbook/assets/Screenshot from 2025-03-12 15-31-10.png" alt=""><figcaption></figcaption></figure>

* **Max Uptime**
  * Displays how long the Redis instance has been running without a restart (e.g., 6 days).
  * Helps track system stability and potential need for maintenance.
* **Clients**
  * Shows the number of active client connections (e.g., 35).
  * A high or fluctuating number might indicate load variations or connection issues.
* **Memory Usage**
  * Indicates the percentage of allocated memory in use (e.g., 83%).
  * High memory usage could lead to performance degradation or eviction of keys.
* **Total Commands per Second**
  * Displays the rate of commands being executed.
  * Spikes in command execution can indicate high activity or potential performance bottlenecks.
* **Hits/Misses per Second**
  * Tracks cache efficiency by measuring successful vs. failed key lookups.
  * A high miss rate may indicate suboptimal caching strategies.
* **Total Memory Usage**
  * Shows used vs. maximum memory allocation over time.
  * Helps identify memory growth trends and potential out-of-memory risks.
* **Network I/O**
  * Monitors data ingress and egress (e.g., in MiB).
  * Spikes may indicate high request loads or potential network-related issues.
* **Total Items per DB**
  * Represents the number of keys stored in each database instance.
  * Helps monitor data distribution and growth across databases.
* **Expiring vs. Non-Expiring Keys**
  * Tracks how many keys are set to expire vs. persistent ones.
  * Useful for understanding key retention policies and potential memory optimizations.
