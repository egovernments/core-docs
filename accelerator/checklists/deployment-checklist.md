# Deployment Checklist

To ensure smooth deployments and minimize potential issues, it's crucial to follow a thorough checklist. Here's a high-level overview:

1. Know what is going to get deployed&#x20;
2. Excessive testing; preferably using a pipeline with automated tests&#x20;
3. Know when is going to get deployed&#x20;
4. Create backups&#x20;
5. Deploy to production&#x20;
6. Test on the live server

By adhering to this checklist, you can enhance control over deployments and reduce the likelihood of complications.

### Know what is put in version control <a href="#id-6ef3" id="id-6ef3"></a>

* [x] It is extremely important to know exactly what you put in version control. Make sure you mask passwords, or better put them in your file with environment variables, like a _.env_ file that contains all environments variables.
* [x] What’s less impactful, but definitely not what we want in .env, is to put in config files and version control.

## Testing <a href="#id-0433" id="id-0433"></a>

* [x] Before any piece of code gets deployed it should be tested thoroughly. Testing the code comes in different degrees.&#x20;
* [x] Code reviews should be part of the routine of every team just to have an extra pair of eyes look at what is being deployed.&#x20;
* [x] In the best-case scenario writing code should go hand-in-hand with writing automated tests for that same piece of code.&#x20;

## Pipelines <a href="#id-505d" id="id-505d"></a>

* [x] Pipelines are flexible in a way that you could configure them however the most common components of a pipeline are build automation, test automation, and deployment automation.
* [x] Ensure that every change to the code is releasable and as easy pushing a button.

### 1. Application Development <a href="#application-development" id="application-development"></a>

Health checks

* #### Containers have Readiness probes <a href="#containers-have-readiness-probes" id="containers-have-readiness-probes"></a>
* #### Containers crash when there's a fatal error <a href="#containers-crash-when-there-s-a-fatal-error" id="containers-crash-when-there-s-a-fatal-error"></a>
* #### Configure a passive Liveness probe <a href="#configure-a-passive-liveness-probe" id="configure-a-passive-liveness-probe"></a>
* #### Liveness probes values aren't the same as the Readiness <a href="#liveness-probes-values-aren-t-the-same-as-the-readiness" id="liveness-probes-values-aren-t-the-same-as-the-readiness"></a>

Apps are independent

* #### The Readiness probes are independent <a href="#the-readiness-probes-are-independent" id="the-readiness-probes-are-independent"></a>
* #### The app retries connecting to dependent services <a href="#the-app-retries-connecting-to-dependent-services" id="the-app-retries-connecting-to-dependent-services"></a>

Graceful shutdown

* #### The app doesn't shut down on SIGTERM, but it gracefully terminates connections <a href="#the-app-doesn-t-shut-down-on-sigterm-but-it-gracefully-terminates-connections" id="the-app-doesn-t-shut-down-on-sigterm-but-it-gracefully-terminates-connections"></a>
* #### The app still processes incoming requests in the grace period <a href="#the-app-still-processes-incoming-requests-in-the-grace-period" id="the-app-still-processes-incoming-requests-in-the-grace-period"></a>
* #### The CMD in the `Dockerfile` forwards the SIGTERM to the process <a href="#the-cmd-in-the-dockerfile-forwards-the-sigterm-to-the-process" id="the-cmd-in-the-dockerfile-forwards-the-sigterm-to-the-process"></a>
* #### Close all idle keep-alive sockets <a href="#close-all-idle-keep-alive-sockets" id="close-all-idle-keep-alive-sockets"></a>

Fault tolerance

* #### Run more than one replica for your Deployment <a href="#run-more-than-one-replica-for-your-deployment" id="run-more-than-one-replica-for-your-deployment"></a>
* #### Avoid Pods being placed into a single node <a href="#avoid-pods-being-placed-into-a-single-node" id="avoid-pods-being-placed-into-a-single-node"></a>
* #### Set Pod disruption budgets <a href="#set-pod-disruption-budgets" id="set-pod-disruption-budgets"></a>

Resources utilisation

* #### Set memory limits and requests for all containers <a href="#set-memory-limits-and-requests-for-all-containers" id="set-memory-limits-and-requests-for-all-containers"></a>
* #### Set CPU request to 1 CPU or below <a href="#set-cpu-request-to-1-cpu-or-below" id="set-cpu-request-to-1-cpu-or-below"></a>
* #### Disable CPU limits — unless you have a good use case <a href="#disable-cpu-limits-unless-you-have-a-good-use-case" id="disable-cpu-limits-unless-you-have-a-good-use-case"></a>
* #### The namespace has a LimitRange <a href="#the-namespace-has-a-limitrange" id="the-namespace-has-a-limitrange"></a>
* #### Set an appropriate Quality of Service (QoS) for Pods <a href="#set-an-appropriate-quality-of-service-qos-for-pods" id="set-an-appropriate-quality-of-service-qos-for-pods"></a>

Tagging resources

* #### Resources have technical labels defined <a href="#resources-have-technical-labels-defined" id="resources-have-technical-labels-defined"></a>
* #### Resources have business labels defined <a href="#resources-have-business-labels-defined" id="resources-have-business-labels-defined"></a>
* #### Resources have security labels defined <a href="#resources-have-security-labels-defined" id="resources-have-security-labels-defined"></a>

Logging

* #### The application logs to `stdout` and `stderr` <a href="#the-application-logs-to-stdout-and-stderr" id="the-application-logs-to-stdout-and-stderr"></a>
* #### Avoid sidecars for logging (if you can) <a href="#avoid-sidecars-for-logging-if-you-can" id="avoid-sidecars-for-logging-if-you-can"></a>

Scaling

* #### Containers do not store any state in their local filesystem <a href="#containers-do-not-store-any-state-in-their-local-filesystem" id="containers-do-not-store-any-state-in-their-local-filesystem"></a>
* #### Use the Horizontal Pod Autoscaler for apps with variable usage patterns <a href="#use-the-horizontal-pod-autoscaler-for-apps-with-variable-usage-patterns" id="use-the-horizontal-pod-autoscaler-for-apps-with-variable-usage-patterns"></a>
* #### Don't use the Vertical Pod Autoscaler while it's still in beta <a href="#don-t-use-the-vertical-pod-autoscaler-while-it-s-still-in-beta" id="don-t-use-the-vertical-pod-autoscaler-while-it-s-still-in-beta"></a>
* #### Use the Cluster Autoscaler if you have highly varying workloads <a href="#use-the-cluster-autoscaler-if-you-have-highly-varying-workloads" id="use-the-cluster-autoscaler-if-you-have-highly-varying-workloads"></a>

Configuration and secrets

* #### Externalise all configuration <a href="#externalise-all-configuration" id="externalise-all-configuration"></a>
* #### Mount Secrets as volumes, not environment variables <a href="#mount-secrets-as-volumes-not-enviroment-variables" id="mount-secrets-as-volumes-not-enviroment-variables"></a>

### 2. Governance <a href="#governance" id="governance"></a>

Namespace limits

* #### Namespaces have LimitRange <a href="#namespaces-have-limitrange" id="namespaces-have-limitrange"></a>
* #### Namespaces have ResourceQuotas <a href="#namespaces-have-resourcequotas" id="namespaces-have-resourcequotas"></a>

Pod security policies

* #### Enable Pod Security Policies <a href="#enable-pod-security-policies" id="enable-pod-security-policies"></a>
* #### Disable privileged containers <a href="#disable-privileged-containers" id="disable-privileged-containers"></a>
* #### Use a read-only filesystem in containers <a href="#use-a-read-only-filesystem-in-containers" id="use-a-read-only-filesystem-in-containers"></a>
* #### Prevent containers from running as root <a href="#prevent-containers-from-running-as-root" id="prevent-containers-from-running-as-root"></a>
* #### Limit capabilities <a href="#limit-capabilities" id="limit-capabilities"></a>
* #### Prevent privilege escalation <a href="#prevent-privilege-escalation" id="prevent-privilege-escalation"></a>

Network policies

* #### Enable network policies <a href="#enable-network-policies" id="enable-network-policies"></a>
* #### There's a conservative NetworkPolicy in every namespace <a href="#there-s-a-conservative-networkpolicy-in-every-namespace" id="there-s-a-conservative-networkpolicy-in-every-namespace"></a>

Role-Based Access Control (RBAC) policies

* #### Disable auto-mounting of the default ServiceAccount <a href="#disable-auto-mounting-of-the-default-serviceaccount" id="disable-auto-mounting-of-the-default-serviceaccount"></a>
* #### RBAC policies are set to the least amount of privileges necessary <a href="#rbac-policies-are-set-to-the-least-amount-of-privileges-necessary" id="rbac-policies-are-set-to-the-least-amount-of-privileges-necessary"></a>
* #### RBAC policies are granular and not shared <a href="#rbac-policies-are-granular-and-not-shared" id="rbac-policies-are-granular-and-not-shared"></a>

Custom policies

* #### Allow deploying containers only from known registries <a href="#allow-deploying-containers-only-from-known-registries" id="allow-deploying-containers-only-from-known-registries"></a>
* #### Enforce uniqueness in Ingress hostnames <a href="#enforce-uniqueness-in-ingress-hostnames" id="enforce-uniqueness-in-ingress-hostnames"></a>
* #### Only use approved domain names in the Ingress hostnames <a href="#only-use-approved-domain-names-in-the-ingress-hostnames" id="only-use-approved-domain-names-in-the-ingress-hostnames"></a>

### 3. Cluster Configuration <a href="#cluster-configuration" id="cluster-configuration"></a>

Approved Kubernetes configuration

* #### The cluster passes the CIS benchmark <a href="#the-cluster-passes-the-cis-benchmark" id="the-cluster-passes-the-cis-benchmark"></a>
* #### Disable metadata cloud providers metada API <a href="#disable-metadata-cloud-providers-metada-api" id="disable-metadata-cloud-providers-metada-api"></a>
