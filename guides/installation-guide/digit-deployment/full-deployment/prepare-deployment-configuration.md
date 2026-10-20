---
description: Steps to prepare the deployment configuration file
---

# Prepare Deployment Configuration

#### Topics covered:

* [Pre-reads for preparing the deployment configuration file](prepare-deployment-configuration.md#pre-reads)
* [Steps to prepare the configuration file](prepare-deployment-configuration.md#steps-to-prepare-deployment-configuration-file)

## Overview

It's important to prepare a global deployment configuration yaml file that contains all necessary user-specific custom values like URL, gateways, persistent storage ids, DB details etc.

## Pre-reads

* Know the basics of Kubernetes: [https://www.youtube.com/watch?v=PH-2FfFD2PU\&t=3s](https://www.youtube.com/watch?v=PH-2FfFD2PU\&t=3s)
* Know the [basics of kubectl](https://www.tutorialspoint.com/kubernetes/kubernetes_kubectl_commands.htm) commands
* Know kubernetes manifests: [https://www.youtube.com/watch?v=ohSUtEfDefc](https://www.youtube.com/watch?v=ohSUtEfDefc)
* Know how to manage env values, secrets of any service deployed in kubernetes [https://www.youtube.com/watch?v=OW244LxB4oI](https://www.youtube.com/watch?v=OW244LxB4oI)
* Know how to port forward to a pod running inside k8s cluster and work locally [https://www.youtube.com/watch?v=TT3nd5n5Yus](https://www.youtube.com/watch?v=TT3nd5n5Yus)
* Know sops to secure your keys/creds: [https://www.youtube.com/watch?v=DWzJ87KbwxA](https://www.youtube.com/watch?v=DWzJ87KbwxA)

Post-Kubernetes Cluster setup, the deployment consists of 2 stages. As part of this sample exercise, we can deploy PGR and show the required configurations. The deployment steps are similar for all other modules except that the prerequisites differ depending on required features like SMS Gateway, Payment Gateway, etc.

## Steps To Prepare Deployment Configuration File

Navigate to the following file in your local machine from the previously cloned DevOps git repository.

{% embed url="https://github.com/egovernments/DIGIT-DevOps/blob/kubernetes-1.35/deploy-as-code/helm/environments/egov-demo.yaml" %}

{% embed url="https://github.com/egovernments/DIGIT-DevOps/blob/kubernetes-1.35/deploy-as-code/helm/environments/egov-demo-secrets.yaml" %}

**Step 1:** Clone the following [DIGIT-DevOps](https://github.com/egovernments/DIGIT-DevOps) repo (If not already done as part of Infra setup), you may need to [install git](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository-from-github/cloning-a-repository) and then run [git clone](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository-from-github/cloning-a-repository) it to your machine.

`$ git clone -b kubernetes-1.35 https://github.com/egovernments/DIGIT-DevOps`

**Step 2:** After cloning the repo CD to the DIGIT-DevOps folder, type the "code" command to open the visual editor and open all the files from the DIGIT-DevOps repo.

```
$ cd DIGIT-DevOps
$ code 
```

**Step 3:** Update the deployment config file with your details, you can use the following template [egov-demo-sample](https://github.com/egovernments/DIGIT-DevOps/blob/kubernetes-1.35/deploy-as-code/helm/environments/egov-demo.yaml).

* ```
  $ vi deploy-as-code/helm/environments/egov-demo.yaml
  ```
* Replace the following as per the applicable values -
  * **Important:** Add your domain name [here](https://github.com/egovernments/DIGIT-DevOps/blob/kubernetes-1.35/deploy-as-code/helm/environments/egov-demo.yaml#L2), which you want to use for accessing DIGIT. ( Do not use the dummy domain )
  * SMS gateway to receive OTP, transaction mobile notification, etc.
  * MDMS, Config repo URL, here is where you provide master data, tenants and various user/role access details.
  * GMap key for the location service
  * Payment gateway, in case you use PT, TL, etc

**Step 4:** Update your credentials and sensitive data in the secret file as per your details.

1. ```
   $ vi deploy-as-code/helm/environments/egov-demo-secrets.yaml
   ```
2. credentials, secrets (You need to encrypt using [sops](https://github.com/mozilla/sops#updatekeys-command) and create a [**\<env>-secret.yaml** ](https://github.com/egovernments/DIGIT-DevOps/blob/kubernetes-1.35/deploy-as-code/helm/environments/egov-demo-secrets.yaml)separately)
3. SOPS expects an encryption key to encrypt/decrypt a specified plain text and keep the details secured. The following are the options to generate the encryption key -
   * Option 1: Generate PGP keys [https://fedingo.com/how-to-generate-pgp-key-in-ubuntu](https://fedingo.com/how-to-generate-pgp-key-in-ubuntu/)
   * Option 2: [Create AWS KMS keys](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html) when you want to use the AWS cloud provider.
4. Once you generate your encryption key, create a **.sops.yaml** configuration file under the **/helm** directory of the cloned repo to define the keys used for specific files. Refer to the SOP [doc](https://github.com/mozilla/sops#211using-sopsyaml-conf-to-select-kmspgp-for-new-files) for more details.

**Note**: For demo purposes, you can use the [egov-demo-secrets.yaml](https://github.com/egovernments/DIGIT-DevOps/blob/kubernetes-1.35/deploy-as-code/helm/environments/egov-demo-secrets.yaml) as it is without sops configuration, but make sure you update your specific details like Git SSH, URL etc. When you decide to push these configurations into any git or public space, make sure you follow the sops configuration mentioned in this article [sops](https://github.com/mozilla/sops#updatekeys-command) to encrypt your secrets.

**Step 5: Important:** Fork the following repos that contain the master data and default configs which you would customize as per your specific implementation later. Like (Master Data, ULB, Tenant details, Users, etc) to your respective GitHub organization account.

1. ​[fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo) both the [mdms](https://github.com/egovernments/egov-mdms-data/tree/UAT), and [config](https://github.com/egovernments/configs/tree/UAT) repos into your GitHub organization account
2. Once you fork the repos into your GitHub organization account, Create a [github user account](https://docs.github.com/en/get-started/signing-up-for-github/signing-up-for-a-new-github-account), generate an SSH authentication key [generate new SSH key ](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)and [add it to above user account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account).
3. New GitHub users should be enabled to access the earlier forked repos.
4. Add the ssh private key that you generated in the previous step to [egov-demo-secrets.yaml ](https://github.com/egovernments/DIGIT-DevOps/blob/kubernetes-1.35/deploy-as-code/helm/environments/egov-demo-secrets.yaml#L45)under the git-sync section.
5. Modify the services git-Sync repo and branch with your fork repo and branch in [egov-demo.yaml](https://github.com/egovernments/DIGIT-DevOps/blob/kubernetes-1.35/deploy-as-code/helm/environments/egov-demo.yaml#L294-L398).​

```
vi deploy-as-code/helm/environments/egov-demo-secrets.yaml
```

**Step 6:** Update the deployment configs for the below as per your specification:

1. Number of replicas/scale of each service (depending on whether dev or prod load).
2. Update the SMS Gateway, Email Gateway, and Payment Gateway details for the notification and payment gateway services, etc.
3. Update the config, MDMS GitHub repos wherever marked
4. Update GMap key (In case you are using Google Map services in your PGR, PT, TL, etc)
5. Create one private S3 bucket for Filestore and one public bucket for logos. Add the bucket details respectively and create an IAM user with the s3 bucket access. Add IAM user details to [\<env-secrets.yaml>](https://github.com/egovernments/DIGIT-DevOps/blob/kubernetes-1.35/deploy-as-code/helm/environments/egov-demo-secrets.yaml).
6. URL/DNS on which the DIGIT will be exposed.
7. SSL certificate for the above URL.
8. Any specific endpoint configs (Internal/external).

```
$ vi deploy-as-code/helm/environments/egov-demo.yaml

```
