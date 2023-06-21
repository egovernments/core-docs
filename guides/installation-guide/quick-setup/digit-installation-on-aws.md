---
description: DIGIT Automation on AWS
---

# DIGIT Installation on AWS

### **Pre-requisites** <a href="#1.-pre-requisites" id="1.-pre-requisites"></a>

1. Install [golang](https://golang.org/doc/install#download)  Use these links to install- [Linux](https://golang.org/dl/go1.13.3.linux-amd64.tar.gz) or [Windows](https://golang.org/dl/go1.13.3.windows-amd64.msi) or [Mac](https://golang.org/dl/go1.13.3.darwin-amd64.pkg)​
2. All DIGIT services are packaged using helm charts, Install helm using the link[![](https://helm.sh/img/favicon-152.png)Installing Helm](https://helm.sh/docs/intro/install/)​
3. ​[kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) is a CLI to connect to the Kubernetes cluster on your machine
4. Install [CURL](https://help.ubidots.com/en/articles/2165289-learn-how-to-install-run-curl-on-windows-macosx-linux) for making API calls
5. ​[Install Visualstudio](https://code.visualstudio.com/download) IDE Code for better code visualization/editing capabilities
6. ​[Install Postman](https://www.postman.com/downloads/) to run digit bootstrap scripts
7. Install [Terraform](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli) to provide infrastructure on AWS
8. Install [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) and [IAM Authenticator](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html)

### Deployment&#x20;

To provision infra and setup DIGIT, follow the below mentioned steps:

1.  Clone the DIGIT-DevOps repository using the below command:

    `git clone` [`https://github.com/egovernments/DIGIT-DevOps.git`](https://github.com/egovernments/DIGIT-DevOps.git)

    &#x20;
2.  Once you clone the repository, _cd_ into DIGIT-DevOps and then checkout DIGIT_-Bootcamp_ branch using the command:

    `cd DIGIT-DevOps git checkout DIGIT-Bootcamp`

    \
    At this step please check if correct credentials are configured using the command:

    `aws configure list`

    Please make sure that the above command shows the proper AWS credentials which you have set. Please proceed only after confirming it.\
    _(Refer to this AWS document in case of any doubts on how to set the credentials:_ [![](https://docs.aws.amazon.com/assets/images/favicon.ico)Configuring the AWS CLI - AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html) _)_\
    \

3.  Generate ssh key pairs (Use either method (a) or method (b)).\
    a. Using online website (not recommended in prod setup. To be only used for demo setups):\
    &#x20; [https://8gwifi.org/sshfunctions.jsp](https://8gwifi.org/sshfunctions.jsp)

    b. Using openssl :

    `openssl genpkey -algorithm RSA -out private_key.pem openssl rsa -pubout -in private_key.pem -out public_key.pem`

    &#x20;
4. Add the public key to your github account (reference: [https://www.youtube.com/watch?v=9C7\_jBn9XJ0\&ab\_channel=AOSNote](https://www.youtube.com/watch?v=9C7\_jBn9XJ0\&ab\_channel=AOSNote) )\
   \

5.  Open input.yaml file in vscode. You can use the below code to directly open it in VS code:

    `code infra-as-code/terraform/sample-aws/input.yaml`

    If the command does not work you can manually go and open the file in VS code. Once the file is open, fill the inputs. Please make sure the inputs that you add follow the regex mentioned in the comments for that input

    _(In case you are not using vscode, you can open it any editor of your choice)_

    &#x20;
6.  Open egov-demo-secret.yaml and add DB password (line number 5), flywayPassword (line number 7) and private key. You can use the following command to open it in VS code:

    `code config-as-code/environments/egov-demo-secrets.yaml`

    Please keep the DB password and flywayPassword same. Private key has to be added inside git-sync key against ssh key (line number 37).

    &#x20;
7.  Next go to _infra-as-code/terraform/sample-aws_ and run _init.go_ script to enrich different files based on _input.yaml_. You can run the script using the following command:

    `cd infra-as-code/terraform/sample-aws go run ../scripts/init.go`

    &#x20;
8.  Now go to _remote-state_ folder and run terraform using the following commands. It will create a S3 bucket and DynamoDB to maintain terraform state.

    `cd remote-state`\
    `terraform init` \
    `terraform plan` \
    `terraform apply`
9.  Next cd back to sample-aws folder and run terraform to provision infra for DIGIT. Use the following command:

    `cd ..` \
    `terraform init` \
    `terraform plan` \
    `terraform apply`

    _(Add the same DB password which you have added in egov-demo-secret.yaml when prompted after running terraform apply)_\
    \

10. Execute the following command to generate a kubeConfig file and update the volumeIds, DB URL, and other relevant details in the egov-demo.yaml file.

    `terraform output -json | go run ../scripts/envYAMLUpdater.go`

    &#x20;
11. Run the export KUBECONFIG command shown on terminal. _(Note: The exact command to run will be printed on terminal. It will be something like this: export KUBECONFIG=\<LOCAL\_KUBECONFIGPATH> )_

    &#x20;
12. Next step is deployment of services. Run the digit-installer.go script to install UPYOG using the following command:

    `cd ../../../deploy-as-code/deployer go run digit_installer.go`

    &#x20;
13. Once this is done you will get the CNAME of the _nginx-ingress-controller_ using the following command:

    `kubectl get svc nginx-ingress-controller -n egov -o jsonpath='{.status.loadBalancer.ingress[0].hostname}'`

    The output of this will be the something like this:\
    [ae210873da6ff4c03bde2ad22e18fe04-233d3411.ap-south-1.elb.amazonaws.com](http://ae210873da6ff4c03bde2ad22e18fe04-233d3411.ap-south-1.elb.amazonaws.com/)\
    You need to add it in your domain provider against your domain name.

&#x20;

### Seed Data Setup: <a href="#seed-data-setup" id="seed-data-setup"></a>

1. Import the following postman collection - [https://api.postman.com/collections/12892142-55ebe4d0-3869-4879-87e1-5ba3b60cc6b7?access\_key=PMAT-01H27R18VPWXP2AE8812P0S12X](https://api.postman.com/collections/12892142-55ebe4d0-3869-4879-87e1-5ba3b60cc6b7?access\_key=PMAT-01H27R18VPWXP2AE8812P0S12X)
2.  Port-forward user pod using the following command -

    `kubectl port-forward <egov_user_pod> 8080:8080 -n egov`
3. Hit super\_user\_creation cURL. This will create a super user with username as GRO and password as eGov@4321.
4. Now, open the accessToken\_generation cURL. The credentials have already been populated. Change "_\{{YOUR\_DOMAIN\_NAME\}}_" placeholder to the domain name defined in _input.yaml_ file while provisioning and hit the cURL.
5. In the response, you will get "_access\_token_" field. Highlight this value, right click on it and set it as global "_token_ "value.
6. Once done, you can execute rainmaker common, rainmaker locality, rainmaker PGR localization and PGR workflow cURLs by changing "_\{{YOUR\_DOMAIN\_NAME\}}_" placeholder to the domain name defined in input.yaml file to setup localization and workflow seed data.&#x20;

&#x20;

### Destroying the Cluster: <a href="#destroying-the-cluster" id="destroying-the-cluster"></a>

If you want to destroy(delete) the cluster after demo is done. You can use the following command:

`kubectl delete svc nginx-ingress-controller -n egov cd ../../infra-as-code/terraform/sample-aws terraform destroy`

For destroying the remote state bucket, set the lifecycle value to false in [main.tf](http://main.tf/) file in the remote-state folder

`lifecycle { prevent_destroy = false }`

After that, go to AWS console and empty the S3 bucket. You can then proceed to destroy the remote state bucket using the _terraform destroy_ command.
