---
description: Steps to trigger airflow DAG
---

# Trigger Airflow DAG

## Overview

In Airflow, a `DAG` –Directed Acyclic Graph – is a collection of the tasks you want to run, organized in a way that reflects their relationships and dependencies.

A DAG is defined in a Python script, which represents the DAGs structure (tasks and their dependencies) as code.

### Run DAG Airflow <a href="#how-to-run-dag-in-airflow" id="how-to-run-dag-in-airflow"></a>

**Manual Trigger**

1.Log onto the Punjab Prod server using the credentials:

URL: [Sign In - Airflow](https://airflow.mseva-qa.lgpunjab.gov.in/login/?next=http%3A%2F%2Fairflow.mseva-qa.lgpunjab.gov.in%2Fhome)

&#x20;   username: admin

&#x20;   password:  admin

<figure><img src="../../../../../.gitbook/assets/image-20220812-045435.png" alt=""><figcaption></figcaption></figure>

2\. Trigger the DAG by clicking on the “Trigger DAG with Config” option.

<figure><img src="../../../../../.gitbook/assets/image-20220812-104728 (1).png" alt=""><figcaption></figcaption></figure>

3\. Enter a date and click on the Trigger button

Format {“date”: “dd-MM-yyyy”}

<figure><img src="../../../../../.gitbook/assets/Kuzp2618iZBIbcPUNFNKJCxwhVRmwVUyZKPjISyEfzrIa_0SgXPaLY_kHfVLWb3HZGvQJIYaTLgIWed9Ozb5nZAfK-2TI8QoOgHM7ETZviHoDH3wUuJ86b-UPHOVMUS6d75C9AWfDcC9mVz3tE233A.png" alt=""><figcaption></figcaption></figure>

4\. Click on the Log option and expand the DAG to view the logs.  Choose a stage for any module.

<figure><img src="../../../../../.gitbook/assets/1-0FCa58wJrxAiWawRo1RUdWIeWjKdH7SaN1b0__phFLG4qOND6RmLCT0azJjsEY7qorTz_6fgujjIfrL2_rgI1EwNbr00BHYLriHLK3X07FSROAAwiCGXMcICwp9ARMZ9l5RnoYPgtJZKfGp1gcmA.png" alt=""><figcaption></figcaption></figure>

Logs can also be viewed in the Elastic search index adaptor\_logs

GET adaptor\_logs/\_search - the timestamp is provided based on the day for which the logs are being searched.

<figure><img src="../../../../../.gitbook/assets/image-20220818-075050.png" alt=""><figcaption></figcaption></figure>

### **Scheduled DAG**

This DAG triggers every day at midnight for the previous day.

<figure><img src="../../../../../.gitbook/assets/image-20220812-104859.png" alt=""><figcaption></figcaption></figure>

**Bulk Insert For A Date Range**

Execute the script to run the DAG for a date range for the staging NDB

sh iterate\_over\_date.sh \<start-date> \<end-date>\
ex: sh iterate\_over\_date.sh 01-03-2022 05-03-2022

* date needs to be in the format of dd-mm-YYYY
* range exclusive of the last date, \[start-date, end-date). For instance: in the above example, the script will trigger DAG on 1st, 2nd, 3rd and 4th March. It will not be triggered on 5th March.

[utilities/Bulk\_insert.sh at develop · pmidc-digit/utilities](https://github.com/pmidc-digit/utilities/blob/develop/egov-national-dashboard-accelerator/Bulk\_insert.sh)
