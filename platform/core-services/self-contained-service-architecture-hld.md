---
description: Handler to manage and simplify service configurations
---

# Self Contained Service Architecture (HLD)

## Overview <a href="#objective" id="objective"></a>

The objective of this module is to handle configurations of services in a centralised manner. The overall objective of the architecture is to simplify configuration handling and remove the need for manual pod restarts to refresh the configurations. The configurations that can be added by this handler are MDMS, pdf, persister, indexer, DSS, reports, workflow and localisation.

### Problems With Existing Approach <a href="#problems-with-existing-approach" id="problems-with-existing-approach"></a>

Currently, any developer who is working on a new service has to check in configuration at 6 different places (including reports, pdf templates etc.). After checking in the configuration the developer has to restart all of these 6 pods. Once this is done, the developer needs cURL for workflow and localisation service to insert their configuration/data. The whole process is long, tedious and error-prone (many times people forget to restart pods after adding config). This approach requires access to GitHub and Jenkins which is not possible in the case of a sandbox environment.

## API Details <a href="#api-details" id="api-details"></a>

The handler will provide API endpoints to manage configurations. The structure of the API request is as follows:

{% code lineNumbers="true" %}
```
[
  {
    "module": "persister",
    "configs": [...]
  },
  {
    "module": "indexer",
    "configs": [...]
  },
  {
    "module": "workflow",
    "configs": [...]
  }
]
```
{% endcode %}

The request contains an array of objects. Each object contains the module name and the configuration that has to be added.

The handler contains two APIs: _\_create_ and _\_update_.&#x20;

The \_create API is used to add configuration for the first time. It works in an idempotent manner i.e if any configuration is already present it ignores it (will not add that particular config). This API is used to integrate modules. During application initialisation, the service calls the API to add the default configurations (if required).&#x20;

The _\_update_ API is called for any further changes to the configuration.

### Moving Config To MDMS <a href="#moving-config-to-mdms" id="moving-config-to-mdms"></a>

Currently, services like Persister, Indexer, etc. use a git-sync container to load configuration files. Usually, the developer runs the services as sidecar containers. Each service requires one. The containers can be removed from all these services by enhancing the MDMS service. Using this approach only the MDMS service is required to run the git-sync pod.&#x20;

**Steps:**

* The service(s) loads the configuration files by calling the MDMS service.&#x20;
* MDMS service returns the requested configuration files.&#x20;

{% hint style="info" %}
**Note:**&#x20;

1. We can prevent the existing resource loader logic to load from the resource folder. In addition to that, we can provide another type of resource loader that fetches from MDMS. Based on the environment variable it selects the loader.
2. Currently, MDMS data is in JSON format. We need to add support (if not present) for YAML files to serve the configuration from MDMS. (Another way is to change the configuration format from YAML to JSON).
{% endhint %}

## Design <a href="#design" id="design"></a>

<figure><img src="../../.gitbook/assets/Config Handler with config in MDMS.png" alt=""><figcaption></figcaption></figure>

The configuration handler integrates with Git and the required DIGIT services (workflow, localisation etc.) to add/update configuration. Once the configuration is added in Git, the pods using this configuration pull the latest changes. There are multiple approaches to achieving this. Below is the list of approaches with their pros and cons.

### **1. Periodic Pull Using Git-sync**

The git-sync runs as a sidecar container instead of an init container and periodically pulls the Git repo based on configured frequency. We can configure the frequency to around 1-2 mins.

{% hint style="info" %}
**Note:** Git-sync checks the hash first and pulls the data only if the hash has changed.
{% endhint %}

**Pros:**

The approach is easy to implement without any need to write new code.

**Cons:**

Data is not refreshed instantly. There will be a lag of 1-2 mins. (Currently, it takes 3-4 min to refresh data as the pod needs to be redeployed).

### **2. Modify Git-sync Code**

Understand and modify the git-sync code to expose an endpoint for manual pull. Whenever the config handler uploads configs on Git it calls the API of the modified git-sync container to initiate the pull.

**Pros:**

Updated configurations will reflect within a few seconds.

**Cons:**

Will increase the development time and efforts.

### Refreshing The Configuration <a href="#refreshing-the-configuration" id="refreshing-the-configuration"></a>

* Once the configuration is pulled by git-sync the services are notified to reload the configuration.&#x20;
* Git-sync provides webhooks which are called once the new hash is synced.&#x20;
* Add one _/config/\_refresh_ API in each of these services and configure them in git-sync. Whenever git-sync pulls data successfully it triggers _\_refresh_ API which in turn refreshes the configuration.
* Since the \_refresh API call goes to only one pod, only that pod will refresh the data. Because of this, we cannot use the local cache.&#x20;
* This requires a cluster-aware caching implementation and this can be done using the Redis instance that is already deployed. Move the configuration to Redis - even if one pod refreshes the cache it reflects in all the pods for that service.
* For services like indexer and persister which load consumers from configuration, cache burst does not work. For this we need to use configuration versioning. In the cache, we store the configuration along with the hash associated with that version. Services like indexer and persister maintain a variable called localOperatingConfigHash in its heap memory. Whenever it fetches data from the Redis cache it compares the localOperatingConfigHash with the current hash(version) of the configuration. If it matches it goes ahead and performs the process. In case it is not the same, it reloads the consumers from the new configuration and updates the localOperatingConfigHash to the value it got from the Redis cache.

<figure><img src="../../.gitbook/assets/Persister local hash.png" alt=""><figcaption></figcaption></figure>

* Another optimised approach is that the persister service fetches the configs when \_refresh API is called. After fetching the config the service gets all the topics present in the configs and get a hash of that list of topics. This hash service is set in its local variable and adds it in the Redis along with the configs. When another pod fetches the config and hash from Redis it compares the hash with its local hash and based on that it restarts consumers. In this way, consumers are restarted only when topics are added or removed.

### Tracer Enhancements <a href="#tracer-enhancements" id="tracer-enhancements"></a>

The tracer library can be updated to automatically connect with the config handler module during initialisation. The tracer module works by using a variable called _**tracer.config.path**_. This variable contains the path where the configuration json is present. By default, it points to the resource folder inside the code base, but for production use cases it can be overwritten with Git URL or any other valid file path as per requirement.

{% hint style="info" %}
### Open Points For Discussion <a href="#open-points-for-discussion" id="open-points-for-discussion"></a>

1. Helm Charts:

Should we think about adding the service helm chart as part of the module code base? We can think of generating it dynamically based on a moustache template.

2\. Approaches to Deploy Config Handler (if we don’t want to provide \_update API):

There are 3 ways we can deploy the config handler if we are trying to use it only by adding config during deployment:

* Config handler code will be part of the tracer
* We create a separate client for the config handler
* We create a separate service and run it as an init container

If we want it to provide \_update API as well then we need to deploy it as a separate microservice.
{% endhint %}
