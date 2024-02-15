# Add Indexer Configuration

## Overview

The indexer is designed to perform all the indexing tasks of the DIGIT platform. The service reads records posted on specific Kafka topics and picks the corresponding index configuration from the yaml file provided by the respective module configuration. Configurations are yaml based. A detailed guide to creating indexer configs is mentioned in the following document - [Indexer Configuration Guide](../../../../platform/api-specifications/indexer.md).

## Steps

1. Create a new file under `egov-indexer` in `configs` repo by the name of `digit-developer-guide.yml` and put the following content into it -

```yaml
ServiceMaps:
  serviceName: Birth Registration Service
  version: 1.0.0
  mappings:
    - topic: save-bt-application
      configKey: INDEX
      indexes:
        - name: btindex-v1
          type: general
          id: $.id
          isBulk: true
          timeStampField: $.auditDetails.createdTime
          jsonPath: $.BirthRegistrationApplications
          customJsonMapping:
            indexMapping: {"Data":{"birthapplication":{},"history":{}}}
            fieldMapping:
              - inJsonPath: $
                outJsonPath: $.Data.birthapplication
            externalUriMapping:
              - path: http://localhost:8282/egov-workflow-v2/egov-wf/process/_search
                queryParam: businessIds=$.applicationNumber,history=true,tenantId=$.tenantId
                apiRequest: {"RequestInfo":{"apiId":"org.egov.pt","ver":"1.0","ts":1502890899493,"action":"asd","did":"4354648646","key":"xyz","msgId":"654654","requesterId":"61","authToken":"d9994555-7656-4a67-ab3a-a952a0d4dfc8","userInfo":{"id":1,"uuid":"1fec8102-0e02-4d0a-b283-cd80d5dab067","type":"EMPLOYEE","tenantId":"pb.amritsar","roles":[{"name":"Employee","code":"EMPLOYEE","tenantId":"pb.amritsar"}]}}}
                uriResponseMapping:
                  - inJsonPath: $.ProcessInstances
                    outJsonPath: $.Data.history

    - topic: update-bt-application
      configKey: INDEX
      indexes:
        - name: btindex-v1
          type: general
          id: $.id
          isBulk: true
          timeStampField: $.auditDetails.createdTime
          jsonPath: $.BirthRegistrationApplications
          customJsonMapping:
            indexMapping: {"Data":{"birthapplication":{},"history":{}}}
            fieldMapping:
              - inJsonPath: $
                outJsonPath: $.Data.birthapplication
            externalUriMapping:
              - path: http://egov-workflow-v2.egov:8080/egov-workflow-v2/egov-wf/process/_search
                queryParam: businessIds=$.applicationNumber,history=true,tenantId=$.tenantId
                apiRequest: {"RequestInfo":{"apiId":"org.egov.pt","ver":"1.0","ts":1502890899493,"action":"asd","did":"4354648646","key":"xyz","msgId":"654654","requesterId":"61","authToken":"d9994555-7656-4a67-ab3a-a952a0d4dfc8","userInfo":{"id":1,"uuid":"1fec8102-0e02-4d0a-b283-cd80d5dab067","type":"EMPLOYEE","tenantId":"pb.amritsar","roles":[{"name":"Employee","code":"EMPLOYEE","tenantId":"pb.amritsar"}]}}}
                uriResponseMapping:
                  - inJsonPath: $.ProcessInstances
                    outJsonPath: $.Data.history
```

<mark style="color:orange;">**Note: Follow the steps below when the code is deployed to the DIGIT environment. These steps are not applicable for deployment in the local environment. You may choose to follow these when you build and deploy.**</mark>&#x20;

### Indexer Configuration Deployment

2. Navigate to the forked DIGIT-DevOps repository. Under the `deploy-as-code/helm/environments` directory, find the deployment helm chart that was used to deploy DIGIT. &#x20;
3. In the deployment helm chart (which was used to set up the DIGIT environment), find "egov-indexer". Find the "egov-indexer-yaml-repo-path" property and add the path to your new indexer file here. The code block is shown below for reference:

```
egov-indexer:
  replicas: 1
  images:
    - egovio/egov-indexer
  db_migration_image: egovio/egov-indexer-db
  initContainers:
    gitSync:
      repo: "git@github.com:egovernments/configs"
      branch: "DEV"
  egov-indexer-yaml-repo-path: "file:///work-dir/configs/egov-indexer/privacy-audit.yaml,file:///work-dir/configs/egov-indexer/billingservices-indexer.yml,file:///work-dir/configs/egov-indexer/collection-indexer.yml,file:///work-dir/configs/egov-indexer/egov-telemetry-indexer.yml,file:///work-dir/configs/egov-indexer/egov-uploader-indexer.yml,file:///work-dir/configs/egov-indexer/error-queue.yml,file:///work-dir/configs/egov-indexer/finance-rolloutadotpion-indexer.yml,file:///work-dir/configs/egov-indexer/payment-indexer.yml,file:///work-dir/configs/egov-indexer/pgr-services.yml,file:///work-dir/configs/egov-indexer/rainmaker-pgr-indexer.yml,file:///work-dir/configs/egov-indexer/rainmaker-pt-indexer.yml,file:///work-dir/configs/egov-indexer/rainmaker-tl-indexer.yml,file:///work-dir/configs/egov-indexer/chatbot-telemetry.yaml,file:///work-dir/configs/egov-indexer/water-service.yml,file:///work-dir/configs/egov-indexer/water-services-meter.yml,file:///work-dir/configs/egov-indexer/sewerage-service.yml,file:///work-dir/configs/egov-indexer/property-services.yml,file:///work-dir/configs/egov-indexer/chatbot-telemetry-v2.yaml,file:///work-dir/configs/egov-indexer/egov-fsm.yaml,file:///work-dir/configs/egov-indexer/egov-vehicle.yaml,file:///work-dir/configs/egov-indexer/egov-vendor.yaml,file:///work-dir/configs/egov-indexer/egov-url-shortening-indexer.yaml,file:///work-dir/configs/egov-indexer/fire-noc-service.yml,file:///work-dir/configs/egov-indexer/egov-echallan.yml,file:///work-dir/configs/egov-indexer/egov-bpa-indexer.yml,file:///work-dir/configs/egov-indexer/edcr-indexer.yml,file:///work-dir/configs/egov-indexer/rainmaker-birth-indexer.yml,file:///work-dir/configs/egov-indexer/rainmaker-death-indexer.yml"

```

4. Raise a PR to the DevOps branch which was forked/used to create the deployment. Once that is merged, restart the indexer service and make sure the cluster configs are propagated.
