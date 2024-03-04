# Inbox Service

## Overview

The inbox service is an event-based service that fetches pre-aggregated data of municipal services and workflow performs complex search operations and returns applications and workflow data in a paginated manner. The service also returns the total count matching the search criteria.

## Sample Configuration

The first step is to capture pre-aggregated events for the module which needs to be enabled in event-based inbox. This index needs to hold all the fields against which a search needs to be performed and any other fields which need to be shown in the UI when applications are listed.

Now, this service allows to search both the module objects as well as `processInstance`(Workflow record) based on the provided criteria for any of the municipal services. For this, it uses a module-specific configuration. A sample configuration is given below -

```json
{
  "tenantId": "pb",
  "moduleName": "INBOX",
  "InboxQueryConfiguration": [
    {
      "module": "WS",
      "index": "ws-inbox-test",
      "allowedSearchCriteria": [
        {
          "name": "tenantId",
          "path": "Data.tenantId.keyword",
          "isMandatory": true,
          "operator": "EQUAL"
        },
        {
          "name": "status",
          "path": "Data.currentProcessInstance.state.uuid.keyword",
          "isMandatory": false
        },
        {
          "name": "mobileNumber",
          "path": "Data.mobileNumberHash.keyword",
          "isMandatory": false,
          "isHashingRequired": true
        },
        {
          "name": "locality",
          "path": "Data.locality.keyword",
          "isMandatory": false
        },
        {
          "name": "assignee",
          "path": "Data.workflow.assignes.keyword",
          "isMandatory": false
        },
        {
          "name": "applicationNumber",
          "path": "Data.applicationNo.keyword",
          "isMandatory": false
        },
        {
          "name": "fromDate",
          "path": "Data.auditDetails.createdTime",
          "isMandatory": false,
          "operator": "GTE"
        },
        {
          "name": "toDate",
          "path": "Data.auditDetails.createdTime",
          "isMandatory": false,
          "operator": "LTE"
        }
      ],
      "sortBy": {
          "path": "Data.additionalDetails.appCreatedDate",
          "defaultOrder": "ASC"
      },
      "sourceFilterPathList": ["Data.currentProcessInstance", "Data.auditDetails", "Data.additionalDetails", "Data.tenantId", "Data.proposedTaps","Data.applicationNo","Data.workflow","Data.locality"]
    }
  ]
}
```

Inside each query configuration object, we have the following keys -

* `module` - Module code for which inbox has been configured.
* `index` - Index where pre-aggregated events are stored.
* `allowedSearchCriteria` - This lists out various parameters on which searching is allowed for the given module
* `sortBy` - Specifies the field path inside the pre-aggregated record present in the index against which the result has to be sorted. Default order can be specified to `ASC` or `DESC` .
* `sourceFilterPathList` - This is a list which specifies the fields which should appear and which should not appear as part of the search result in order to avoid clutter and to improve query performance.
* &#x20;`allowedSearchCriteria` - Within each object is going to have the following keys -
  * `name` - Name of the incoming search parameter in the inbox request body.
  * `path` - Path inside the pre-aggregated record present in the index against which the incoming search parameter needs to be matched.
  * `isMandatory` - This specifies whether a particular parameter is mandatory to be sent in inbox search request or not.
  * `operator` - This specifies which operator clause needs to be applied while forming ES queries. Currently, we support equality and range comparison operators only.

\
A new inbox service needs to be enabled via the configuration present in MDMS. The path to the MDMS configuration is - [https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/inbox-v2/InboxConfiguration.json](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/inbox-v2/InboxConfiguration.json).

Once the configuration is added to this MDMS file, the MDMS service for that particular environment has to be restarted.

### **Migrating To An Event-based Inbox**&#x20;

If any existing module needs to be migrated onto a new inbox, data needs to be [reindexed](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/888963174/Indexer+Service), and configuration like the above needs to be written to enable these modules on the new inbox.

* For modules where search has to be given on PII data like mobile number, a migration API needs to be written which will fetch data from the database, decrypt it, hash it using the encryption client and store it in the index to enable search.
* For modules where a search has to be given on non-PII data, the indexer service’s \_legacyIndex API can be invoked to move data to the new index.
