# Adopt New MDMS - Steps

Follow the steps below to adopt the new MDMS -

1. Define the schema for the master that you want to promote to MDMS v2.
2. Ensure that the schema has a unique field (a unique field can also be composite) to enforce data integrity.
3. In case the data does not have unique identifiers e.g. complex masters like the one [mentioned here](https://github.com/egovernments/health-campaign-mdms/blob/QA/data/default/health/project-task-configuration.json), consider adding a redundant field which can serve as the unique identifier.
4. Use the following API endpoint to create a schema - _/mdms-v2/schema/v1/\_create_
5. Search and verify the created schema using the following API endpoint - _/mdms-v2/schema/v1/\_search_
6. Once the schema is in place, add the data using the following API endpoint - _/mdms-v2/v2/\_create/{schemaCode}_
7. Verify the data by using the following API endpoint - _/mdms-v2/v2/\_search_
