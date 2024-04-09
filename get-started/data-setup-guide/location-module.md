---
description: Setting up boundary hierarchies for tenants
---

# Location Module

## Overview

The location module serves the boundary hierarchies for a tenant. Location is defined separately for every tenant (mostly ULBs) in DIGIT. Each tenant has a unique tenantId.

## Steps

The tenantId key can be a combination of `state` or `state.city` or `state.city.ulb`. The hierarchyType can be one of Revenue, Admin or Election. Multiple hierarchy types can be defined for the same city tenant.

{% code lineNumbers="true" %}
```
{
 "tenantId": "pb.amritsar",
 "moduleName": "egov-location",
 "TenantBoundary": [
   {
     "hierarchyType": {
       "code": "REVENUE",
       "name": "REVENUE"
     },
     "boundary": {
       "id": 1,
       "boundaryNum": 1,
       "name": "Amritsar",
       "localname": "Amritsar",
       "longitude": null,
       "latitude": null,
       "label": "City",
       "code": "pb.amritsar",
       "children":[
         {
```
{% endcode %}

The entire hierarchy can be defined in a nested way as children. One sample of location data for the Amritsar ULB is [available here](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/amritsar/egov-location/boundary-data.json).&#x20;

Location data is stored in GitHub as part of MDMS. The `egov-location` folder needs to be created inside the city tenant (see Amritsar example above). It is stored in the following format:

```
Module name: egov-location (folder) 
Master name: TenantBoundary (key)
```

## Data Setup&#x20;

Enter the boundary hierarchy data in the `<tenant>/egov-location/boundary-data.json` file in the appropriate branch of your forked MDMS repository. For example - if you want changes to be visible in the Dev environment, add the data in the DEV branch of the MDMS repository.&#x20;

{% hint style="info" %}
Follow the Git flow processes to ensure high-quality data. Make sure the PR requests are raised, verified and merged especially where multiple people are working on the same branch.
{% endhint %}

Restart the MDMS service in your environment once the new data is available in the desired branch.

### Boundary Localization

Users also need to upsert localisation codes for any new boundary data in MDMS. Else, users see the label names (auto-generated) for the city names in the UI. Check the [Localisation Data Setup](localisation-module.md) guide for more information on how to perform localisation.&#x20;

The localisation code should follow the following format - \*_tenantId\*\_\*moduleName\*\_\*hierarchyType\*\_\*cityCode\*\_\*zoneCode\*\_\*blockCode\*\_\*areaCode_

For example, to find the localisation code for "Ajitnagar area 1", assuming tenantId as "pb" and hierarchyType as "Revenue":

1. moduleName: EGOV-LOCATION
2. cityCode: PB.AMRITSAR
3. zoneCode: Z1
4. blockCode: B1
5. areaCode: SUN04

So finally the localisation label code for "Ajitnagar area 1" would be PB\_EGOV-LOCATION\_REVENUE\_PB.AMRITSAR\_Z1\_B1\_SUN04 (visible in the UI if no localisation is present).&#x20;
