# API Checklist

## APIs - The Do's & Don'ts

The APIs developed on DIGIT adhere to specific conventions and principles. Below are the dos and don'ts to be observed when following these API principles.

1. Always define the Yaml for your APIs as the first thing using Open API 3 Standard ([https://swagger.io/specification/](https://swagger.io/specification/)).
2. APIs path should be standardised as follows:
   * **/{service}/{entity}/{version}/\_create**: This endpoint should be used to create the entity.
   * **/{service}/{entity}/{version}/\_update**: This endpoint should be used to edit an entity which is already existing.
   * **/{service}/{entity}/{version}/\_search**: This endpoint should be used to provide a search on the entity based on certain criteria.
   * **/{service}/{entity}/{version}/\_count**: This endpoint should be provided to give a count of entities that match the given search criteria.
3. Always use POST for each of the endpoints.
4. Take most search parameters in the POST body only.
5. If query params for search need to be supported then make sure to have the same parameters in the POST body also and the POST body should take priority over query params.
6. Provide additional detail for objects in **\_create** and **\_update** APIs so that custom requirements can use these fields.
7. Each API should have a [**RequestInfo**](https://github.com/egovernments/core-services/blob/4e92620bd77fce183fdd66d3a8d9248f65561ada/docs/common-contract.yml#L45) object in the request body at the top level.
8. Each API should have a [**ResponseInfo**](https://github.com/egovernments/core-services/blob/4e92620bd77fce183fdd66d3a8d9248f65561ada/docs/common-contract.yml#L154) object in the response body at the top level.
9. Mandatory fields should be the minimum for the APIs.
10. minLength and maxLength should be defined for each attribute.
11. Read-only fields should be called out.
12. Use common models already available in the platform in your APIs. Example -
    * [Address](https://github.com/egovernments/core-services/blob/4e92620bd77fce183fdd66d3a8d9248f65561ada/docs/common-contract.yml#L228)
    * [User](https://github.com/egovernments/core-services/blob/4e92620bd77fce183fdd66d3a8d9248f65561ada/docs/common-contract.yml#L96) (Citizen/ Employee/ Owner)
    * [Role](https://github.com/egovernments/core-services/blob/4e92620bd77fce183fdd66d3a8d9248f65561ada/docs/common-contract.yml#L130)
    * [AuditDetails](https://github.com/egovernments/core-services/blob/4e92620bd77fce183fdd66d3a8d9248f65561ada/docs/common-contract.yml#L270)
    * [ErrorRes](https://github.com/egovernments/core-services/blob/4e92620bd77fce183fdd66d3a8d9248f65561ada/docs/common-contract.yml#L213) (Response sent in case of errors)
    * TODO: Add all the models here
13. For receiving files in an API, do not use binary file data. Instead, accept the file store ids.
14. If there is only one file to be uploaded and no persistence is needed, and no additional JSON data is to be posted, you can consider using direct file upload instead of using filestore id.
