# Deployment of Airflow DAG

## Overview <a href="#deployment-of-airflow" id="deployment-of-airflow"></a>

This page provides steps to deploy Airflow DAG.

## Deployment of Airflow <a href="#deployment-of-airflow" id="deployment-of-airflow"></a>

The Kubernetes environment is required for the deployment of Airflow.

**Step 1**: Clone the git repo for [airflow](https://github.com/airflow-helm/charts.git), and update the[ values.yaml ](https://github.com/airflow-helm/charts/blob/main/charts/airflow/values.yaml)as per the requirement.

**Step 2**: Update the git repository URL and subpath for the directory in values.yaml

Example: the following params are updated as given below:&#x20;

* repo: "[GitHub - pmidc-digit/utilities](https://github.com/pmidc-digit/utilities.git) ”
* repoSubPath: "egov-national-dashboard-accelerator/dag
* branch: "develop

**Step 3**: Change the directory to airflow and update the helm. Update the helm repo locally and add the airflow repo to Helm using the command below:

* helm repo add apache-airflow [https://airflow.apache.org](https://airflow.apache.org/)

The above command pulls the airflow repo and it is added to the local helm repository.

**Step 4**: Installing Apache airflow after updating the helm repositories

* helm install airflow apache-airflow/airflow --namespace egov

The above command will take the updated repo details.

**Step 5**: Upgrade the changes made to values.yaml using the command below.

* helm upgrade --install airflow apache-airflow/airflow -n airflow -f values.yaml

The above command updates the git repo, subpath and branch while deployment.

**Step 6**: Deployment is done pods service will start running with updated values.yaml

* Latest files for the deployment: Attached below is the final "values.yaml" file. It syncs both the plugins and dags from the repo. [Airflow Deployment](https://github.com/pmidc-digit/utilities/tree/dataphi/egov-national-dashboard-accelerator/docs/deployment)
