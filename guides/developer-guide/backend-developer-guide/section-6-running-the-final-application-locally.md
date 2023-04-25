# Section 6: Running the final application locally

, it is time to test our completed application!

Before testing our application, we need to run a couple of services locally -

1. To run the persister service locally -&#x20;
   * &#x20;Run Kafka.
   * Open egov-persister folder which should be present under core-services repository.
   *   Update the following properties in application.properties file -&#x20;

       ```
       spring.datasource.url=jdbc:postgresql://localhost:5432/{LOCAL_DATABASE_NAME}

       egov.persist.yml.repo.path=file://{ABSOLUTE_PATH_OF_PERSISTER_CONFIG_FILE}
       ```
2.  To run indexer service locally (optional) -&#x20;

    * Run Kafka.
    * Run ElasticSearch.
    * Open egov-indexer folder which should be present under core-services repository.
    * Update the following properties in application.properties file -

    ```
    egov.indexer.yml.repo.path=file://{ABSOLUTE_PATH_OF_INDEXER_CONFIG_FILE}
    ```

For **example**, the path to config files would be something like -&#x20;

```
egov.indexer.yml.repo.path=file:///Users/nithin/Documents/eGov/egov-repos/core-services/egov-indexer/src/main/resources/collection-indexer.yml
```

To run and test our sample application, the following steps need to be followed -

1. Ensure that Kafka, Persister, Indexer, PDF service are running locally and run the code of voter-registration-service from DIGIT\_DEVELOPER\_GUIDE branch (for consistency).
2. Port-forward the following services -
   * egov-user to port 8284 (for e.g. - `kubectl port-forward egov-user-58d6dbf966-8r9gz 8284:8080`)
   * egov-localization to port 8286 (for e.g. `kubectl port-forward egov-localization-d7d5ccd49-xz9s9 8286:8080`)
   * egov-filestore to 8288 (for e.g. `kubectl port-forward egov-filestore-86c688bbd6-zzk72 8288:8080`)
   * egov-mdms to 8082 (for e.g. `kubectl port-forward egov-mdms-service-c9d4877d7-kd4zp 8082:8080`)

3\. Run birth-registration-service that we just created.

4\. Import the postman collection of the API’s that this sample service exposes from here -

[Birth Registration Postman Collection](https://www.getpostman.com/collections/3084ba7dea58547bf07e)

5\. Setup environment variables in Postman:

* hostWithPort - Eg. yourserver.digit.org:8080 or yourserver.digit.org if the service is running on port 80.&#x20;
* applicationNumber - used in the search/update requests to search for that specific application number. Set it post the create birth registration application call.&#x20;

If no workflow has been configured, run the scripts to configure and search for workflow. Double check ID gen by running the ID gen script.

a. Hit the \_create API request to create a voter registration application.

b. Hit the \_search API request to search for the created voter registration applications.

c. Hit \_update API request to update your application or transition it further in the workflow by changing the actions.

_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
