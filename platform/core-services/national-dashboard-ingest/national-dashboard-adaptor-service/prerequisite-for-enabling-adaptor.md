# Prerequisite for enabling Adaptor



1.Airflow should be deployed on the state side to extract data from the Elastic Search server to push to National Dashboard Adaptor .

2.The airflow should be configured with the required connection id’s and the variables.

es\_conn: To connect to the required ES server

digit-auth: To connect to the required API to insert data.

Variables:The credentials to connect to the API.

3.The index should have the data till the ward level data and should have the similar structure to have all the queries pull out the required result.

4.Pulling data from the DIGIT source only.

&#x20;

#### Changes done for the UPYOG:

* Builds deployed
* national-dashboard-ingest-db:nda-patch-db6cb27b02-18
* national-dashboard-kafka-pipeline:v0.0.1-762c61e743-3
* Upyog devOps and MDMS changes
* [<img src="https://github.com/fluidicon.png" alt="" data-size="line">NDSS adaptor related update by Gurjeet-eGov · Pull Request #6 · upyog/UPYOG-DevOps](https://github.com/upyog/UPYOG-DevOps/pull/6) **- upyog devOps PR**
* [<img src="https://github.com/fluidicon.png" alt="" data-size="line">NDSS adaptor related changes by Gurjeet-eGov · Pull Request #11 · upyog/upyog-mdms-data](https://github.com/upyog/upyog-mdms-data/pull/11) **- upyog mdms PR**
* Add localisation for newly loaded Punjab tenants
* Added NDA\_SYSTEM role action mapping in MDMS and created a user with access rights of the same
* Credentials: SYSTEMSU1 / eGov@123 - PG , user type: SYSTEM
