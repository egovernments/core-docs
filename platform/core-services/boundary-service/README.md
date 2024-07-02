# Boundary Service

## Overview

Boundary service provides APIs to create Boundary entities, define their hierarchies, and establish relationships within those hierarchies. You can search for boundary entities, hierarchy definitions, and boundary relationships. However, you can only update boundary entities and relationships.

## Pre-requisites

1. Prior knowledge of Java/J2EE.
2. Prior knowledge of Spring Boot.
3. Prior knowledge of REST APIs and related concepts like path parameters, headers, JSON etc.
4. Prior knowledge of Git.
5. Advanced knowledge of operating JSON data would be an added advantage to understanding the service.

## Key Functionalities

1. **Create Boundary entity**: It introduces functionality to define your boundary entity with all validations and properties supported by GeoJson. Currently, only the geometry type of _Polygon_ and _Point_ is supported by it.
2. **Search Boundary entity**: It has APIs to search boundaries based on the tenantid & codes, both being mandatory.
3. **Update Boundary entity**: This allows updating the geometry details of a boundary entity.
4. **Create Boundary Hierarchy-definition**: It allows defining boundary hierarchy definitions against a particular _tenantId_ and _hierarchyType_ which then can be referenced while creating boundary relationships.
5. **Search Boundary Hierarchy-definition**: boundary-service supports searching for hierarchy definitions based on tenantId and HierarchyType where tenantId is mandatory. In case the hierarchyType is not provided, it returns all hierarchy definitions for the given tenantId.
6. **Create Boundary Relationship**: It supports defining relationships between existing boundary entities according to the established hierarchy. It requires tenantId, code, hierarchyType, boundaryType, and parent fields. Where **tenantId and code** uniquely combine to determine a boundary entity, **tenantId and hierarchType** combine to define the hierarchy used in establishing the relationship between the boundary entity and its parent.\
   It verifies if the parent relationship is already established before creating a new one. It also checks if the specified boundaryType is a direct descendant of the parent boundaryType according to the hierarchy definition.
7. **Search Boundary Relationship**: This functionality supports searching the boundary relationships based on the given params -
   1. tenantId
   2. hierarchyType
   3. boundaryType
   4. codes
   5. includeChildren
   6. includeParents

where tenantId and hierarchyType are mandatory and the rest are optional.

8. **Update Boundary Relationship**: This allows updating the parent boundary relationship within the same level as per the hierarchy.

## API Details

1. _/boundary/\_create_ - Takes `RequestInfo` and `Boundary` in the request body. boundary has all attributes which define the boundary.
2. _/boundary/\_search_ - Takes `RequestInfo` in the request body and search criteria fields (refer to the functionality above for exact fields ) as `params` and return the boundary based on the provided search criteria.
3. _/boundary/\_update_ - Takes `RequestInfo` and `Boundary` in the request body where the boundary has all the info that needs to be updated and returns the updated boundary.
4. _/boundary-hierarchy-definition/\_create_ - Takes `RequestInfo` and boundary hierarchy definition in the request body where `BoundaryHierarchy` object has all the information for the hierarchy definition being created.
5. _/boundary-hierarchy-definition/\_search_ - Takes `RequestInfo` and `BoundaryTypeHierarchySearchCriteria` in the request body to return boundary hierarchy definition based on the provided search criteria.
6. _/boundary-relationships/\_create_ - This API takes `RequestInfo` and `BoundaryRelationship` in the request body where `BoundaryRelationship` has all the info required to define a relationship between two boundaries.
7. _/boundary-relationships/\_search_ - This API takes `RequestInfo` in the request body and search criteria fields (refer to functionality for the exact fields) are passed as `params` to return master data based on the provided search criteria and return the response.
8. _/boundary-relationships/\_update_ - This API takes `RequestInfo` and `BoundaryRelationship` in the request body to update the fields given in the `BoundaryRelationship` and returns the updated data.

#### Postman Collection for Boundary Service APIs: <a href="#postman-collection-for-boundary-service-apis" id="postman-collection-for-boundary-service-apis"></a>

[https://api.postman.com/collections/20755293-c145daab-6465-49a8-b316-4f56a94f186b?access\_key=PMAT-01HYHWJ5DZJ6VV0BX8HP9R1DBA](https://api.postman.com/collections/20755293-c145daab-6465-49a8-b316-4f56a94f186b?access\_key=PMAT-01HYHWJ5DZJ6VV0BX8HP9R1DBA)

