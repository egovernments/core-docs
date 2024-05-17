---
description: Configure service to enable fetch and share of location details
---

# Location

## Overview <a href="#overview" id="overview"></a>

A core application that provides location details of the tenant for which the services are being provided.

### API's Playground : [DIGIT-Playground](https://digit-api.apidog.io/doc-507201)&#x20;

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before you proceed with the documentation, make sure the following pre-requisites are met -

* Java 17
* PostgreSQL server is running and the DB is created
  * Follow this guide to see how to [setup and create DB](https://www.cherryservers.com/blog/how-to-install-and-setup-postgresql-server-on-ubuntu-20-04) in postgreSQL.
* Working Knowledge of [egov-mdms](mdms-v2-master-data-management-service/mdms-master-data-management-service/setting-up-master-data/mdms-overview.md) service to add location data in master data.
* egov-mdms service is running and all the required [MDMS masters](mdms-v2-master-data-management-service/mdms-master-data-management-service/setting-up-master-data/configuring-master-data.md) are loaded in it

## Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

* The location information is also known as the boundary data of ULB
* Boundary data can be of different hierarchies - ADMIN or ELECTION hierarchy defined by the Administrators and Revenue hierarchy defined by the Revenue department.
* The election hierarchy has the locations divided into several types like zone, election wards, blocks, streets and localities. The Revenue hierarchy has the locations divided into a zone, ward, block and locality.
* The model which defines the localities like zone, ward and etc is a boundary object which contains information like name, lat, long, parent or children boundary if any. The boundaries come under each other in a hierarchy. For instance, a zone contains wards, a ward contains blocks, and a block contains locality. The order in which the boundaries are contained in each other differs based on the tenants.

| Environment Variables                | Description                                     |
| ------------------------------------ | ----------------------------------------------- |
| `egov.services.egov_mdms.hostname`   | Host name for MDMS service.                     |
| `egov.services.egov_mdms.searchpath` | MDMS Search URL.                                |
| `egov.service.egov.mdms.moduleName`  | MDMS module which contain boundary master.      |
| `egov.service.egov.mdms.masterName`  | MDMS master file which contain boundary detail. |

## Deployment Details

1. Add/Update the MDMS master file which contains boundary data of ULBs.
2. Add Role-Action mapping for the egov-location APIs.
3. Deploy/Redeploy the latest version of the egov-mdms service.
4. Fill the above environment variables in the egov-location with proper values.
5. Deploy the latest version of the egov-location service.

## Configuration Details <a href="#configuration-details" id="configuration-details"></a>

The boundary data has been moved to MDMS from the master tables in DB. The location service fetches the JSON from MDMS and parses it to the structure of the boundary object as mentioned above. A sample master would look like below.

{% code lineNumbers="true" %}
```json
{
  "tenantId": "pg.cityA",
   "moduleName": "egov-location",
  "TenantBoundary": [
  {
      "hierarchyType": {
              "code": "ADMIN",
              "name": "ADMIN"
      },
       "boundary": {
                "id": 1,
                "boundaryNum": 1,
                "name": "CityA",
                "localname": "CityA",
                "longitude": null,
                "latitude": null,
                "label": "City",
                "code": "pg.cityA",
                "children": []
        }

    }
 ]
}
```
{% endcode %}

<table><thead><tr><th width="342">Attribute Name</th><th>Description</th></tr></thead><tbody><tr><td>tenantId</td><td>The tenantId (ULB code) for which the boundary data configuration is defined.</td></tr><tr><td>moduleName</td><td>The name of the module where TenantBoundary master is present.</td></tr><tr><td>TenantBoundary.hierarchyType.name</td><td>Unique name of the hierarchy type.</td></tr><tr><td>TenantBoundary.hierarchyType.code</td><td>Unique code of the hierarchy type.</td></tr><tr><td>TenantBoundary.boundary.id</td><td>Id of boundary defined for particular hierarchy.</td></tr><tr><td>boundaryNum</td><td>Sequence number of boundary attribute defined for the particular hierarchy.</td></tr><tr><td>name</td><td>Name of the boundary like Block 1 or Zone 1 or City name.</td></tr><tr><td>localname</td><td>Local name of the boundary.</td></tr><tr><td>longitude</td><td>Longitude of the boundary.</td></tr><tr><td>latitude</td><td>Latitude of the boundary.</td></tr><tr><td>label</td><td>Label of the boundary.</td></tr><tr><td>code</td><td>Code of the boundary.</td></tr><tr><td>children</td><td>Details of its sub-boundaries.</td></tr></tbody></table>

## Integration Details <a href="#integration" id="integration"></a>

### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

The egov-location APIs can be used by any module which needs to store the location details of the tenant.

### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

* Get the boundary details based on boundary type and hierarchy type within the tenant boundary structure.
* Get the geographical boundaries by providing appropriate GeoJson.
* Get the tenant list in the given latitude and longitude.

### Integration Steps <a href="#steps-to-integration" id="steps-to-integration"></a>

1. To integrate, the host of egov-location should be overwritten in the helm chart.
2. /boundarys/\_search should be added as the search endpoint for searching boundary details based on tenant Id, Boundary Type, Hierarchy Type etc.
3. /geography/\_search should be added as the search endpoint. This method handles all requests related to geographical boundaries by providing appropriate GeoJson and other associated data based on tenantId or lat/long etc.
4. /tenant/\_search should be added as the search endpoint. This method tries to resolve a given lat, long to a corresponding tenant, provided there exists a mapping between the reverse geocoded city to the tenant.
5. The MDMS tenant boundary master file should be loaded in the MDMS service.

## Reference Docs <a href="#reference-docs" id="reference-docs"></a>

### Doc Links

| Title                                                                                                                                  |
| -------------------------------------------------------------------------------------------------------------------------------------- |
| [Local setup](https://github.com/egovernments/core-services/blob/669c94194911ada92b6cb3c87e5fad7a7478cc6a/egov-location/LOCALSETUP.md) |

### API List

| APIs                                                           |
| -------------------------------------------------------------- |
| [/boundarys/\_search](https://digit-api.apidog.io/api-6903255) |
| [/geography/\_search](https://digit-api.apidog.io/api-6829077) |
| [/tenant/\_search](https://digit-api.apidog.io/api-6829078)    |

Please refer to the [Swagger API contract](https://github.com/egovernments/DIGIT-Specs/blob/grouped-service-contracts/Common%20Services/location.yaml) for the location service to understand the structure of APIs and to have a visualisation of all internal APIs.

