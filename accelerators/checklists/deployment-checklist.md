# Deployment Checklist

To ensure smooth deployments and minimize potential issues, it's crucial to follow a thorough checklist. Here's a high-level overview:

1. Know what is going to get deployed
2. Excessive testing; preferably using a pipeline with automated tests
3. Know when is going to get deployed
4. Create backups
5. Deploy to production
6. Test on the live server

By adhering to this checklist, you can enhance control over deployments and reduce the likelihood of complications.

### Know what is put in version control <a href="#id-6ef3" id="id-6ef3"></a>

* [x] It is extremely important to know exactly what you put in version control. Make sure you mask passwords, or better put them in your file with environment variables, like a _.env_ file that contains all environments variables.
* [x] What’s less impactful, but definitely not what we want in .env, is to put in config files and version control.

## Testing <a href="#id-0433" id="id-0433"></a>

* [x] Before any piece of code gets deployed it should be tested thoroughly. Testing the code comes in different degrees.
* [x] Code reviews should be part of the routine of every team just to have an extra pair of eyes look at what is being deployed.
* [x] In the best-case scenario writing code should go hand-in-hand with writing automated tests for that same piece of code.

## Pipelines <a href="#id-505d" id="id-505d"></a>

* [x] Pipelines are flexible in a way that you could configure them however the most common components of a pipeline are build automation, test automation, and deployment automation.
* [x] Ensure that every change to the code is releasable and as easy pushing a button.

### 1. Application Development <a href="#application-development" id="application-development"></a>

Health checks

* **Containers have Readiness probes**
* **Containers crash when there's a fatal error**
* **Configure a passive Liveness probe**
* **Liveness probes values aren't the same as the Readiness**

Apps are independent

* **The Readiness probes are independent**
* **The app retries connecting to dependent services**

Graceful shutdown

* **The app doesn't shut down on SIGTERM, but it gracefully terminates connections**
* **The app still processes incoming requests in the grace period**
* **The CMD in the `Dockerfile` forwards the SIGTERM to the process**
* **Close all idle keep-alive sockets**

Fault tolerance

* **Run more than one replica for your Deployment**
* **Avoid Pods being placed into a single node**
* **Set Pod disruption budgets**

Resources utilisation

* **Set memory limits and requests for all containers**
* **Set CPU request to 1 CPU or below**
* **Disable CPU limits — unless you have a good use case**
* **The namespace has a LimitRange**
* **Set an appropriate Quality of Service (QoS) for Pods**

Tagging resources

* **Resources have technical labels defined**
* **Resources have business labels defined**
* **Resources have security labels defined**

Logging

* **The application logs to `stdout` and `stderr`**
* **Avoid sidecars for logging (if you can)**

Scaling

* **Containers do not store any state in their local filesystem**
* **Use the Horizontal Pod Autoscaler for apps with variable usage patterns**
* **Don't use the Vertical Pod Autoscaler while it's still in beta**
* **Use the Cluster Autoscaler if you have highly varying workloads**

Configuration and secrets

* **Externalise all configuration**
* **Mount Secrets as volumes, not environment variables**

### 2. Governance <a href="#governance" id="governance"></a>

Namespace limits

* **Namespaces have LimitRange**
* **Namespaces have ResourceQuotas**

Pod security policies

* **Enable Pod Security Policies**
* **Disable privileged containers**
* **Use a read-only filesystem in containers**
* **Prevent containers from running as root**
* **Limit capabilities**
* **Prevent privilege escalation**

Network policies

* **Enable network policies**
* **There's a conservative NetworkPolicy in every namespace**

Role-Based Access Control (RBAC) policies

* **Disable auto-mounting of the default ServiceAccount**
* **RBAC policies are set to the least amount of privileges necessary**
* **RBAC policies are granular and not shared**

Custom policies

* **Allow deploying containers only from known registries**
* **Enforce uniqueness in Ingress hostnames**
* **Only use approved domain names in the Ingress hostnames**

### 3. Cluster Configuration <a href="#cluster-configuration" id="cluster-configuration"></a>

Approved Kubernetes configuration

* **The cluster passes the CIS benchmark**
* **Disable metadata cloud providers metada API**
