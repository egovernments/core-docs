# Indexer Configuration

## Overview

Indexer uses a config file per module to store all the configurations pertaining to that module. The Indexer reads multiple such files at start-up to support indexing for all the configured modules. In config, we define source and, destination elastic search index names, custom mappings for data transformation and mappings for data enrichment.&#x20;

## Sample Configuration

Below is the sample configuration for indexing TL application creation data into elastic search.

{% code lineNumbers="true" %}
```
ServiceMaps:
  serviceName: Trade License
  version: 1.0.0
  mappings:
  - topic: save-tl-tradelicense
    configKey: INDEX
    indexes:
    - name: tlindex-v1
      type: licenses
      id: $.id, $.tenantId
      isBulk: true
      timeStampField: $.auditDetails.createdTime
      jsonPath: $.Licenses
      customJsonMapping:
        indexMapping: {"Data":{"tradelicense":{},"ward":{},"tenantData":{}, "history":{}}}
        fieldMapping:
        - inJsonPath: $
          outJsonPath: $.Data.tradelicense
        externalUriMapping:
        - path: http://egov-location.egov:8080/egov-location/location/v11/boundarys/_search
          queryParam: hierarchyTypeCode=REVENUE,boundaryType=locality,codes=$.tradeLicenseDetail.address.locality.code,tenantId=$.tenantId
          apiRequest: {"RequestInfo":{"apiId":"org.egov.pt","ver":"1.0","ts":1502890899493,"action":"asd","did":"4354648646","key":"xyz","msgId":"654654","requesterId":"61","authToken":"d9994555-7656-4a67-ab3a-a952a0d4dfc8","userInfo":{"id":1,"uuid":"1fec8102-0e02-4d0a-b283-cd80d5dab067","type":"EMPLOYEE","tenantId":"pb.amritsar","roles":[{"name":"Employee","code":"EMPLOYEE","tenantId":"pb.amritsar"}]}}}
          uriResponseMapping:
          - inJsonPath: $.TenantBoundary[0].boundary[0]
            outJsonPath: $.Data.ward
        - path: http://egov-workflow-v2.egov:8080/egov-workflow-v2/egov-wf/process/_search
          queryParam: businessIds=$.applicationNumber,history=true,tenantId=$.tenantId
          apiRequest: {"RequestInfo":{"apiId":"org.egov.pt","ver":"1.0","ts":1502890899493,"action":"asd","did":"4354648646","key":"xyz","msgId":"654654","requesterId":"61","authToken":"d9994555-7656-4a67-ab3a-a952a0d4dfc8","userInfo":{"id":1,"uuid":"1fec8102-0e02-4d0a-b283-cd80d5dab067","type":"EMPLOYEE","tenantId":"pb.amritsar","roles":[{"name":"Employee","code":"EMPLOYEE","tenantId":"pb.amritsar"}]}}}
          uriResponseMapping:
          - inJsonPath: $.ProcessInstances
            outJsonPath: $.Data.history
        mdmsMapping:
        - path: http://egov-mdms-service.egov:8080/egov-mdms-service/v1/_search
          moduleName: tenant
          masterName: tenants
          tenantId: pb
          filter: "[?(@.code == $tenant)]"
          filterMapping:
          - variable: $tenant
            valueJsonpath: $.tenantId
          uriResponseMapping:
          - inJsonPath: $.MdmsRes.tenant.tenants
            outJsonPath: $.Data.tenantData
```
{% endcode %}

## **Variable List** <a href="#hardbreak-the-configuration-file-contains-following-keys" id="hardbreak-the-configuration-file-contains-following-keys"></a>

The table below lists the key configuration variables.

<table><thead><tr><th width="199">Variable Name</th><th>Descriptions</th></tr></thead><tbody><tr><td>serviceName</td><td>Name of the module to which this configuration belongs.</td></tr><tr><td>summary</td><td>Summary of the module.</td></tr><tr><td>version</td><td>Version of the configuration.</td></tr><tr><td>mappings</td><td>List of definitions within the module. Every definition corresponds to one index requirement. Which means, every object received onto the kafka queue can be used to create multiple indexes, each of these indexes will need configuration, all such configurations belonging to one topic forms one entry in the mappings list. The keys listed henceforth together form one definition and multiple such definitions are part of this mappings key.</td></tr><tr><td>topic</td><td>The topic on which the data is to be received to activate this particular configuration.</td></tr><tr><td>configKey</td><td>Key to identify to what type of job is this config for. values: INDEX, REINDEX, LEGACYINDEX. INDEX: LiveIndex, REINDEX: Reindex, LEGACYINDEX: LegacyIndex.</td></tr><tr><td>indexes</td><td>Key to configure multiple index configurations for the data received on a particular topic. Multiple indexes based on a different requirement can be created using the same object.</td></tr><tr><td>name</td><td>Index name on the elastic search. (Index will be created if it doesn't exist with this name.)</td></tr><tr><td>type</td><td>Document type within that index to which the index json has to go. (Elasticsearch uses the structure of index/type/docId to locate any file within index/type with id = docId)</td></tr><tr><td>id</td><td>Takes comma-separated JsonPaths. The JSONPath is applied on the record received on the queue, the values hence obtained are appended and used as ID for the record.</td></tr><tr><td>isBulk</td><td>Boolean key to identify whether the JSON received on the Queue is from a Bulk API. In simple words, whether the JSON contains a list at the top level.</td></tr><tr><td>jsonPath</td><td>Key to be used in case of indexing a part of the input JSON and in case of indexing a custom json where the values for custom json are to be fetched from this part of the input.</td></tr><tr><td>timeStampField</td><td>JSONPath of the field in the input which can be used to obtain the timestamp of the input.</td></tr><tr><td>fieldsToBeMasked</td><td>A list of JSONPaths of the fields of the input to be masked in the index.</td></tr><tr><td>customJsonMapping</td><td>Key to be used while building an entirely different object using the input JSON on the queue</td></tr><tr><td>indexMapping</td><td>A skeleton/mapping of the JSON that is to be indexed. Note that, this JSON must always contain a key called "Data" at the top-level and the custom mapping begins within this key. This is only a convention to smoothen dashboarding on Kibana when data from multiple indexes have to be fetched for a single dashboard.</td></tr><tr><td>fieldMapping</td><td>Contains a list of configurations. Each configuration contains keys to identify the field of the input JSON that has to be mapped to the fields of the index json which is mentioned in the key 'indexMapping' in the config.</td></tr><tr><td>inJsonPath</td><td>JSONPath of the field from the input.</td></tr><tr><td>outJsonPath</td><td>JSONPath of the field of the index json.</td></tr><tr><td>externalUriMapping</td><td>Contains a list of configurations. Each configuration contains keys to identify the field of the input JSON that is to be enriched using APIs from the external services. The configuration for those APIs also is a part of this.</td></tr><tr><td>path</td><td>URI of the API to be used. (it should be POST/_search API.)</td></tr><tr><td>queryParam</td><td>Configuration of the query params to be used for the API call. It is a comma-separated key-value pair, where the key is the parameter name as per the API contract and value is the JSONPath of the field to be equated against this parameter.</td></tr><tr><td>apiRequest</td><td>Request Body of the API. (Since we only use _search APIs, it should be only RequestInfo.)</td></tr><tr><td>uriResponseMapping</td><td>Contains a list of configuration. Each configuration contains two keys: One is a JSONPath to identify the field from response, Second is also a JSONPath to map the response field to a field of the index json mentioned in the key 'indexMapping'.</td></tr><tr><td>mdmsMapping</td><td>Contains a list of configurations. Each configuration contains keys to identify the field of the input JSON that is to be denormalized using APIs from the MDMS service. The configuration for those MDMS APIs also is a part of this.</td></tr><tr><td>path</td><td>URI of the API to be used. (it should be POST/_search API.)</td></tr><tr><td>moduleName</td><td>Module Name from MDMS.</td></tr><tr><td>masterName</td><td>Master Name from MDMS.</td></tr><tr><td>tenantId</td><td>Tenant id to be used.</td></tr><tr><td>filter</td><td>Filter to be applied to the data to be fetched.</td></tr><tr><td>filterMapping</td><td>Maps the field of input json to variables in the filter</td></tr><tr><td>variable</td><td>Variable in the filter</td></tr><tr><td>valueJsonpath</td><td>JSONPath of the input to be mapped to the variable.</td></tr></tbody></table>
