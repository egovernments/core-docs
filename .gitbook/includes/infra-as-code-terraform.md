---
title: Infra-as-code(terraform)
---

# Overview

Terraform is an open-source infrastructure as code ([IaC](https://www.techtarget.com/searchitoperations/definition/Infrastructure-as-Code-IAC)) software tool that allows DevOps engineers to programmatically provision the physical resources an application requires to run.

Infrastructure as code is an IT practice that manages an application's underlying IT infrastructure through programming. This approach to resource allocation allows developers to logically manage, monitor and provision resources -- as opposed to requiring that an operations team manually configure each required resource.

Terraform users define and [enforce infrastructure configurations](https://www.techtarget.com/searchcloudcomputing/tip/How-to-deploy-Terraform-code-in-an-Azure-DevOps-pipeline) by using a JSON-like configuration language called HCL (HashiCorp Configuration Language). HCL's simple syntax makes it easy for DevOps teams to provision and re-provision infrastructure across multiple clouds and on-premises data centres.

# Cloud Resources Required

Before we provision the cloud resources, we need to understand and be sure about what resources need to be provisioned by Terraform to deploy DIGIT. The following picture shows the various key components. (AKS, Node Pools, Postgres DB, Volumes, Load Balancer)

<div align="left"><img src="../assets/image (175).png" alt=""></div>

# Understand Terraform Script <a href="#set-up-and-initialize-your-terraform-workspace" id="set-up-and-initialize-your-terraform-workspace"></a>

* Ideally, one would write the terraform script from scratch using this [doc](https://learn.hashicorp.com/collections/terraform/modules).
* Here we have already written the terraform script that one can reuse/leverage that provisions the production-grade DIGIT Infra and can be customized with the user-specific configuration.

# Deployment Steps

1. Clone the following [DIGIT-DevOps](https://github.com/egovernments/DIGIT-DevOps) where we have all the sample terraform scripts available for you to leverage.

{% code lineNumbers="true" %}
```
git clone https://github.com/egovernments/DIGIT-DevOps.git
cd DIGIT-DevOps
git checkout kubernetes-1.34
code .
cd infra-as-code/terraform/azure

### You'll see the following file structure 

├── azure
│       ├── main.tf
│       ├── outputs.tf
│       ├── providers.tf
│       ├── remote-state
│       │            └── main.tf
│       └── variables.tf
└── modules
     ├── db
     │    ├── aws
     │    |    ├── main.tf
     │    │    ├── outputs.tf
     │    |    └── variables.tf
     │    └── azure
     │         ├── main.tf
     │         └── variables.tf
     │── kubernetes
     │    └── azure
     │         │   	
     │         ├── main.tf
     │         ├── outputs.tf
     |         └── variables.tf       
```
{% endcode %}

2\. Change the [input.yaml](https://github.com/egovernments/DIGIT-DevOps/blob/kubernetes-1.34/infra-as-code/terraform/azure/input.yaml) according to your specifications.

Save the file and exit the editor.

# Terraform Execution: Infrastructure Resources Provisioning

Once you have finished declaring the resources, you can deploy all resources.

<figure><img src="../assets/image (345).png" alt=""><figcaption></figcaption></figure>

1. `terraform init`: command is used to initialise a working directory containing Terraform configuration files.
2. `terraform plan`: command creates an execution plan, which lets you preview the changes that Terraform plans to make to your infrastructure.
3. `terraform apply`: command executes the actions proposed in a Terraform plan to create or update infrastructure.

After the complete creation, you can see resources in your Azure account.

Now we know what the terraform script does, the resources graph that it provisions and what custom values should be given with respect to your environment.\
\
The next step is to begin to run the Terraform scripts to provision the infrastructure required to deploy DIGIT on Azure.

1. Use the CD command to move into the following directory, run the following commands 1-by-1 and watch the output closely.

{% code lineNumbers="true" %}
```
##### Create the DIGIT Infra #####

az login
##### using above command you can get subscription id and tenant id

az ad sp create-for-rbac --name <sp_name> \
             --role owner \
             --scopes /subscriptions/<subscription_id>
##### Using above command you are creating client-id and client-secret

export ARM_SUBSCRIPTION_ID=<AZURE_SUBSCRIPTION_ID> ## update azure account subscription ID

#### DIGIT-DevOps/infra-as-code/terraform/azure (working directory)

cd DIGIT-DevOps/infra-as-code/terraform/azure

go run ../scripts/init.go

cd remote-state

terraform init

terraform plan

terraform apply 

cd ..

terraform init

terraform plan

terraform apply
```
{% endcode %}

# **Test Kubernetes Cluster**

The Kubernetes tools can be used to verify the newly created cluster.

1. Once the **Terraform Apply** execution is complete, it generates the Kubernetes configuration file or you can get it from Terraform state.
2. Use the below command to get kubeconfig. It will automatically store your kubeconfig in .kube folder.

```
az aks get-credentials --resource-group <resource_group_name> --name <cluster_name>
```

`3.` Verify the health of the cluster.

```
kubectl get nodes 
```

The details of the worker nodes should reflect the status as Ready for All.\
\
<mark style="color:orange;">**Note:**</mark> Refer to the[ DIGIT deployment ](https://docs.digit.org/platform/guides/installation-guide/digit-deployment)documentation to deploy DIGIT services.
