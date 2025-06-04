# GCP - Provision Infrastructure

## Overview

There are several ways to deploy the solution to the cloud. In this case, we will use Terraform Infra-as-code.

Terraform is an open-source infrastructure as code ([IaC](https://www.techtarget.com/searchitoperations/definition/Infrastructure-as-Code-IAC)) software tool that allows DevOps engineers to programmatically provision the physical resources an application requires to run.

Infrastructure as code is an IT practice that manages an application's underlying IT infrastructure through programming. This approach to resource allocation allows developers to logically manage, monitor and provision resources -- as opposed to requiring that an operations team manually configure each required resource.

Terraform users define and [enforce infrastructure configurations](https://www.techtarget.com/searchcloudcomputing/tip/How-to-deploy-Terraform-code-in-an-Azure-DevOps-pipeline) by using a JSON-like configuration language called HCL (HashiCorp Configuration Language). HCL's simple syntax makes it easy for DevOps teams to provision and re-provision infrastructure across multiple clouds and on-premises data centres.

### Cloud Resources Required <a href="#cloud-resources-required" id="cloud-resources-required"></a>

Before we provision the cloud resources, we need to understand and be sure about what resources need to be provisioned by Terraform to deploy DIGIT. The following picture shows the various key components (VPC, GKE, Node Pools, Postgres DB, Volumes, Load Balancer).

<figure><img src="../../../../.gitbook/assets/image (343).png" alt=""><figcaption></figcaption></figure>

### Understand Terraform Script <a href="#understand-terraform-script" id="understand-terraform-script"></a>

* Ideally, one would write the Terraform script from scratch using this [doc](https://learn.hashicorp.com/collections/terraform/modules).
* Here we have already written the Terraform script that one can reuse/leverage that provisions the production-grade DIGIT Infra and can be customised with the user-specific configuration.

## Deployment Steps <a href="#deployment-steps" id="deployment-steps"></a>

1. Clone the following [DIGIT-DevOps](https://github.com/egovernments/DIGIT-DevOps), where we have all the sample Terraform scripts available for you to leverage.

{% code lineNumbers="true" %}
```
git clone https://github.com/egovernments/DIGIT-DevOps.git
cd DIGIT-DevOps
git checkout kubernetes-1.31
code .
cd infra-as-code/terraform/sample-gcp

### You'll see the following file structure 

├── sample-gcp
│       ├── remote-state
│       │      ├── main.tf
│       │      └── variables.tf
│       ├── main.tf
│       ├── outputs.tf
│       └── variables.tf
└── modules
     ├── db
     │    └── gcp
     │         ├── main.tf
     │         ├── outputs.tf
     │         └── variables.tf
     │── kubernetes
     │    └── gcp
     │         ├── main.tf
     │         ├── outputs.tf
     |         └── variables.tf
     │── network
     │    └── gcp
     │         ├── main.tf
     │         ├── outputs.tf
     |         └── variables.tf
     └── storage
    	  └── gcp
               ├── main.tf
     	       ├── outputs.tf
     	       └── variables.tf
```
{% endcode %}

2. Declare the variables in [remote-state/variables.tf](https://github.com/egovernments/DIGIT-DevOps/blob/kubernetes-1.31/infra-as-code/terraform/sample-gcp/remote-state/variables.tf) for GCP storage to maintain assets & terraform remote state.

{% code lineNumbers="true" %}
```
variable "project_id" {
  default     = "<GCP_PROJECT_ID>"
  description = "GCP project to create the bucket in"
}

variable "region" {
  default     = "<GCP_REGION>"
  description = "GCP region for the bucket"
}

variable "bucket_name" {
  default     = "<terraform_state_bucket_name>"
  description = "Name of the GCS bucket to store Terraform state"
}

```
{% endcode %}

3. Update bucket-name in [main.tf](https://github.com/egovernments/DIGIT-DevOps/blob/kubernetes-1.31/infra-as-code/terraform/sample-gcp/main.tf), to initialize backend.

{% code lineNumbers="true" %}
```
terraform {
  backend "gcs" {
    bucket = "<terraform_state_bucket_name>"  # Replace with the name after creating remote state bucket
    prefix  = "terraform/state"
  }
```
{% endcode %}

4. Declare the variables in [variables.tf](https://github.com/egovernments/DIGIT-DevOps/blob/kubernetes-1.31/infra-as-code/terraform/sample-gcp/variables.tf)

{% code lineNumbers="true" %}
```
variable "project_id" {
  default     = "<GCP_PROJECT_ID>"
  description = "Name of the GCp Project"
}
variable "region" {
  default     = "<GCP_REGION>"
}
variable "zone" {
  default = "<GCP_AVAILABILITY_ZONE>"
}
variable "env_name" {
  default     = "<ENVIRONMENT_NAME>"
  description = "Name of the env"
}
variable "private_subnet_cidr" {
  default     = "10.10.0.0/24"
  description = "cidr_range for private subnet"
}
variable "public_subnet_cidr" {
  default     = "10.10.64.0/19"
  description = "cidr_range for public subnet"
}
variable "gke_version" {
  default = "1.31.7-gke.1265000"
}
variable "node_machine_type" {
  default = "n2d-highmem-2"            # Allocate as per quota available
}
variable "desired_node_count" {
  default = "3"                        # Allocate as per quota available
}
variable "min_node_count" {
  default = "3"                        # Allocate as per quota available
}
variable "max_node_count" {
  default = "4"                        # Allocate as per quota available
}
variable "node_disk_size_gb" {
  default = "50"
}
variable "db_name" {
  default = "<DATABASE_NAME>"          # avoid using hypen 
}                                      # or any speacial characters
variable "db_username" {
  default = "<DATABASE_USERNAME>"
}
variable "db_password" {}
variable "db_cpu" {
  default = 2
}
variable "db_memory_mb" {
  default = 4096                       # must be a multiple of 256MiB
}
variable "db_disk_size_gb" {
  default = "25"
}
variable "db_max_connections" {
  default = "100"
}
variable "force_peering_cleanup" {
  default = false
}
```
{% endcode %}

Save the files and exit the editor.

### Terraform Execution: Infrastructure Resources Provisioning <a href="#terraform-execution-infrastructure-resources-provisioning" id="terraform-execution-infrastructure-resources-provisioning"></a>

Once you have finished declaring the resources, you can deploy all resources.

<figure><img src="../../../../.gitbook/assets/image (344).png" alt=""><figcaption></figcaption></figure>

1. `terraform init`: command is used to initialise a working directory containing Terraform configuration files.
2. `terraform plan`: command creates an execution plan, which lets you preview the changes that Terraform plans to make to your infrastructure.
3. `terraform apply`: command executes the actions proposed in a Terraform plan to create or update infrastructure.

After the complete creation, you can see resources in your Azure account.

Now we know what the terraform script does, the resources graph that it provisions and what custom values should be given with respect to your environment. The next step is to begin to run the Terraform scripts to provision the infrastructure required to deploy DIGIT on Azure.

Use the CD command to move into the following directory, run the following commands 1-by-1 and watch the output closely.

{% code lineNumbers="true" %}
```
cd DIGIT-DevOps/infra-as-code/terraform/sample-gcp/remote-state

terraform init

terraform plan

terraform apply 

cd ..

terraform init

terraform plan

terraform apply

```
{% endcode %}

### **Test Kubernetes Cluster** <a href="#test-kubernetes-cluster" id="test-kubernetes-cluster"></a>

The Kubernetes tools can be used to verify the newly created cluster.

1. Once the **Terraform Apply** execution is complete, use the following command to get the kubeconfig. It will store your kubeconfig in the .kube/\<file-name> folder.

{% code lineNumbers="true" %}
```
export KUBECONFIG=~/.kube/<file-name>    # provide new filename to store kubeconfig
gcloud container clusters get-credentials <ENVIRONMENT_NAME> --region <GCP_REGION> --project <GCP_PROJECT_ID> 
```
{% endcode %}

2. Verify the health of the cluster.\
   &#xNAN;_**Note:**_ The details of the worker nodes should reflect the status as Ready for All.

{% code lineNumbers="true" %}
```
kubectl get nodes
```
{% endcode %}

3. Update below output received post terraform apply in the [environment](https://github.com/egovernments/DIGIT-DevOps/tree/gcp-support/deploy-as-code/charts/environments) configuration

{% code lineNumbers="true" %}
```
db_instance_private_ip        # env.yaml
db_name                       # env.yaml
db_username                   # env-secrets.yaml
db_password                   # env-secrets.yaml
sops_key                      # .sops.yaml (for encryption/decryption of secrets)
```
{% endcode %}

4. Sample [sops](https://github.com/egovernments/DIGIT-DevOps/blob/gcp-support/deploy-as-code/charts/.sops.yaml) configuration

{% code lineNumbers="true" %}
```
# creation rules are evaluated sequentially; the first match wins
creation_rules:
        # upon creation of a file that matches the pattern *dev.yaml,
        # KMS set A is used
        # eGOV Internal ------------------------------------------------------------------------------------------------------------- #
        - path_regex: environments/egov\-demo\-secrets\.yaml$
          gcp_kms: 'projects/mcs-gcp-test-2/locations/asia-south1/keyRings/gcp-test-sops-keyring/cryptoKeys/gcp-test-sops-key'
```
{% endcode %}

{% hint style="info" %}
_**Note:**_ Refer to the[ DIGIT deployment ](../../digit-deployment/full-deployment-beta/)documentation to deploy DIGIT services.
{% endhint %}

