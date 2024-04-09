# Installation of Terraform

**Terraform:** Terraform is an open-source infrastructure as code software tool that enables you to safely and predictably create, change, and improve infrastructure.

**what is Terraform is used for:** Terraform is an IAC tool, used primarily by DevOps teams to automate various infrastructure tasks. The provisioning of cloud resources, for instance, is one of the main use cases of Terraform. It is a open-source provisioning tool written in the Go language and created by HashiCorp.

* To install Terraform, use the following link to download the zip file.

{% embed url="https://releases.hashicorp.com/terraform/0.14.10/" %}

* As per our requirment we have to install a specific version which is **0.14.10.**

{% embed url="https://releases.hashicorp.com/terraform/0.14.10/terraform_0.14.10_linux_amd64.zip" %}

* Install the unzip.

```
$ sudo apt-get install unzip
```

* Extract the downloaded file archive.

```
unzip terraform_0.14.10_linux_amd64.zip
```

* Move the executable into a directory searched for executables.

```
sudo mv terraform /usr/local/bin/
```

* Run the below command to check whether the terraform is working.

```
terraform --version
```

<figure><img src="../../../.gitbook/assets/Screenshot from 2022-12-12 17-06-42.png" alt=""><figcaption></figcaption></figure>
