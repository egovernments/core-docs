# Persister Service



### Overview <a href="#overview" id="overview"></a>

Persister service provides a framework to persist data in transactional fashion with low latency based on a config file. Removes repetitive and time consuming persistence code from other services.

### Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before you proceed with the documentation, make sure the following pre-requisites are met -

* Prior Knowledge of Java/J2EE.
* Prior Knowledge of SpringBoot.
* Prior Knowledge of PostgresSQL.
* Prior Knowledge of JSONQuery in Postgres. (Similar to PostgresSQL with a few aggregate functions.).
* Kafka server is up and running.

### Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

* Persist data asynchronously using kafka providing very low latency
* Data is persisted in batch
* All operations are transactional
* Values in prepared statement placeholder are fetched using JsonPath
* Easy reference to parent object using ‘{x}’ in jsonPath which substitutes the value of the variable x in the JsonPath with value of x for the child object.(explained in detail below in doc)
* Supported data types _**ARRAY**_(**"ARRAY"**), _**STRING**_(**"STRING"**), _**INT**_(**"INT"**),_**DOUBLE**_(**"DOUBLE"**), _**FLOAT**_(**"FLOAT"**), _**DATE**_(**"DATE"**), _**LONG**_(**"LONG"**),_**BOOLEAN**_(**"BOOLEAN"**),_**JSONB**_(**"JSONB"**)

### Configuration Details <a href="#configuration-details" id="configuration-details"></a>

Persister uses configuration file to persist data. The key variables are described below:

* serviceName: Name of the service to which this configuration belongs.
* description: Description of the service.
* version: the version of the configuration.
* fromTopic: The kafka topic from which data is fetched
* queryMaps: Contains the list of queries to be executed for the given data.
* query: The query to be executed in form of prepared statement:
  * basePath: base of json object from which data is extrated
  * jsonMaps: Contains the list of jsonPaths for the values in placeholders.
  * jsonPath: The jsonPath to fetch the variable value.

```
serviceMaps:
 serviceName: student-management-service
 mappings:
 - version: 1.0
   description: Persists student details in studentinfo table
   fromTopic: save-student-info
   isTransaction: true
   queryMaps:
       - query: INSERT INTO studentinfo( id, name, age, marks) VALUES (?, ?, ?, ?);
         basePath: Students.*
         jsonMaps:
          - jsonPath: $.Students.*.id

          - jsonPath: $.Students.*.name

          - jsonPath: $.Students.*.age

          - jsonPath: $.Students.*.marks
```

#### Bulk Persister: <a href="#bulk-persister" id="bulk-persister"></a>

To persist large quantity of data bulk setting in persister can be used. It is mainly used when we migrate data from one system to another. The bulk persister have the following two settings:

| Variable Name          | Default Value | Description                                      |
| ---------------------- | ------------- | ------------------------------------------------ |
| persister.bulk.enabled | false         | Switch to turn on or off the bulk kafka consumer |
| persister.batch.size   | 100           | The batch size for bulk update                   |

Any kafka topic containing data which has to be bulk persisted should have **'-batch'** appended at the end of topic name example: **save-pt-assessment-batch**.

#### Persister Config Versioning: <a href="#persister-config-versioning" id="persister-config-versioning"></a>

* Each persister config has a version attribute which signifies the service version, this version can contain custom DSL; defined here, [GitHub - zafarkhaja/jsemver: Java implementation of the SemVer Specification](https://github.com/zafarkhaja/jsemver#external-dsl)
* Every incoming request \[via kafka] is expected to have a version attribute set, \[jsonpath, $.RequestInfo.ver] if versioning is to be applied.
* If the request version is absent or invalid \[not semver] in the incoming request, then a default version defined by the following property in application.properties`default.version=1.0.0` is used.
* The request version is then matched against the loaded persister configs and applied appropriately.

### Deployment Details <a href="#deployment-details" id="deployment-details"></a>

1. Write configuration as per the requirement. Refer the example given earlier.
2. In the environment file, mention the file path of configuration under the variable `egov.persist.yml.repo.path` while mentioning the file path we have to add `file:///work-dir/` as prefix. for example: `egov.persist.yml.repo.path = file:///work-dir/configs/egov-persister/abc-persister.yml`. If there are multiple file separate it with comma (`,`) .
3. Deploy latest version of egov-persister service and push data on kafka topic specified in config to persist it in DB.

### Integration  <a href="#integration" id="integration"></a>

#### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

The persister configuration can be used by any module to store records in particular table of database.

#### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

* Insert/Update Incoming Kafka messages to Database.
* Add Modify kafka message before putting it into database.
* Persist data asynchronously.
* Data is persisted in batch.

#### Steps to Integration <a href="#steps-to-integration" id="steps-to-integration"></a>

1. Write configuration as per your requirement. Structure of the config file is explained above in the same document.
2. Check-in the config file to a remote location preferably github.
3. Provide the absolute path of the checked-in file to DevOps, to add it to the file-read path of egov-persister. The file will be added to egov-persister's environment manifest file for it to be read at start-up of the application.
4. Run the egov-persister app and push data on kafka topic specified in config to persist it in DB

## Reference Docs

### Play around with the API's : [DIGIT-Playground](https://digit-api.apidog.io/doc-507201)&#x20;
