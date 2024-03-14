---
description: Setting up DIGIT  using helmfile
---

# DIGIT Deployment Using Helmfile

## Overview

This page walks you through the steps required to set up DIGIT using helmfile.

## Pre-requisites

* [helmfile](https://helmfile.readthedocs.io/en/latest/)
* git
* Kubernetes Cluster

Helmfile is a declarative spec for deploying helm charts. It lets you…

* Keep a directory of chart value files and maintain changes in version control.
* Apply CI/CD to configuration changes.
* Periodically sync to avoid skew in environments.

To avoid upgrades for each iteration of `helm`, the `helmfile` executable delegates to `helm` - as a result, [`helm`](https://helm.sh/docs/intro/install/) must be installed.

### Why Helmfile <a href="#installation" id="installation"></a>

* Standardisation of Helm templates (Override specific parameters such as namespace)
* To improve Utilisation of Helm capabilities (Rollback)
* Easy to add any open-source helm chart in your DIGIT stack

## Installation <a href="#installation" id="installation"></a>

* download one of [releases](https://github.com/helmfile/helmfile/releases)
* run as a container
* Archlinux: install via `pacman -S helmfile`
* open SUSE: install via `zypper in helmfile` assuming you are on Tumbleweed; if you are on Leap you must add the [kubic](https://download.opensuse.org/repositories/devel:/kubic/) repo for your distribution version once before that command, e.g. `zypper ar https://download.opensuse.org/repositories/devel:/kubic/openSUSE_Leap_\$releasever kubic`
* Windows (using [scoop](https://scoop.sh/)): `scoop install helmfile`
* macOS (using [homebrew](https://brew.sh/)): `brew install helmfile`

#### Running as a container <a href="#running-as-a-container" id="running-as-a-container"></a>

The [Helmfile Docker images are available in GHCR](https://github.com/helmfile/helmfile/pkgs/container/helmfile). There is no `latest` tag, since the `0.x` versions can contain breaking changes, so make sure you pick the right tag. Example using `helmfile 0.156.0`:

```sh-session
$ docker run --rm --net=host -v "${HOME}/.kube:/helm/.kube" -v "${HOME}/.config/helm:/helm/.config/helm" -v "${PWD}:/wd" --workdir /wd ghcr.io/helmfile/helmfile:v0.156.0 helmfile sync
```

You can also use a shim to make calling the binary easier:

```sh-session
$ printf '%s\n' '#!/bin/sh' 'docker run --rm --net=host -v "${HOME}/.kube:/helm/.kube" -v "${HOME}/.config/helm:/helm/.config/helm" -v "${PWD}:/wd" --workdir /wd ghcr.io/helmfile/helmfile:v0.156.0 helmfile "$@"' |
    tee helmfile
$ chmod +x helmfile
$ ./helmfile sync
```

## Helm File - commands

### init

The helmfile init sub-command checks the dependencies required for helmfile operation, such as helm, helm diff plugin, helm secrets plugin, helm helm-git plugin, helm s3 plugin. When it does not exist or the version is too low, it can be installed automatically.

### sync

The helmfile sync sub-command sync your cluster state as described in your helmfile. The default helmfile is helmfile.yaml, but any YAML file can be passed by specifying a --file path/to/your/yaml/file flag.

### apply

The helmfile apply sub-command begins by executing diff. If diff finds that there is any changes, sync is executed. Adding --interactive instructs Helm File to request your confirmation before sync.

### destroy

The helmfile destroy sub-command uninstalls and purges all the releases defined in the manifests. helmfile --interactive destroy instructs Helm File to request your confirmation before actually deleting releases.\


## Deploying DIGIT Using Helmfile

```
$ git clone https://github.com/egovernments/DIGIT-DevOps.git
$ cd DIGIT-DevOps
$ git checkout DIGIT-2.9LTS(Helmfile)
```

* Update domain name in env.yaml

```
$ vi deploy-as-code/charts/environments/env.yaml
```

<figure><img src="../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

* Update db password , flywaypassword, loginusername, loginpassword  and git-sync private key in env-secrets.yaml

&#x20;           **Note:**  Make sure the db\_password and flywaypassword are same

```
$ vi deploy-as-code/charts/environments/env-secrets.yaml
```

<figure><img src="../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Note** &#x20;

1\. Generate ssh key pairs using below method \
Using online website (not recommended in production setup. To be only used for demo setups): [https://8gwifi.org/sshfunctions.jsp](https://8gwifi.org/sshfunctions.jsp)\
2\. Add the public key to your github account - (reference: [https://www.youtube.com/watch?v=9C7\_jBn9XJ0\&ab\_channel=AOSNote](https://www.youtube.com/watch?v=9C7\_jBn9XJ0\&ab\_channel=AOSNote) )
{% endhint %}

* Run the below command to successfully install the DIGIT.

```
$ helmfile -f deploy-as-code/digit-helmfile.yaml apply
```

## **Deploying DIGIT Using Managed Database**

This guide outlines a deployment strategy for running containerized applications on Kubernetes, focusing on seamless database integration. It's suitable for teams looking to simplify their database setup, whether using in-cluster PostgreSQL or external managed database services.

### Transitioning to Managed Database Services

By updating the Kubernetes deployment configuration, teams can easily switch from an in-cluster PostgreSQL database to a managed service. This move enhances scalability and reliability while reducing the operational overhead of database management.

#### Key Benefits:

* **Scalability and Reliability:** Managed services offer superior scalability and reliability compared to in-cluster databases.
* **Reduced Operational Overhead:** Outsourcing database management allows teams to concentrate on application development.

### Integration Steps

```
$ git clone https://github.com/egovernments/DIGIT-DevOps.git
$ cd DIGIT-DevOps
$ git checkout DIGIT-2.9LTS(Helmfile)
```

*   To integrate a managed PostgreSQL service, modify the following parameters in the&#x20;

    deploy-as-code/charts/environments/env.yaml  configuration file:

    * `db-host`: Update with the database service host address.
    * **`db-name`**: Update with the specific database name.
    * `db-url`: Update with the complete database connection URL.
    * `domain`: Update domain name with your domain name

```
$ vi deploy-as-code/charts/environments/env.yaml
```

<figure><img src="../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

* Update db password , db username, flyway username, flyway password, login username, login password  and git-sync private key in env-secrets.yaml

```
$ vi deploy-as-code/charts/environments/env-secrets.yaml
```

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Note:**  1. Generate ssh key pairs using below method \
Using online website (not recommended in production setup. To be only used for demo setups): [https://8gwifi.org/sshfunctions.jsp](https://8gwifi.org/sshfunctions.jsp)\
2\. Add the public key to your github account - (reference: [https://www.youtube.com/watch?v=9C7\_jBn9XJ0\&ab\_channel=AOSNote](https://www.youtube.com/watch?v=9C7\_jBn9XJ0\&ab\_channel=AOSNote) )
{% endhint %}

* Run the below command to successfully install the DIGIT.

```
$ helmfile -f deploy-as-code/digit-helmfile.yaml apply    
```

## Post Deployment

Please hit the below url to login into the employee dashboard with SUPERUSER access

```
https://<domain_name>/employee
```

Login with the user credentials which you have provided in the below file path

```
deploy-as-code/charts/environments/env-secrets.yaml
```

## **Destroying The Deployed DIGIT Using Helmfile**

```
$ helmfile -f deploy-as-code/digit-helmfile.yaml destroy
```

\
Tested Environment

This deployment approach has been thoroughly tested on an Amazon Web Services Elastic Kubernetes Service (AWS EKS) Cluster with Kubernetes version 1.28.\
