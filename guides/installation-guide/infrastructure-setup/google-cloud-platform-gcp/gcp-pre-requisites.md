# GCP - Pre-requisites

## **Pre-requisites** <a href="#pre-requisites" id="pre-requisites"></a>

1. [**GCP Account**](https://console.cloud.google.com/) with admin access to provision infrastructure. You will need a paid subscription to the GCP.
2. Install [**GCloud CLI**](https://cloud.google.com/sdk/docs/install) - to authenticate & connect with GCP APIs.
3. Install [**kubectl**](https://kubernetes.io/docs/tasks/tools/) (any version) on the local machine - it helps interact with the Kubernetes cluster.
4. Install [**Helm**](https://helm.sh/docs/intro/install/) - helps package the services, configurations, environments, secrets, etc, into [**Kubernetes manifests**](https://devspace.cloud/docs/cli/deployment/kubernetes-manifests/what-are-manifests)**.** Verify that the installed version of Helm is equal to 3.0 or higher.

```
// command to check helm version
helm version
```

5. Install [terraform](https://releases.hashicorp.com/terraform/0.14.10/) - for the [Infra-as-code](https://core.digit.org/guides/installation-guide/infrastructure-setup/sdc/2.-infra-as-code-kubespray) (IaC) to provision cloud resources. This provides the desired resource graph and helps destroy the cluster in one go.​

{% code lineNumbers="true" %}
```
// On Linux
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt-get update && sudo apt-get install terraform
```
{% endcode %}

{% code lineNumbers="true" %}
```
// On Mac
brew tap hashicorp/tap
brew install hashicorp/tap/terraform
```
{% endcode %}

6. (Optional) Install [**tfswitch**](https://github.com/warrensbox/terraform-switcher) - to run different versions of Terraform on the machine. [tfswitch](https://github.com/warrensbox/terraform-switcher) supports multiple Terraform versions on the same machine, and you can toggle between the desired versions.

{% code lineNumbers="true" %}
```
// On Mac
brew install warrensbox/tap/tfswitch
```
{% endcode %}

{% code lineNumbers="true" %}
```
// On Linux
curl -L https://raw.githubusercontent.com/warrensbox/terraform-switcher/master/install.sh -o install.sh
sudo bash install.sh
```
{% endcode %}

Run tfswitch, and it will show a list of Terraform versions. Scroll down and select the **Terraform** version (0.14.10).

7. Install [**Golang**](https://go.dev/doc/install#download)
   * For Linux: Follow the [instructions here](https://go.dev/doc/install#download) to install Golang on Linux.
   * For Windows: Download the installer using the [link here](https://go.dev/doc/install#download) and follow the installation instructions.
   * For Mac: Download the installer using the [link here](https://go.dev/doc/install#download) and follow the installation instructions.
8. Install [**SOPS**](https://github.com/getsops/sops) -
   * For Linux: Follow the [instructions here](https://technotim.live/posts/install-mozilla-sops/) to install SOPS on Linux.
   * For Windows: Download the binary & follow the [instructions](https://github.com/getsops/sops/discussions/1251#discussioncomment-11141061) provided.
   * For Mac: Follow the [instructions here](https://formulae.brew.sh/formula/sops) to install SOPS on macOS.
9. Install [**cURL**](https://curl.se/) **-** for making API calls.
   * For Linux: Follow the [instructions here](https://help.ubidots.com/en/articles/2165289-learn-how-to-install-run-curl-on-windows-macosx-linux)
   * For Windows: Download the wizard & follow the [instructions](https://curl.se/windows/) provided.
   * For Mac: Follow the [instructions here](https://help.ubidots.com/en/articles/2165289-learn-how-to-install-run-curl-on-windows-macosx-linux) to install on macOS.
10. Install [**Visual Studio Code**](https://code.visualstudio.com/download) **-** for better code visualisation/editing capabilities.
11. Install [**Postman**](https://www.postman.com/downloads/) **-** to run digit bootstrap scripts.
