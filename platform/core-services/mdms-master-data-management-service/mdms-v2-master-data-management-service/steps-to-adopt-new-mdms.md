# Steps to adopt new MDMS

Follow the steps below to adopt the new MDMS -

1. Define the schema for the master that you want to promote to MDMS v2.
2. Ensure that the schema has a unique field (a unique field can also be composite) which enforces the data being added against that schema.
3. If the data does not have the scope for having unique identifiers e.g. complex masters like - [https://github.com/egovernments/health-campaign-mdms/blob/QA/data/default/health/project-task-configuration.json](https://github.com/egovernments/health-campaign-mdms/blob/QA/data/default/health/project-task-configuration.json) - consider adding a redundant field which can serve as the unique identifier.
4. Hit the following API endpoint to create schema in the system - _/mdms-v2/schema/v1/\_create_
5. Now that the schema has been created, verify the created schema by searching for it using the following API endpoint - _/mdms-v2/schema/v1/\_search_
6. Once the schema is in place, data can be created against the created schema using the following API endpoint - _/mdms-v2/v2/\_create/{schemaCode}_
7. Once the data is created, data can be verified by searching it by using the following API endpoint - _/mdms-v2/v2/\_search_
