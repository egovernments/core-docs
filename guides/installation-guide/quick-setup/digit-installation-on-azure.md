---
description: DIGIT services deployment in azure cloud platform
---

# DIGIT Installation on Azure

## **Pre-requisites** <a href="#id-1.-pre-requisites" id="id-1.-pre-requisites"></a>

* Make sure you have your Azure account with the necessary credentials.
* Install [Golang](https://golang.org/doc/install#download) - Use these links to install- [Linux](https://golang.org/dl/go1.13.3.linux-amd64.tar.gz) or [Windows](https://golang.org/dl/go1.13.3.windows-amd64.msi) or [Mac](https://golang.org/dl/go1.13.3.darwin-amd64.pkg)
* ​All DIGIT services are packaged using helm charts, Install helm using the link [<img src="https://helm.sh/img/favicon-152.png" alt="" data-size="line">Installing Helm](https://helm.sh/docs/intro/install/)
* ​[kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) is a CLI to connect to the Kubernetes cluster on your machine
* Install [CURL](https://help.ubidots.com/en/articles/2165289-learn-how-to-install-run-curl-on-windows-macosx-linux) for making API calls
* ​[Install VisualStudio](https://code.visualstudio.com/download) IDE Code for better code visualization/editing capabilities
* ​[Install Postman](https://www.postman.com/downloads/) to run digit bootstrap scripts
* Install [Terraform](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli) to provide infrastructure on Azure
* Install [Azure CLI ](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)and [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

## Infra Setup

* Clone the DIGIT-DevOps Repo and check out to the Azure branch

{% code lineNumbers="true" %}
```
git clone https://github.com/egovernments/DIGIT-DevOps.git
cd DIGIT-DevOps
git checkout azure-install
code
```
{% endcode %}

* Change to the remote state in the sample-azure directory

```
cd infra-as-code/terraform/sample-azure/remote-state
```

* Login to Azure using the below command in the terminal

```
az login
```

* Update the variables in variables.tf file
* Run the below commands to create resource-group, storage-account and container

{% code lineNumbers="true" %}
```
terraform init
terraform plan
terraform apply
```
{% endcode %}

* Copy the storage account name and change to the sample-azure directory

```
cd ..
```

* Open main.tf file and update the below placeholder details

{% code lineNumbers="true" %}
````
```
terraform {
  backend "azurerm" {
      resource_group_name  = "<resource_group>"
      storage_account_name = "<storage_account>"
      container_name       = "<container>"
      key                  = "terraform.tfstate"
  }
}
```
````
{% endcode %}

* Create client-id and client-secret with necessary permissions&#x20;

{% code lineNumbers="true" %}
```
az ad sp create-for-rbac --name <sp_name> \
             --role owner \
             --scopes /subscriptions/<subscription_id>
```
{% endcode %}

* Open variables.tf file - update the variables and run the below commands

{% code lineNumbers="true" %}
```
terraform init
terraform plan
terraform apply
```
{% endcode %}

* Note the db\_name and server\_name
* Fetch the kubeconfig using the below command. This will automatically store your kubeconfig in .kube folder

```
az aks get-credentials --resource-group <resource_group_name> --name <cluster_name>
```

* Check the kubeconfig and pods by running the below commands

{% code lineNumbers="true" %}
```
kubectl config get-contexts
kubectl config use-context <cluster_name>
kubectl get pods -A
```
{% endcode %}

## Deployment

* Change to the environments directory and open egov-demo.yaml

{% code lineNumbers="true" %}
```
cd ../../..
cd config-as-code/environments
```
{% endcode %}

* Update the below configurations in egov-demo.yaml

{% code lineNumbers="true" %}
```
global:
   domain: <domain_name> ## Add your Domain Name "Eg: site.mydomain.com" Do not use the dummy domain
   setup: fullsetup

cluster-configs:
    configmaps:
        egov-config:
            namespace: [ egov, monitoring ]
            data:
                db-host: <db_host_name> ## Add db-host name eg: egov-demo.database.azure.com
                db-name: <db_name> ## Add db-name
                db-url: jdbc:postgresql://<db_host_name>/<db_name> ## example: jdbc:postgresql://egov-demo.postgres.database.azure.com:5432/egov_demo
                domain: <domain_name> ## Add your Domain Name    
                egov-services-fqdn-name: https://<domain_name>/ ## Add your Domain Name
    
```
{% endcode %}

* Open the egov-demo-secrets.yaml file and update db details and private key

<pre data-line-numbers><code>cluster-configs:
    secrets:
        db:          # update the postgres db credentials
            username: &#x3C;db_username>
            password: &#x3C;db_pwd> # must be more than 8 characters
            flywayUsername: &#x3C;db_username>
            flywayPassword: &#x3C;db_pwd> 
        git-sync:
<strong>            ssh: |
</strong>                -----BEGIN RSA PRIVATE KEY-----
                MIIEogIBAAKCAQEAg5idfPBCic+oyvNH4pkRm7OAO6bLDJT2sFtNHkXmVN3OGLUZ
                NBnXUEJS8Gkdal1JOhWSZBv6YBpOXX7m/sI3B3klxj5sLayyj9p21Yrc+Jcadsam
                XZWvl8nI1VZDBgmddnnWSHcYP+3kD6ChxykoVrbJKKi0PGNDYEKOLHvbQ/Qy5x6M
                w73xSlvF+80A3f7JhcssW/aZOIscTcNB8dAi84csjLcGIKQLKKB9omFbnd9Jh5V4
                TipjkYWhxpYo3bRGL3MfwYjzq/dGHT0I72XoeD8TT5TqYATV05KSwYPWOfDoRSp6
                LX3gyWFlibzwUkblL0rQqqEYXeXMpvUM3HadnQIDAQABAoIBACRz4Bw9yZC3L0CY
                x27ji9cfkAP2HgTsNrF/eQtLvZQApRh/Ae5Gwjf/R05FL9rI4IHwe86zWVXJs69+
                eapUTj4JtwcFP54fWo8yqvxYLQHHiZMhT/BYiH15beJ6tLI1c6Lf+RW1t8fts+EI
                VAgBRKVQmMRkhxi7Pmypwwxbes+FrZKK28CkkE6oyTXNco1Fpw/Txn93bscHgf3+
                3bHjKJw6y3e+Zgg73oLdLRSUUgrgWRlb0ShlrGrgu1hXANFGLoRGPNas4AcbqzRZ
                34a1ddroiXpcZdY+XHkLn1SupWyS0lj//EvGG0DjILjWYH1mLVsas/PB/l83T/O+
                UyQ8OdkCgYEAx23W6NndOq6tPnGMdP1NUxXGy7WwahSszNy7PWzBmfYP5yByncWi
                lBNT2ahl26qiPt98EuHEotm2lVN+yF+8sVWZJeGYNp3A5CP/plkRfPeEmKP0sqyK
                4BXgLca440/EsJnkwUOV26OOMnRu72wzJ2aUZO7l7bkyVZk7kwaIHN8CgYEAqOzg
                5F1kuAd8qwodrquVc8P+iO8uJtBMZqjjwLVw/DyfA4Eq6kdLCWQMByRojXiFYg/1
                X5xNiwLs/0qzEfh3ruBFahUNC2dzlEJwochDfXaKpCUDkxH7fKUhbMmij3s/C07Y
                js9OGdzxU3X/cGOSXONdHWDjuItoQkyANgcDmQMCgYA2uOYSqM1yr8Gr875lz6er
                F7uf5DAPO7Ma16qtNS1+kK1Wb2nj7voohZEplXK1rwGsHOjPyZGKWhEmsm2Ej/iX
                9HP8mAWLXwgx0crxm1kYIFcLB1o6uOu2h2onRXMwNJA1IVVKzr/NL/jx0U8rdVYo
                BpbLh14iOAIeyNg3BMDOowKBgEK/lv2lia7OBozvKltioWNlBqbFG89qb0YBZj03
                dLW2nn6cA4EfOp8zUS1hTY7ZGJtvAt4MvPc46LzXn3pyW5hWNhd8yfK/pgPnXOoQ
                X9qrhIzns0nhySWvek2qPvnDEV4+gYOslofRren0rkKSlbrufFSnfFPnggLwh5jR
                nLJRAoGAcQFfoWwwP5cpPM9g4WgaYENbV0BQchwwqti0TQWXrTUsgHCdHj+mrTv4
                F0R/hKrVuk1WrWDK/nkL94gTytLsjS5wF84Na+QZKcVxEUqRhndHZomPX3iVRLkV
                MvayNKpGzZEs+Qd3WyJq4y19vWwhCFQ802Pa5IAOz+tPWNi/6v4=
                -----END RSA PRIVATE KEY-----
</code></pre>

Generate SSH key pairs (Use either method (a) or method (b)) to update the private key.

a. Using the online website (not recommended for production setup. To be only used for demo setups): [https://8gwifi.org/sshfunctions.jsp](https://8gwifi.org/sshfunctions.jsp)

b. Using OpenSSL :

`openssl genpkey -algorithm RSA -out private_key.pem openssl rsa -pubout -in private_key.pem -out public_key.pem`

Add the public key to your GitHub account (reference: [https://www.youtube.com/watch?v=9C7\_jBn9XJ0\&ab\_channel=AOSNote](https://www.youtube.com/watch?v=9C7\_jBn9XJ0\&ab\_channel=AOSNote) )

* Change to the deployer directory&#x20;

{% code lineNumbers="true" %}
```
cd ../..
cd deploy-as-code/deployer
go run standalone_installer.go
```
{% endcode %}

* Run the below command to deploy nginx-ingress

```
kubectl apply -f ../../config-as-code/helm/charts/backbone-services/azure-nginx/ingress.yaml
```

* Check the pods once all services are deployed successfully

```
kubectl get pods -A
```

* Run the below command to get the load balancer id&#x20;

```
kubectl get svc -A | grep ingress
```

* Copy the load balancer id and add it to your domain provider against your domain name.
