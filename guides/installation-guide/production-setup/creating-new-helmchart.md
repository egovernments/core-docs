# Creating New HelmChart

## Overview

This documentation provides a detailed explanation of how to create a new helm chart using common templates and deploy it using helmfile.

## Pre-requisites

* helm

## Steps&#x20;

* Clone the DIGIT-DevOps repository using the below command and checkout to the DIGIT-2.9LTS branch.

```
$ git clone https://github.com/egovernments/DIGIT-DevOps.git
$ cd DIGIT-DevOps
$ git checkout DIGIT-2.9LTS
```

* Navigate to  the common\_chart\_template chart

```
$ cd deploy-as-code/charts/common-chart-template
```

* Edit the chart.yaml with your service\_name and update the dependency chart path.

```
apiVersion: v2
name: <service_name>
description: A Helm chart for Kubernetes

# A chart can be either an 'application' or a 'library' chart.
#
# Application charts are a collection of templates that can be packaged into versioned archives
# to be deployed.
#
# Library charts provide useful utilities or functions for the chart developer. They're included as
# a dependency of application charts to inject those utilities and functions into the rendering
# pipeline. Library charts do not define any templates and therefore cannot be deployed.
type: application

# This is the chart version. This version number should be incremented each time you make changes
# to the chart and its templates, including the app version.
version: 0.1.0

# This is the version number of the application being deployed. This version number should be
# incremented each time you make changes to the application.
appVersion: 1.16.0

dependencies:
- name: common
  version: 0.0.5
  repository: file://<path_to_common>
```

* Now, edit the values.yaml file to override the values present in the common chart and the values need to be provided for your service. If your service doesn't depend on db then you can disable the DB migration by setting the value enable as false. Also if you are using your docker account you need to update the docker container in the below values.yaml file.

```
$ cat values.yaml

# docker container
global:
    containerRegistry: <docker_account>
    
# Common Labels
labels:
  app: "<service_name>"
  group: "<service_group>"

# Ingress Configs
ingress:
  enabled: true
  zuul: true
  context: "<service_name>"

# Init Containers Configs
initContainers:
  dbMigration:
    enabled: true
    image:
      repository: "<image_name-db>"
      tag: <image_tag>

# Container Configs
image:
  repository: "<image_name>"
  tag: <image_tag>
replicas: "1"
tracing-enabled: true
healthChecks:
  enabled: true
  livenessProbePath: "/<service_name>/health"
  readinessProbePath: "/<service_name>/health"

# Additional Container Envs
env: |
  - name: <key>
    value: <value>
```

* After making these changes you need to provide this chart configuration in helmfile.yaml file

```
cat helmfile.yaml

releases:
- name: <service_name>
  chart: ./<path_to_chart>
  namespace: <namespace>
  installed: true
  version: <chart_version>
```
