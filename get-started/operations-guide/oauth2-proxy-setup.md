---
description: This doc is about OAuth2-proxy Setup
---

# OAuth2-Proxy Setup

## Pre-reads

{% embed url="https://oauth2-proxy.github.io/oauth2-proxy/" %}

## Pre-requisites <a href="#prerequisites" id="prerequisites"></a>

* DIGIT uses [golang](https://golang.org/doc/install#download) (required v1.13.3) automated scripts to deploy the builds onto Kubernetes - [Linux](https://golang.org/dl/go1.13.3.linux-amd64.tar.gz) or [Windows](https://golang.org/dl/go1.13.3.windows-amd64.msi) or [Mac](https://golang.org/dl/go1.13.3.darwin-amd64.pkg)
* All DIGIT services are packaged using helm charts[ ![](https://helm.sh/img/favicon-152.png)Installing Helm](https://helm.sh/docs/intro/install/)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) is a CLI to connect to the Kubernetes cluster from your machine
* [Install Visualstudio](https://code.visualstudio.com/download) IDE Code for better code/configuration editing capabilities
* Git
* [GitHub OAuth app](https://docs.github.com/en/developers/apps/building-oauth-apps/creating-an-oauth-app)

## Oauth2-proxy Setup

*   Clone the following [DIGIT-DevOps](https://github.com/egovernments/DIGIT-DevOps) repo (If not already done as part of Infra setup), you may need to [install git](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository-from-github/cloning-a-repository) and then run [git clone](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository-from-github/cloning-a-repository) on your machine.

    `git clone -b release https://github.com/egovernments/DIGIT-DevOps`
* `Add below configs into your environment file`

```
oauth2-proxy:
  config:
    configFile: |-
      email_domains = [ "*" ]
      github_org = "<github_org>"                     # Repalce with GitHub org name
      github_team = "<github_team>,<github_team>"     # Repalce with GitHub teams
      upstreams = [ "file:///dev/null" ]
```

* Create a GitHub OAuth app and add the below secrets into the environment secrets file
  * GitHub OAuth App Creation&#x20;
    * Follow the [GitHub OAuth app](https://docs.github.com/en/developers/apps/building-oauth-apps/creating-an-oauth-app)
    * Homepage URL:- mentions your domain name eg. https://\<your\_domain\_name>
    * Authorization callback URL:-  https://\<your\_domain\_name>/oauth2/callback

```
oauth2-proxy:   ## To work oauth2-proxy service, create and add your github OAuth Apps details
    clientID: qwgethjymnbv  
    clientSecret: 3a08079easd95696fd3baad5292
    cookieSecret: QVbnq0L96wtBg==   ## Any random hash value
```

*   Deploy the oauth2-proxy via Jenkins deployment job or go land deployer&#x20;

    ```
    cd DIGIT-DevOps/deploy-as-code/deployer
    go run main.go deploy -e <environment_name> 'oauth2-proxy'
    ```
