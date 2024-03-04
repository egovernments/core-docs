# Backbone Deployment

On this page:

* [Overview](backbone-deployment.md#overview)
* [Pre-requisites](backbone-deployment.md#pre-requisites)
* [Deployment steps](backbone-deployment.md#deployment-steps)

## Overview

Once the cluster is ready and healthy you can start deploying backbones services.

Deploy configuration and deployment in the following Services Lists

1. Backbone (Redis, ZooKeeper-v2, Kafka-v2,elasticsearch-data-v1, elasticsearch-client-v1, elasticsearch-master-v1)
2. Gateway (Zuul, nginx-ingress-controller)

## Pre-requisites

* Understanding of VM Instances, LoadBalancers, SecurityGroups/Firewalls, nginx, DB Instances, and data volumes.
* Experience with Kubernetes, Docker, Jenkins, helm, golang, Infra-as-code.

## Deployment Steps

Deploy configuration and deployment backbone services:

1. Clone the git repo[ ![](https://github.githubassets.com/favicon.ico)https://github.com/egovernments/eGov-infraOps](https://github.com/egovernments/eGov-infraOps) . Copy existing [dev.yaml](https://github.com/egovernments/eGov-infraOps/blob/master/helm/environments/dev.yaml) and [dev-secrets.yaml](https://github.com/egovernments/eGov-infraOps/blob/master/helm/environments/dev-secrets.yaml) with new environment name (eg..yaml and-secrets.yaml)
2. Modify the global domain and set namespaces create to true

![](https://gblobscdn.gitbook.com/assets%2F-MERG\_iQW5oN4ukgXP8K%2F-MGrj6BrCyQtBc7G4ijs%2F-MGrupRtrQfYiFoTL3XU%2Fimage.png?alt=media\&token=8a640c33-f38c-4580-bf8c-caa157f34b6b)

3. Modify the below-mentioned changes for each backbone service:

Eg. For Kafka-v2&#x20;

4. If you are using **AWS as a cloud provider,** change the respective volume ids and zones. (You will get the volume ids and zone details from either a remote state bucket or from the AWS portal).

<div align="left">

<img src="https://gblobscdn.gitbook.com/assets%2F-MERG_iQW5oN4ukgXP8K%2F-MGrj6BrCyQtBc7G4ijs%2F-MGruyV9kiA__4LV9Lk4%2Fimage.png?alt=media&#x26;token=2cc00446-64c9-4f9f-8ac8-867e064ffc44" alt="">

</div>

Eg. Kafka-v2&#x20;

5. If you are using **Azure cloud provider,** change the diskName and diskUri. (You will get the volume ids and zone details from either the remote state bucket or from the Azure portal)

![](https://gblobscdn.gitbook.com/assets%2F-MERG\_iQW5oN4ukgXP8K%2F-MGrj6BrCyQtBc7G4ijs%2F-MGrv51muGFmWUGyVBK3%2Fimage.png?alt=media\&token=60131808-5004-463e-861c-9d777d32f09e)

Eg. Kafka-v2&#x20;

6. If you are using **ISCSI ,** change the targetPortal and iqn.

![](https://gblobscdn.gitbook.com/assets%2F-MERG\_iQW5oN4ukgXP8K%2F-MGrj6BrCyQtBc7G4ijs%2F-MGrv9UA0Up-YonBuNxS%2Fimage.png?alt=media\&token=aabe3f81-21a0-4973-be51-d2648a4f914d)

7. Deploy the backbone services using the go command

```
cd /eGov-infraOps/egov-deployergo run main.go deploy -e dev -p -c 'kafka-v2,redis,zookeeper-v2,elasticsearch-data-v1,elasticsearch-master-v1,playground,cert-manager,kafka-connect,kafka-connect-restart-tasks,kibana-v1,nginx-ingress'
```

8. Modify the “dev” environment name with your respective environment name.

**Flags**:

* e --- Environment name
* p --- Print the manifest
* c --- Enable Cluster Configs

Check the status of pods

```
kubectl get pods --all-namespaces
```

​
