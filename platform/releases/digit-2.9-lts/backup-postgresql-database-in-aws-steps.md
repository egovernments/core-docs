# Backup PostgreSQL Database In AWS - Steps

## Overview

This document provides step-by-step instructions on how to take backups of PostgreSQL databases hosted on AWS.

## **Pre-requisites**

* Access to an AWS account with permissions to manage Amazon RDS instances.
* PostgreSQL database hosted on Amazon RDS.

## **Steps**

**Step 1: Navigate to the Amazon RDS Console:**

* Log in to the AWS Management Console.
* Go to the Amazon RDS service.

**Step 2: Select the PostgreSQL Instance:**

* From the list of DB instances, select the PostgreSQL instance for which you want to take the backup.

**Step 3: Enable Automated Backups (Optional):**

* If automated backups are not already enabled, navigate to the "Backup" tab of the RDS instance.
* Click on "Modify" and enable automated backups.
* Configure the backup retention period according to your requirements.

**Step 4: Manually Trigger a Snapshot:**

To create a manual snapshot, select the RDS instance you want to back up. Click on the **Actions** button in the right upper corner and select **Take a snapshot**.

![](https://www.sqlservercentral.com/wp-content/uploads/2021/06/word-image-183.png)

This will redirect you to a page like the one below.

![](https://www.sqlservercentral.com/wp-content/uploads/2021/06/word-image-184.png)

Provide a meaningful name for the snapshot and click “**Create snapshot**”.

![](https://www.sqlservercentral.com/wp-content/uploads/2021/06/word-image-185.png)

This will create a manual snapshot of the DB instance that you created.

![](https://www.sqlservercentral.com/wp-content/uploads/2021/06/word-image-186.png)

**Step 5: Create a Manual Backup Using pg\_dump:**

* Connect to the PostgreSQL database using a PostgreSQL client tool or command-line interface.
*   Use the `pg_dump` command to export the database to a file:

    ```bash
    bashCopy codepg_dump -h <hostname> -U <username> -d <database_name> -f <backup_file_name>.sql
    ```

    Replace `<hostname>`, `<username>`, `<database_name>`, and `<backup_file_name>` with the appropriate values.

**Step 6: Copy Backup Files to Amazon S3 (Optional):**

* If desired, copy the backup files to Amazon S3 for long-term storage and redundancy.
* Use the AWS CLI or SDKs to upload the files to an S3 bucket.

## Summary

This document has provided instructions on how to take backups of PostgreSQL databases hosted on AWS. Regular backups are essential for data protection and disaster recovery purposes.

\
