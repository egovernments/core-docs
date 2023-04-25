# Deployment of Airflow DAG

### Deployment of Airflow <a href="#deployment-of-airflow" id="deployment-of-airflow"></a>

For deployment of Airflow we need the Kubernetes Environment.

**Step 1**: clone the git repo for [airflow](https://github.com/airflow-helm/charts.git) , and update the[ values.yaml ](https://github.com/airflow-helm/charts/blob/main/charts/airflow/values.yaml) as per the requirement.

**Step 2**: update the git repository url and subpath for the directory in values.yaml

Here we have updated  as&#x20;

repo: "[GitHub - pmidc-digit/utilities](https://github.com/pmidc-digit/utilities.git) ”

repoSubPath: "egov-national-dashboard-accelerator/dag

branch: "develop

**Step 3**: change the directory to airflow and update the helm .update the helm repo on local and add the airflow repo to Helm using below command

helm repo add apache-airflow [https://airflow.apache.org](https://airflow.apache.org/)

The above command will pull airflow repo and it will be added to your local helm repository.

**Step 4**: Installing apache airflow after updating helm repositories

&#x20;helm install airflow apache-airflow/airflow --namespace egov

The above command will take the updated

**Step 5**: to upgrade the changes we made to values.yaml use below command.

helm upgrade --install airflow apache-airflow/airflow -n airflow -f values.yaml

The above command will update the git repo, subpath and branch while deployment.

**Step 6**: Deployment is done pods service will start running with updated values.yaml

&#x20;

Latest files for the deployment:

Attached is the final "values.yaml" file. It syncs both the plugins and dags from repo.

[Airflow Deployment](https://github.com/pmidc-digit/utilities/tree/dataphi/egov-national-dashboard-accelerator/docs/deployment)
