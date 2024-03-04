---
description: DIGIT Automation on AWS
---

# DIGIT Installation on AWS

## **Pre-requisites** <a href="#id-1.-pre-requisites" id="id-1.-pre-requisites"></a>

Following are the pre-requisites and installation steps for setting up DIGIT on AWS:

1. **Install** [**Golang**](https://go.dev/doc/install#download):
   * For Linux: Follow the [instructions here](https://go.dev/doc/install#download) to install Golang on Linux.
   * For Windows: Download the installer using the [link here](https://go.dev/doc/install#download) and follow the installation instructions.
   * For Mac: Download the installer using the [link here](https://go.dev/doc/install#download) and follow the installation instructions.
2. **Install** [**Helm**](https://helm.sh/docs/intro/install/) **- DIGIT services are packaged with Helm Charts**
3. **Install** [**kubectl**](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) **-** CLI to connect to the Kubernetes cluster on your machine
4. **Install** [**cURL**](https://help.ubidots.com/en/articles/2165289-learn-how-to-install-run-curl-on-windows-macosx-linux) **-** for making API calls
5. **Install** [**Visual Studio Code**](https://code.visualstudio.com/download) **-** for better code visualization/editing capabilities
6. **Install** [**Postman**](https://www.postman.com/downloads/) **-** to run digit bootstrap scripts
7. **Install** [**Terraform**](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli) **-** to provide infrastructure on AWS
8. **Install** [**AWS CLI**](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) **and** [**IAM Authenticator**](https://docs.aws.amazon.com/eks/latest/userguide/what-is-eks.html)&#x20;

Once you have installed all these pre-requisites, you are ready to set up DIGIT and its services.

## Deployment&#x20;

To provision infrastructure and set up DIGIT, follow the steps below:

1.  Clone the DIGIT-DevOps repository:

    `git clone` [`https://github.com/egovernments/DIGIT-DevOps.git`](https://github.com/egovernments/DIGIT-DevOps.git)
2.  Navigate to the cloned repository and checkout the release-1.27-kubernetes branch:

    `cd DIGIT-DevOps git checkout release-1.27-kubernetes`
3.  Check if correct credentials are configured using the command:

    `aws configure list`

    _<mark style="color:blue;">Make sure that the above command reflects the set AWS credentials. Proceed once the details are confirmed. (Refer to the AWS document in case of any doubts on how to set the credentials:</mark>_ [<img src="https://docs.aws.amazon.com/assets/images/favicon.ico" alt="" data-size="line">_<mark style="color:blue;">Configuring the AWS CLI - AWS Command Line Interface</mark>_](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html) _<mark style="color:blue;">)</mark>_
4.  Generate ssh key pairs using either method (a) or method (b).\
    a. Using online website (not recommended in production setup. To be only used for demo setups): [https://8gwifi.org/sshfunctions.jsp](https://8gwifi.org/sshfunctions.jsp)

    b. Using openssl :

    `openssl genpkey -algorithm RSA -out private_key.pem openssl rsa -pubout -in private_key.pem -out public_key.pem`
5. Add the public key to your github account - (reference: [https://www.youtube.com/watch?v=9C7\_jBn9XJ0\&ab\_channel=AOSNote](https://www.youtube.com/watch?v=9C7\_jBn9XJ0\&ab\_channel=AOSNote) )
6.  Open input.yaml file in vscode. You can use the below code to directly open it in VS code:

    `code infra-as-code/terraform/sample-aws/input.yaml`

    _If the command does not work you can manually go and open the file in VS code. Once the file is open, fill the inputs. (In case you are not using vscode, you can open it any editor of your choice)_
7. Fill in the inputs as per the regex mentioned in the comments.&#x20;
8.  Open egov-demo-secret.yaml and add DB password (line number 5), flywayPassword (line number 7) and private key.&#x20;

    `code config-as-code/environments/egov-demo-secrets.yaml`

    _Make sure the DB password and flywayPassword are same. Private key has to be added inside git-sync key against ssh key (line number 37)._
9.  Go to _infra-as-code/terraform/sample-aws_ and run _init.go_ script to enrich different files based on _input.yaml_.&#x20;

    `cd infra-as-code/terraform/sample-aws go run ../scripts/init.go`
10. Navigate to the _remote-state_ folder and run terraform to create a S3 bucket and DynamoDB.

    `cd remote-state`\
    `terraform init` \
    `terraform plan` \
    `terraform apply`
11. Navigate back to sample-aws folder and run terraform to provision infrastructure for DIGIT.&#x20;

    `cd ..` \
    `terraform init` \
    `terraform plan` \
    `terraform apply`

    _(Add the same DB password which you have added in egov-demo-secret.yaml when prompted after running terraform apply)_
12. Execute the following command to generate a kubeConfig file and update the volumeIds, DB URL, and other relevant details in the egov-demo.yaml file.

    `terraform output -json | go run ../scripts/envYAMLUpdater.go`
13. Run the export KUBECONFIG command shown on terminal. _(Note: The exact command to run will be printed on terminal. It will be something like this: export KUBECONFIG=\<LOCAL\_KUBECONFIGPATH> )_
14. Run the digit-installer.go script to install DIGIT using the following command:

    `cd ../../../deploy-as-code/deployer go run digit_installer.go`
15. Once the deployment is done get the CNAME of the _nginx-ingress-controller:_

    `kubectl get svc nginx-ingress-controller -n egov -o jsonpath='{.status.loadBalancer.ingress[0].hostname}'`

    The output of this will be the something like this:\
    [ae210873da6ff4c03bde2ad22e18fe04-233d3411.ap-south-1.elb.amazonaws.com](http://ae210873da6ff4c03bde2ad22e18fe04-233d3411.ap-south-1.elb.amazonaws.com/)\
    Add the CNAME to your domain provider against your domain name.

### Seed Data Setup <a href="#seed-data-setup" id="seed-data-setup"></a>

Follow the steps below to set up seed data:

1. Import the provided [postman collection](https://api.postman.com/collections/12892142-55ebe4d0-3869-4879-87e1-5ba3b60cc6b7?access\_key=PMAT-01H27R18VPWXP2AE8812P0S12X).
2.  Port-forward user pod using the following command -

    `kubectl port-forward <egov_user_pod> 8080:8080 -n egov`
3. Hit super\_user\_creation cURL. This will create a super user with username as GRO and password as eGov@4321.
4. Open the accessToken\_generation cURL. The credentials have already been populated. Change "_\{{YOUR\_DOMAIN\_NAME\}}_" placeholder to the domain name defined in _input.yaml_ file while provisioning and hit the cURL.
5. In the response, you will get "_access\_token_" field. Highlight this value, right click on it and set it as global "_token_ "value.
6. Execute rainmaker common, rainmaker locality, rainmaker PGR localization and PGR workflow cURLs by changing "_\{{YOUR\_DOMAIN\_NAME\}}_" placeholder to the domain name defined in input.yaml file to setup localization and workflow seed data.&#x20;

### Destroying The Cluster <a href="#destroying-the-cluster" id="destroying-the-cluster"></a>

Follow the steps below to destroy the cluster once the demo is done:

1. Delete the nginx-ingress-controller service in the `egov` namespace using the below command and navigate to the `infra-as-code/terraform/sample-aws` directory: `kubectl delete svc nginx-ingress-controller -n egov cd ../../infra-as-code/terraform/sample-aws terraform destroy` Run the Terraform destroy command to delete the cluster.
2.  To destroy the remote state bucket, first set the lifecycle value to false in the `main.tf` file in the `remote-state` folder:

    `lifecycle { prevent_destroy = false }`
3. After making this change, go to the AWS console and empty the S3 bucket associated with the remote state.
4. Once the bucket is emptied, you can proceed to destroy the remote state bucket using the Terraform destroy command.
