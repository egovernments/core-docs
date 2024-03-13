# Updating RDS Version in AWS

### **1. Introduction:**

This document provides step-by-step instructions on how to update the version of Amazon RDS (Relational Database Service) using both the AWS Management Console and Terraform.

### **2. Prerequisites:**

* Access to an AWS account with permissions to manage Amazon RDS instances.
* Basic knowledge of AWS Management Console and Terraform.
* Create a RDS Snapshot Backup for Data Protection.

### **3. Updating RDS Version using AWS Management Console:**

&#x20;**Step 1: Navigate to the Amazon RDS Console:**

* Log in to the AWS Management Console.
* Go to the Amazon RDS service.

**Step 2: Select the RDS Instance:**

* From the list of DB instances, select the RDS instance for which you want to update the version.

**Step 3: Initiate the Upgrade:**

* From the given databases, select the database you wish to upgrade the Engine Version of and click on the **“Modify”** button.&#x20;

<figure><img src="https://media.geeksforgeeks.org/wp-content/uploads/20210511181445/Screenshot55LI.jpg" alt=""><figcaption></figcaption></figure>

* In the Modify DB Instance wizard, locate the "DB Engine Version" section. Select the desired version from the dropdown list. Review the other configuration settings and click on the "Continue" button.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-03-05 at 6.04.43 PM.png" alt=""><figcaption></figcaption></figure>

* Select **“Apply Immediately”** and Review the summary of changes and click on the "Modify DB Instance" button to initiate the upgrade.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-03-05 at 6.05.26 PM.png" alt=""><figcaption></figcaption></figure>

**Step 4: Monitor the Upgrade Progress:**

* Once the upgrade is initiated, monitor the upgrade progress from the RDS dashboard.
* The status of the instance will change to "modifying" during the upgrade process.
* Once the upgrade is completed, the status will change back to "available."

### **4. Updating RDS Version using Terraform:**

**Step 1: Define the Terraform Configuration:**

* Create or update the Terraform configuration file (e.g., `variable.tf`) with the necessary settings to manage the RDS instance.
* Use the `aws_rds_instance` resource to define the RDS instance.
* Specify the desired version in the `engine_version` attribute.

**Step 2: Apply the Terraform Configuration:**

* Run `terraform plan` to preview the changes that will be applied.
* Run `terraform apply` to apply the changes and update the RDS instance with the new version.

**Step 3: Monitor Terraform Execution:**

* Monitor the Terraform execution for any errors or warnings.
* Once the execution is completed, verify that the RDS instance has been updated to the new version.

### **5. Conclusion:**

This document has provided instructions on how to update the version of Amazon RDS using both the AWS Management Console and Terraform. Regularly updating the RDS version ensures that your database instance is up-to-date with the latest features and security patches.

\
