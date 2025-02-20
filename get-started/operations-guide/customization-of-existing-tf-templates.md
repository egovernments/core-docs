# Customise Existing Terraform Templates

## Overview

This page provides details about customizing the sample-aws terraform template to set up the DIGIT infra in AWS.

## Pre-requisites

* [Install Visualstudio](https://code.visualstudio.com/download) IDE Code for better code/configuration editing capabilities
* Install [Terraform](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli) v0.14.10
* Install [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

## Customisation

* Clone the DIGIT-DevOps repo

```
$ git clone https://github.com/egovernments/DIGIT-DevOps.git
```

* Here we are using **AWS cloud service provider** to create terraform infra. So, we are choosing the **sample-aws module** (the **Terraform module** is a collection of standard configuration files in a dedicated directory).
* Open sample-aws in Visual Studio using the below command.

```
$ code DIGIT-DevOps/tree/release/infra-as-code/terraform/sample-aws
```

* In that **sample-aws** module, find the below terraform templates

{% code lineNumbers="true" %}
```
main.tf
providers.tf
outputs.tf
variables.tf
```
{% endcode %}

* **main.tf** will contain the main set of configurations for your module.
* **outputs.tf** will contain the output definitions for your module. Module outputs are made available to the configuration using the module, so they are often used to pass information about the parts of your infrastructure defined by the module to other parts of your configuration.
* **providers.tf** allows the terraform to interact with cloud providers and SAAS providers. In this sample-aws our provider is **AWS**.
* **variables.tf** contains the variable definitions for your module. When your module is used by others, the variables will be configured as arguments in the `module` block. Since all Terraform values must be defined, any variables that are not given a default value will become required arguments. Variables with default values can also be provided as module arguments, overriding the default value.
* To set up the DIGIT infra we made changes in **variables.tf**. Open **variables.tf** in Visual Studio using the below code.

```
$ code DIGIT-DevOps/tree/release/infra-as-code/terraform/sample-aws/variables.tf
```

* Change the values in **variables.tf** which are specified to replace based on our requirements.For **example: cluster\_name, network\_availability\_zones, availability\_zones, ssh\_key\_name, db\_name, db\_username.**
* After customizing the values in variables.tf, configure the **AWS credentials** using the below commands.

```
$ aws configure --profile <profile_name>
```

* Provide the AWS access key ID, AWS secret access key, Default region and Default output format.

<figure><img src="../../.gitbook/assets/Screenshot from 2022-12-20 22-15-02.png" alt=""><figcaption></figcaption></figure>

* Set the **aws\_session \_token** using the below command.

```
$ aws configure --profile <profile_name> set aws_session_token <session_token>
```

<figure><img src="../../.gitbook/assets/Screenshot from 2022-12-20 22-15-49.png" alt=""><figcaption></figcaption></figure>

* To make sure that aws credentials are configured use the below command.

```
$ aws s3 ls
```

* The output will be similar to the below image.

<div align="left"><figure><img src="../../.gitbook/assets/Screenshot from 2022-12-20 22-19-14.png" alt=""><figcaption></figcaption></figure></div>

* After that run the below commands in the terminal one after another.

```
$ terraform init
$ terraform apply
$ terraform plan
```

* **terraform init** is used to initialize your code to download the requirements mentioned in your code.
* **terraform plan** is used to review changes and choose whether to simply accept them or not.
* **terraform apply** is used to accept changes and apply them against real infrastructure.
* After successfully running these commands we can set up the infra in aws. We can see the **config file** which is used to deploy the environment.
* To destroy the terraform, use the below command.

```
terraform destroy
```
