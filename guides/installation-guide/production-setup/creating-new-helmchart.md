# Creating New HelmChart

## Overview

This documentation provides you with a detailed explanation of how to create a new helm chart using common templates and to deploy it using helmfile.

## Steps

* Run the below command to create a new helmchart.

```
$ helm create <service_name>
$ cd <service_name>
$ ls
$ cd templates
$ ls
```

* Remove all the templates that are not required for your service using the below command

```
$ rm -r <file_name>
```

* Clone the DIGIT-DevOps repository and checkout to required branch name in which you want to add the helmchart.
