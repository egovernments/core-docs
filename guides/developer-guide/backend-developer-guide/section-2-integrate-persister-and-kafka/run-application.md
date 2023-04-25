# Run Application

We have completed integration with key services and we can now test out the REST APIs we have built.

**Steps:** To run and test our sample application, follow the steps below.

1. Ensure that Kafka and Persister are running in the local environment.
2. Run birth-registration-service that we just created.
3. Import the postman collection of the APIs that this sample service exposes from here: [Birth Registration Postman Collection](https://www.getpostman.com/collections/3084ba7dea58547bf07e)

Test the following APIs:

a. Hit the \_create API request to create a birth registration application. You should see entries in the local database.

b. Hit the \_search API request to search for the created birth registration applications.

c. Hit \_update API request to update your application by changing the baby's firstName field. You should be able to see the updates in the DB.
