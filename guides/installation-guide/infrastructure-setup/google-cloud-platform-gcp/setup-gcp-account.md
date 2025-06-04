---
description: Steps to setup the GCP account before provisioning Infrastructure
---

# Setup GCP Account

## Overview <a href="#overview" id="overview"></a>

Follow the steps below to set up your GCP account before you proceed with the DIGIT deployment.

## **Setup**  <a href="#get-gcp-access" id="get-gcp-access"></a>

* Sign up for the GCP account if you do not already have one. Use this link to [get started](https://console.cloud.google.com/getting-started).
* Create a new project & [assign billing to it](https://cloud.google.com/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project).
* Assign Administrator/Owner Access to the user for the necessary permissions.
* Request CPU quotas (if not already available). You can check available quotas [here](https://console.cloud.google.com/apis/api/compute.googleapis.com/quotas?inv=1\&invt=AbxRbg\&pageState=\(%22allQuotasTable%22:\(%22f%22:%22%255B%257B_22k_22_3A_22_22_2C_22t_22_3A10_2C_22v_22_3A_22_5C_22region_3Aasia-south1_5C_22_22_2C_22s_22_3Atrue%257D_2C%257B_22k_22_3A_22_22_2C_22t_22_3A10_2C_22v_22_3A_22_5C_22CPUs_5C_22_22%257D%255D%22\)\)).
* Open the terminal. Run the following command you have installed on the AWS CLI, and use the credentials.
  * Initialise **GCloud CLI -** `gcloud init`
  * You will be prompted to log in and grant access in a web browser or to select an existing account. Complete the authorisation step when prompted.
  * Choose a current Google Cloud project if prompted.

{% code lineNumbers="true" %}
```
This account has a lot of projects! Listing them all can take a while.
 [1] Enter a project ID
 [2] Create a new project
 [3] List projects
Please enter your numeric choice:
```
{% endcode %}

{% hint style="info" %}
**Note:** If you only have access to one project, including the default project for your user account, `gcloud init` selects it for you. Otherwise, you can select a project from a list of projects for which you have **Owner**, **Editor** or **Viewer** permissions.
{% endhint %}

* Choose a default Compute Engine zone if prompted. (example: asia-south1-a for a zone in the Mumbai region)
* To view the properties set through the `gcloud init` command, use the `gcloud config list` command.

{% code lineNumbers="true" %}
```
[compute]
region = GCP_REGION
zone = GCP_AVAILABILITY_ZONE
[core]
account = demo@example.com
disable_usage_reporting = False
project = GCP_PROJECT_ID
```
{% endcode %}

* Run the below cmd and provide the prompted permissions. This enables Terraform to use the default credentials available.

{% code lineNumbers="true" %}
```
gcloud auth application-default login
```
{% endcode %}

* Install _**gke-gcloud-auth-plugin**_ for kubectl authentication.

{% code lineNumbers="true" %}
```
gcloud components install gke-gcloud-auth-plugin
```
{% endcode %}

* Enable the necessary Google APIs

{% code lineNumbers="true" %}
```
gcloud services enable compute.googleapis.com \
                       container.googleapis.com \
                       servicenetworking.googleapis.com \
                       sqladmin.googleapis.com \
                       cloudkms.googleapis.com \
                       --project=<GCP_PROJECT_ID>        # update project-id

# in-case above cmd fails
# try below one-liner cmd, update project-id at the end
gcloud services enable compute.googleapis.com container.googleapis.com servicenetworking.googleapis.com sqladmin.googleapis.com cloudkms.googleapis.com --project=<GCP_PROJECT_ID>
```
{% endcode %}

* Use the project-id, region & zone in Terraform to connect with your GCP account & provision cloud resources.
