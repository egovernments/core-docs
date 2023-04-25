# Azure

### Prepare Azure Environment

For provisioning Kubernetes clusters with the [Azure cloud provider](https://github.com/kubermatic/machine-controller/tree/master/pkg/cloudprovider/provider/azure) Kubermatic needs a service account with (at least) the Azure role `Contributor`. Follow the steps below to create a matching service account.

### Login to Azure and Get Basic Information

Login to Azure with [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/?view=azure-cli-latest) `az`.

This command opens in your default browser window where you can authenticate. Get your subscription ID once you are logged in successfully.

```
az account show --query id -o json

********-****-****-****-************
```

Get your Tenant ID -

```
az account show --query tenantId -o json

********-****-****-****-************
```

Create a new app using -

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/********-****-****-****-************"

Retrying role assignment creation: 1/36
Retrying role assignment creation: 2/36
Retrying role assignment creation: 3/36
{
  "appId": "********-****-****-****-************",
  "displayName": "azure-cli-2018-11-25-08-01-39",
  "name": "http://azure-cli-2018-11-25-08-01-39",
  "password": "********-****-****-****-************",
  "tenant": "********-****-****-****-************"
}
```

Enter provider credentials using the values mentioned in the step [Prepare Azure Environment ](azure.md#prepare-azure-environment)into Kubermatic Dashboard:

* `Client ID`: Take the value of `appId`
* `Client Secret`: Take the value of `password`
* `Tenant ID`: your tenant ID
* `Subscription ID`: your subscription ID

