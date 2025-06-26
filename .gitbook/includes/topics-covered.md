---
title: Setup AWS Account
---

# Overview

Follow the details below to set up your AWS account before you proceed with the DIGIT deployment.

## **Get AWS Access**

<details>

<summary><strong>Public Users</strong></summary>

* Sign up for the AWS account if you do not already have one. Use this link to [get started](https://aws.amazon.com/getting-started/)
* Assign Administrator Access to the IAM user for necessary permissions.
* Use the [**AWS IAM User**](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html) **credentials provided** for the Terraform ([**Infra-as-code**](../../guides/installation-guide/infrastructure-setup/azure/3.-infra-as-code-terraform.md)) to connect with your AWS account and provision the cloud resources.
* The system will generate a **Secret Access Key** and **Access Key ID**. **Save the keys.**
* Open the terminal. Run the following command you have installed on the AWS CLI and use the credentials. (Provide the credentials and leave the region and output format blank).

**Note: Make sure the profile name provided in the commands below is also used in the Terraform scripts same as the AWS profile.**

```
aws configure --profile digit-quickstart-poc 

AWS Access Key ID []:<Your access key>
AWS Secret Access Key []:<Your secret key>
Default region name []: ap-south-1
Default output format []: text
```

```
// Setting profile
export AWS_PROFILE=digit-quickstart-poc
```

* The above will create the following file in your machine under the user home directory. /path/to/user/home/.aws/credentials

```
[digit-quickstart-poc] 
aws_access_key_id=*********** 
aws_secret_access_key=*************************
```

</details>

Once the command line access is configured, everything is set to proceed with the Terraform to provision the DIGIT Infra-as-code.
