---
description: Installation Guide for DIGIT via GitHub Actions in AWS
---

# DIGIT Deployment Using GitHub Actions

## Pre-requisites

* AWS account
* Github account

## Installation

### Prepare AWS IAM User

1. Create an IAM User in your AWS account.
2. Generate `ACCESS_KEY` and `SECRET_KEY` for the IAM user.
3. Assign Administrator Access to the IAM user for necessary permissions.

### Configure GitHub Repository

1. Fork the DIGIT-DevOps Repository into your organization account on GitHub.
2. Navigate to the repository settings, then to Secrets and Variables, click actions and add the following repository secrets:
   * `AWS_ACCESS_KEY_ID: <GENERATED_ACCESS_KEY>`
   * `AWS_SECRET_ACCESS_KEY: <GENERATED_SECRET_KEY>`
   * `AWS_DEFAULT_REGION: ap-south-1`
   * `AWS_REGION: ap-south-1`
3. Enable GitHub Actions
   * Clone the DIGIT-DevOps repository which you've forked and open the repo in the code editor.
   * Switch the branch from master to DIGIT-2.9LTS using the below command.

<pre><code><strong>git checkout DIGIT-2.9LTS
</strong></code></pre>

* Open the GitHub Actions workflow file.
* Specify the branch name you wish to enable GitHub Actions for.

### Configure Infrastructure-as-Code

1. Navigate to `infra-as-code/terraform/sample-aws`.
2. Open `input.yaml` and enter details such as `domain_name`, `cluster_name`, `bucket_name`, `db_name` and add  `public_ssh_key` generated using below SSH Key Pair.

### Configure Application Secrets

1. Navigate to deploy`-as-code/charts/environments`.
2. Open `env-secrets.yaml`.
3. Enter `db_password` and `ssh_private_key`. Add the `public_key` to your GitHub account.

### Generate SSH Key Pair

Choose one of the following methods to generate an SSH key pair:

* **Method a:** Use an online website (Note: This is not recommended for production setups, only for demo purposes): `https://8gwifi.org/sshfunctions.jsp`
*   **Method b:** Use OpenSSL commands:

    ```
    openssl genpkey -algorithm RSA -out private_key.pem
    openssl rsa -pubout -in private_key.pem -out public_key.pem
    ```

### Finalize Installation

After entering all the details, push these changes to the remote GitHub repository. Open the `Actions` tab in your GitHub account to view the workflow. You should see that the workflow has started, and the pipelines are completed successfully.

<figure><img src="../../../../.gitbook/assets/Screenshot 2024-03-06 at 12.55.10 PM.png" alt=""><figcaption><p>Github actions workflow that gets created after committing the inputs</p></figcaption></figure>

This indicates that your setup is correctly configured, and your application is ready to be deployed. Monitor the output of the workflow for any errors or success messages to ensure everything is functioning as expected.

### KubeConfig Setup

For guidance on setting up your AWS CLI, please follow the instructions provided in [Installation Guide - Production Setup on AWS](https://core.digit.org/guides/installation-guide/production-setup/aws/3.-setup-aws-account). Additionally, ensure your AWS CLI is correctly configured by referring to the official AWS documentation on Configuring the AWS CLI - AWS Command Line Interface. Confirm your AWS credentials are correctly set by executing:

```
aws configure list --profile <profile_name>
```

Proceed only after verifying the correct configuration of your credentials. For any uncertainties on how to set up the credentials, consult the AWS documentation for detailed instructions.

<figure><img src="../../../../.gitbook/assets/image (316).png" alt=""><figcaption></figcaption></figure>

Run the below command to export AWS Credentials

```
export AWS_PROFILE=<profile_name>
```

Use this link to [get the kubeconfig from EKS](https://docs.aws.amazon.com/eks/latest/userguide/create-kubeconfig.html) to get the kubeconfig file for the cluster. The region code is the default region provided in the availability zones in variables.tf. Eg. ap-south-1. EKS cluster name also should've been filled in variables.tf.

```
# Run the below command and give the respective region-code and the cluster name
aws eks --region <region-code> update-kubeconfig --name <cluster_name>
```

Verify that you can connect to the cluster by running the following command.

```
kubectl config use-context <cluster_name>

kubectl get nodes -A

kubectl get pods -A
```

Once the deployment is done get the CNAME of the _nginx-ingress-controller:_

```
kubectl get svc ingress-nginx-controller -n backbone -o jsonpath='{.status.loadBalancer.ingress[0].hostname}'
```

The output of this will be the something like this:

&#x20;[ae210873da6ff4c03bde2ad22e18fe04-233d3411.ap-south-1.elb.amazonaws.com](http://ae210873da6ff4c03bde2ad22e18fe04-233d3411.ap-south-1.elb.amazonaws.com/)&#x20;

Add the CNAME to your domain provider against your domain name.

## Cleanup & Uninstallation Of DIGIT Infrastructure

As you wrap up your work with DIGIT, ensuring a smooth and error-free cleanup of the resources is crucial. Regular monitoring of the GitHub Actions workflow's output is essential during the destruction process. Watch out for any error messages or signs of issues. A successful job completion will be confirmed by a success message in the GitHub Actions window, indicating that the infrastructure has been effectively destroyed.

When you're ready to remove DIGIT and clean up the resources it created, proceed with executing the `terraform_infra_destruction` job. This action is designed to dismantle all setup resources, clearing the environment neatly.

We hope your experience with DIGIT was positive and that this guide makes the uninstallation process straightforward.

### How to Run the Terraform Infrastructure Destruction Job

To initiate the destruction of a Terraform-managed infrastructure, follow these steps:

1. Navigate to **Actions**.
2. Click **DIGIT-Install workflow**.
3. Select **Run workflow**.
4. When prompted, type **"destroy"**. This action starts the `terraform_infra_destruction` job.

You can observe the progress of the destruction job in the actions window.

{% hint style="info" %}
**Note:** For DIGIT configurations created using the master branch.
{% endhint %}

<div align="left">

<figure><img src="../../../../.gitbook/assets/Screenshot 2024-03-07 at 11.13.55 AM.png" alt=""><figcaption><p>Destroying the created DIGIT Infrastructure via Terraform</p></figcaption></figure>

</div>

If DIGIT is installed from a branch other than the main one, ensure that the branch name is correctly specified in the workflow file.  For instance, if the installation is done from the **digit-install** branch, the following snippet should be updated to reflect that.

```github-actions-workflow
name: DIGIT-Install workflow
# Workflow branch creating cluster against the input.yaml file  
on:
  push:
    branches:
      - master
      - digit-install
  workflow_dispatch:
    inputs:
      destroyCommand:
        description: 'Type "destroy" to run the terraform_infra_destruction job.'
        required: true
        default: ''  
```

&#x20;
