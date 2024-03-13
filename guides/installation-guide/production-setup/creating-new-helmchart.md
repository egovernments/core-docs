---
description: >-
  This documentation provides you a detail explanation on how to create a new
  helm chart using common templates and to deploy it using helmfile
---

# Creating New HelmChart

* Run the below command to create new helmchart

```
$ helm create <service_name>
$ cd <service_name>
$ ls
$ cd templates
$ ls
```

* Remove all the templates that are not required for your service using below command

```
$ rm -r <file_name>
```

* Now, Clone the DIGIT-DevOps repositority and checkout to your required branch name in which you want to add the helmchart.
