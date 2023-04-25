---
description: >-
  In this tutorial, we will go through the step by step process of setup
  central-instance infra
---

# Setup Central Instance Infra

## Pre-reads <a href="#pre-reads" id="pre-reads"></a>

* Know about EKS: [https://www.youtube.com/watch?v=SsUnPWp5ilc](https://www.youtube.com/watch?v=SsUnPWp5ilc)
* Know node groups​ [https://docs.aws.amazon.com/eks/latest/userguide/managed-node-groups.html](https://docs.aws.amazon.com/eks/latest/userguide/managed-node-groups.html)
* Know about Taints and Tolerations [https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)
* Know about node-affinity [https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity)
* Know what is terraform: [https://youtu.be/h970ZBgKINg](https://youtu.be/h970ZBgKINg)​

## Pre-requisites <a href="#prerequisites" id="prerequisites"></a>

1. ​[**AWS account**](https://portal.aws.amazon.com/billing/signup?nc2=h\_ct\&src=default\&redirect\_url=https%3A%2F%2Faws.amazon.com%2Fregistration-confirmation#/start) with admin access to provision EKS Service, you can always subscribe to free AWS account to learn the basics and try, but there is a limit to [**what is offered as free**](https://aws.amazon.com/free/), for this demo you need to have a commercial subscription to the EKS service.
2. Install [**terraform**](https://releases.hashicorp.com/terraform/0.14.10/) version (0.14.10) for the Infra-as-code (IaC) to provision cloud resources as code and with desired resource graph and also it helps to destroy the cluster at one go.&#x20;
3. Install [**kubectl**](https://kubernetes.io/docs/tasks/tools/) on your local machine that helps you interact with the kubernetes cluster
4. Install [**Helm**](https://helm.sh/docs/intro/install/) that helps you package the services along with the configurations, envs, secrets, etc into a [**kubernetes manifests**](https://devspace.cloud/docs/cli/deployment/kubernetes-manifests/what-are-manifests)
5. **​**[**Install AWS CLI**](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html) on your local machine so that you can use aws cli commands to provision and manage the cloud resources on your account.
6. Install [**AWS IAM Authenticator**](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html) that helps you authenticate your connection from your local machine so that you should be able to deploy DIGIT services.
7. ​Use the [**AWS IAM User**](https://docs.aws.amazon.com/IAM/latest/UserGuide/id\_users\_create.html) **credentials provided** for the Terraform ([**Infra-as-code**](https://devops.digit.org/devops-general/infra-as-code)) to connect with your AWS account and provision the cloud resources.
   * You'll get a **Secret Access Key** and **Access Key ID**. **Save them safely.**
   *   Open the terminal and run the following command. The AWS CLI is already installed and the credentials are saved. (Provide the credentials and you can leave the region and output format blank).

       ```
       aws configure --profile central-instance-account 

       AWS Access Key ID []:<Your access key>
       AWS Secret Access Key []:<Your secret key>
       Default region name []: ap-south-1
       Default output format []: text
       ```

       The above will create the following file In your machine as /Users/.aws/credentials

       ```
       [mgramseva-infra-account] 
       aws_access_key_id=*********** 
       aws_secret_access_key=****************************
       ```

Before we provision the cloud resources, we need to understand and be sure about what resources need to be provisioned by terraform to deploy DIGIT. The following picture shows the various key components. (EKS, Worker Nodes, Postgress DB, EBS Volumes, Load Balancer)

&#x20;the following is the resources that we are going to provision using terraform in a standard way so that every time and for every environment, it'll have the same infra.

* EKS Control Plane (Kubernetes Master)
* Work node group (VMs with the estimated number of vCPUs, Memory)
* Node-Groups&#x20;
* EBS Volumes (persistent volumes)
* RDS (Postgresql)
* VPCs (private network)
* Users to access, deploy and read-only

## Provisioning of central Instance Infra Using Terraform

1. Fork the DIGIT-DevOps repository into your organization account using the GitHub web portal. Make sure to add the right users to the repository. Clone the forked DIGIT-DevOps repository. Navigate to the `sample-central-instance` directory which contains the sample AWS infra provisioning script.&#x20;

```
git clone --branch release https://github.com/egovernments/DIGIT-DevOps.git

cd DIGIT-DevOps/infra-as-code/terraform/sample-central-instance/remote-state
```

<details>

<summary>main.tf</summary>

```
provider "aws" {
  region = "ap-south-1"
}

resource "aws_s3_bucket" "terraform_state" {
  bucket = "central-instance-test-terraform-state"     // Replce bucket name

  versioning {
    enabled = true
  }

  lifecycle {
    prevent_destroy = true
  }
}

resource "aws_dynamodb_table" "terraform_state_lock" {
  name           = "central-instance-test-terraform-state"   // Replce bucket name
  read_capacity  = 1
  write_capacity = 1
  hash_key       = "LockID"

  attribute {
    name = "LockID"
    type = "S"
  }
}
```

</details>

```
cd DIGIT-DevOps/infra-as-code/terraform/sample-central-instance/
```

<details>

<summary>main.tf</summary>

```
terraform {
  backend "s3" {
    bucket = "central-instance-test-terraform-state"  //Replace bucket name
    key = "terraform"
    region = "ap-south-1"
  }
}

module "network" {
  source             = "../modules/kubernetes/aws/network"
  vpc_cidr_block     = "${var.vpc_cidr_block}"
  cluster_name       = "${var.cluster_name}"
  availability_zones = "${var.network_availability_zones}"
}

module "db" {
  source                        = "../modules/db/aws"
  subnet_ids                    = "${module.network.private_subnets}"
  vpc_security_group_ids        = ["${module.network.rds_db_sg_id}"]
  availability_zone             = "${element(var.availability_zones, 0)}"
  instance_class                = "db.t3.medium"             //Replace DB instance class according to your environments
  engine_version                = "11.15"                
  storage_type                  = "gp2"
  storage_gb                    = "100"              
  backup_retention_days         = "7"
  administrator_login           = "admin"                   
  administrator_login_password  = "${var.db_password}"
  identifier                    = "${var.cluster_name}-db"
  db_name                       = "${var.db_name}"
  environment                   = "${var.cluster_name}"
}


data "aws_eks_cluster" "cluster" {
  name = "${module.eks.cluster_id}"
}

data "aws_eks_cluster_auth" "cluster" {
  name = "${module.eks.cluster_id}"
}
provider "kubernetes" {
  host                   = "${data.aws_eks_cluster.cluster.endpoint}"
  cluster_ca_certificate = "${base64decode(data.aws_eks_cluster.cluster.certificate_authority.0.data)}"
  token                  = "${data.aws_eks_cluster_auth.cluster.token}"
  load_config_file       = false
  version                = "~> 1.11"
}

module "eks" {
  source          = "terraform-aws-modules/eks/aws"
  version         = "17.24.0"
  cluster_name    = "${var.cluster_name}"
  cluster_version = "${var.kubernetes_version}"
  subnets         = "${concat(module.network.private_subnets, module.network.public_subnets)}"

  tags = "${
    map(
      "kubernetes.io/cluster/${var.cluster_name}", "owned",
      "KubernetesCluster", "${var.cluster_name}"
    )
  }"

  vpc_id = "${module.network.vpc_id}"

  worker_groups_launch_template = [
    {
      name                    = "spot"
      subnets                 = "${concat(slice(module.network.private_subnets, 0, length(var.availability_zones)), slice(module.network.public_subnets, 0, length(var.availability_zones)))}"
      override_instance_types = "${var.override_instance_types}"
      asg_max_size            = 1
      asg_desired_capacity    = 1
      kubelet_extra_args      = "--node-labels=node.kubernetes.io/lifecycle=spot"
      spot_allocation_strategy= "capacity-optimized"
      spot_instance_pools     = null
    },
  ]
  
}

module "es-master" {

  source = "../modules/storage/aws"
  storage_count = 3
  environment = "${var.cluster_name}"
  disk_prefix = "es-master"
  availability_zones = "${var.availability_zones}"
  storage_sku = "gp2"
  disk_size_gb = "2"
  
}
module "es-data-v1" {

  source = "../modules/storage/aws"
  storage_count = 3
  environment = "${var.cluster_name}"
  disk_prefix = "es-data-v1"
  availability_zones = "${var.availability_zones}"
  storage_sku = "gp2"
  disk_size_gb = "25"
  
}

module "zookeeper" {

  source = "../modules/storage/aws"
  storage_count = 3
  environment = "${var.cluster_name}"
  disk_prefix = "zookeeper"
  availability_zones = "${var.availability_zones}"
  storage_sku = "gp2"
  disk_size_gb = "2"
  
}

module "kafka" {

  source = "../modules/storage/aws"
  storage_count = 3
  environment = "${var.cluster_name}"
  disk_prefix = "kafka"
  availability_zones = "${var.availability_zones}"
  storage_sku = "gp2"
  disk_size_gb = "50"
  
}

data "aws_security_group" "node_sg" {
 tags = {
    Name = "${var.cluster_name}-eks_worker_sg"
  }
  depends_on = [
   module.eks
  ]
}
  
module "node-group" {  
  for_each = toset(["digit", "urban", "sanitation", "ifix", "mgramseva"])  // Replace/Add node groups
  source = "../modules/node-pool/aws"

  cluster_name        = "${var.cluster_name}"
  node_group_name     = "${each.key}-ng"
  kubernetes_version  = "${var.kubernetes_version}"
  security_groups     =  ["${module.network.worker_nodes_sg_id}", "${data.aws_security_group.node_sg.id}"]
  subnet              = "${concat(slice(module.network.private_subnets, 0, length(var.node_pool_zone)))}"
  node_group_max_size = 1
  node_group_desired_size = 1
  depends_on = [
    module.network,
    module.eks
  ]
}  



```

</details>

<details>

<summary>variables.tf</summary>

```
#
# Variables Configuration
#

variable "cluster_name" {
  description = "Name of the Kubernetes cluster"
  default = "cental-instance-test"  //Replace
}

variable "vpc_cidr_block" {
  default = "192.172.32.0/19"
}

variable "network_availability_zones" {
  description = "Configure availability zones configuration for VPC. Leave as default for India. Recommendation is to have subnets in at least two availability zones"
  default = ["ap-south-1a", "ap-south-1b"]  // Replace if needed 
}

variable "availability_zones" {
  description = "Amazon EKS runs and scales the Kubernetes control plane across multiple AWS Availability Zones to ensure high availability. Specify a comma separated list to have a cluster spanning multiple zones. Note that this will have cost implications"
  default = ["ap-south-1a"]  #REPLACE IF NEEDED
}

variable "node_pool_zone" {
 description = "Should be same as availability_zones"
 default = ["ap-south-1a"] #REPLACE IF NEEDED
}

variable "kubernetes_version" {
  default = "1.20"  #REPLACE IF NEEDED
}

variable "instance_type" {
  default = "m4.xlarge"
}

variable "override_instance_types" {
  default = ["r5a.large", "r5ad.large", "r5d.large", "m4.xlarge"]
  
}

variable "number_of_worker_nodes" {
  default = "1"
}

variable "ssh_key_name" {
  default = "central-instance"
}

variable "db_name" {
  description = "RDS DB name. Make sure there are no hyphens or other special characters in the DB name. Else, DB creation will fail"
  default = "test_db" #REPLACE
}

variable "db_password" {}

```

</details>

```
terraform init
terraform plan
terraform apply
```
