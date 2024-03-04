---
description: >-
  Complete DIGIT installation step-by-step Instructions across various Infra
  types like public & private clouds
---

# Production Setup

#### Topics Covered:

* [Production setup overview](./#basics)
* [List of pre-reads for a better understanding](./#pre-reads)
* [Pre-requisites for setup](./#pre-requisites)
* [Choose your cloud for setup](./#1.-choose-your-cloud)
* [Deployment steps](./#2.-deploy-digit)
* [Post-deployment steps](./#3.-post-deployment-steps)
* [Assess the deployment](./#4.-assessment-of-the-digit-deployment)
* [Destroy the cluster](./#5.-destroy-the-cluster)

## Basics

The [**Quickstart Guide**](../quick-setup/) would have helped you to get your hands dirty and build the Kubernetes cluster on a local/single VM instance - which you can consider for either local development or to understand the details involved in infra and deployment.

However, DIGIT is a [**cloud-native**](https://www.appdynamics.com/topics/what-is-cloud-native-architecture#\~3-challenges) platform and at the same time [**cloud-agnostic**](https://looker.com/definitions/cloud-agnostic)**.** Depending on the scale and performance running **DIGIT on production** requires advanced capabilities like HA, DRS, autoscaling, resiliency, etc. All these capabilities are supported by commercial clouds like **AWS, Google, Azure, VMware, OpenStack, etc..** and also the private clouds like **NIC** and a **few SDCs implemented clouds.** These cloud providers provide the **Kubernetes-as-a-managed-service** that makes the entire infra setup and management seamless and automated, like **infra-as-code, and config-as-code**.

## Pre-reads

* Know the basics of Kubernetes: [https://www.youtube.com/watch?v=PH-2FfFD2PU\&t=3s](https://www.youtube.com/watch?v=PH-2FfFD2PU\&t=3s)
* Know the [basics of kubectl](https://www.tutorialspoint.com/kubernetes/kubernetes\_kubectl\_commands.htm) commands
* Know kubernetes manifests: [https://www.youtube.com/watch?v=ohSUtEfDefc](https://www.youtube.com/watch?v=ohSUtEfDefc)
* Know how to manage env values, secrets of any service deployed in kubernetes [https://www.youtube.com/watch?v=OW244LxB4oI](https://www.youtube.com/watch?v=OW244LxB4oI)
* Know how to port forward to a pod running inside k8s cluster and work locally [https://www.youtube.com/watch?v=TT3nd5n5Yus](https://www.youtube.com/watch?v=TT3nd5n5Yus)
* Know sops to secure your keys/creds: [https://www.youtube.com/watch?v=DWzJ87KbwxA](https://www.youtube.com/watch?v=DWzJ87KbwxA)

## Pre-requisites

* Unlike quickstart, full installation requires state/user-specific configurations ready before proceeding with the deployment.
* You need to have a fully qualified DNS (URL) - (Should not be a dummy)
* Persistent storage depends on the cloud you are using for Kafka, ES, etc.
* Either a standalone or a hosted PostGres DB above v11.x
* Access to MDMS repository for master data like Roles, Access, Actions, tenants, etc. Sample repo view [here](https://github.com/egovernments/egov-mdms-data).
* Access to Configs repository like persister, searcher configs etc. Sample repo view [here](https://github.com/egovernments/configs).
* GeoLocation provider configs (Google Location API), SMS Gateway, Payment Gateway, etc.
* Create a [github user account](https://docs.github.com/en/get-started/signing-up-for-github/signing-up-for-a-new-github-account). This should be different from the repo-forked GitHub organization account. Once a user account is ready, generate the ssh authentication key [generate a new SSH key ](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)and [add it to the above user accou](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)[t](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account).
* [Fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo) both the [mdms](https://github.com/egovernments/egov-mdms-data/tree/UAT), and [config](https://github.com/egovernments/configs/tree/UAT) repos into your GitHub account.
* The newly created user must have access to the MDMS and config forked repo.

## 1. Choose Your Cloud

Choose your cloud and follow the instructions to set up a Kubernetes cluster before moving on to deployment.

{% content-ref url="aws/" %}
[aws](aws/)
{% endcontent-ref %}

{% content-ref url="azure/" %}
[azure](azure/)
{% endcontent-ref %}

{% content-ref url="sdc/" %}
[sdc](sdc/)
{% endcontent-ref %}

## 2. Deploy DIGIT

Post-infra setup (Kubernetes Cluster), the deployment involves 2 stages and 2 modes. Check out the stages first and then the modes. As part of a sample exercise, we will deploy the PGR module. However, deployment steps are similar.  The pre-requisites have to be configured accordingly.

### 2 Stages For Deployment

**Stage 1: Prepare an <**[**env.yaml> master config file**](https://github.com/egovernments/DIGIT-DevOps/blob/master/deploy-as-code/helm/environments/dev.yaml)**, you can provide any name to this file. The file has the following configurations and this env file needs to be in line with your cluster name.**

* each service global, local env variables
* credentials, secrets (You need to encrypt using [sops](https://github.com/mozilla/sops#updatekeys-command) and create a **\<env>-secret.yaml** separately)
* Number of replicas/scale of individual services (Depending on whether dev or prod)
* MDMS, config repos (Master data, ULB, tenant details, users, etc)
* sms g/w, email g/w, payment g/w
* GMap key (In case you are using Google Map services in your PGR, PT, TL, etc)
* S3 Bucket for Filestore
* URL/DNS on which the DIGIT will be exposed
* SSL certificate for the above URL
* End-points configs (Internal/external)

**Stage 2: Run the digit\_setup deployment script and simply answer the questions that it asks.**

```
cd DIGIT-DevOps/deploy-as-code/egov-deployer

go run digit_setup.go

#Be prepared for the following questions
1. Do you have the Kubernetes Setup?
2. Provide the path of the intented env kubeconfig file
3. Which version of the DIGIT that you want to install
4. What DIGIT Modules that you choose to install (Choose PGR)
5. All, done, Now do you want to preview the deployment manifests 
6. Are you good to proceed with the DIGIT Installation

All Done.
```

All done, wait and watch for 10 min, you'll have the DIGIT setup completed and the application will be running on the given URL.

### 2 Modes Of Deployment

Essentially, DIGIT deployment means that we need to generate Kubernetes manifests for each individual service. We use the tool called the helm, which is an easy, effective and customizable packaging and deployment solution. So depending on where and in which env you initiate the deployment there are 2 modes that you can deploy.

1. **From local machine** - whatever we are trying in this sample exercise so far.
2. **Advanced: From CI/CD System like Jenkins** - Depending on how you want to set up your CI/CD and the expertise the steps varies. Find out how we have set up CI/CD on Jenkins and the pipelines are created automatically without any manual intervention [here](broken-reference).

## 3. Post-Deployment Steps

Post-deployment - the application is now accessible from the configured domain.

To try out PGR employee login - Create a sample tenant, city, and user to log in and assign an LME employee role using the seed script.

* [x] Run the [kubectl port-forwarding](https://phoenixnap.com/kb/kubectl-port-forward) of the **egov-user** service from Kubernetes cluster to your localhost. This gives you access to egov-user service directly and you can now interact with the API directly.

```
kubectl port-forward svc/egov-user 8080:8080 -n egov
Forwarding from 127.0.0.1:8080 -> 8080
Forwarding from [::1]:8080 -> 8080
```

* [x] Seed the sample data
* [x] Ensure you have the postman to run the following seed data API. If not, [Install postman](https://www.postman.com/downloads/canary/) on your local machine.
* [x] Import the following postman collection into the postman and run it. This collection has the seed data that enable sample test users and localisation data.
  * [DIGIT Bootstrap](https://raw.githubusercontent.com/egovernments/DIGIT-DevOps/quickstart/deploy-as-code/bootstrap\_scripts/seed\_data.json)

![](<../../../.gitbook/assets/image (155).png>)

![](<../../../.gitbook/assets/image (246).png>)

## 4. Assess DIGIT Deployment

By now we have successfully completed the DIGIT setup on the cloud. Use the URL that you mentioned in your env.yaml Eg: https://mysetup.digit.org and create a grievance to ensure the PGR module deployed is working fine. Refer to the product documentation below for the steps.

**Credentials:**

1. Citizen: You can use your default mobile number (9999999999) to sign in using the default Mobile OTP 123456.
2. Employee: Username: **GRO** and password: **eGov@4321**

{% embed url="https://urban.digit.org/products/modules/public-grievances-and-redressal/pgr-user-manual" %}

Post grievance creation and assignment of the same to LME, capture the screenshot of the same and share it to ensure your setup is working fine.

## 5. Destroy The Cluster

Post validating the PGR functionality share the API response of the following request to assess the correctness of successful DIGIT PGR Deployment.

Finally, clean up the DIGIT setup if you wish, using the following command. This will delete the entire cluster and other cloud resources that were provisioned for the DIGIT setup.

To destroy previously-created infrastructure with Terraform, run the command below:

1. ELB is not deployed via Terraform. ELB has created at deployment time by the setup of Kubernetes Ingress. This has to be deleted manually by deleting the ingress service.&#x20;
   1. `kubectl delete deployment nginx-ingress-controller -n <namespace>`
   2.  `kubectl delete svc nginx-ingress-controller -n <namespace>`

       **Note**: Namespace can be one of egov or jenkins.
2. Delete S3 buckets manually from the AWS console and also verify if ELB got deleted.
   1. In case of if ELB is not deleted, you need to delete ELB from [AWS console](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-delete.html).
3. Run `terraform destroy`.

```
cd DIGIT-DevOps/infra-as-code/terraform/my-digit-eks
terraform destroy
```

## Conclusion

All done, we have successfully created infra on the cloud, deployed DIGIT, bootstrapped DIGIT, performed a transaction on PGR and finally destroyed the cluster.

