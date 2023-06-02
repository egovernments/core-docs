---
description: UI configuration for the application
---

# UI Configuration

## **Overview**

This page provides details about the MuktaSoft UI configuration required to enable it in any environment

### **DevOps Configuration**

In the DevOps repository of your organization, locate the following `"deploy-as-code/helm/environments/works-dev.yaml"`. Inside the environment YAML file used to deploy the Works platform, please add the following block of code:

```

works-ui:
  custom-js-injection: |
    sub_filter.conf: "
      sub_filter  '<head>' '<head>
      <script src={{INSERT_YOUR_AWS_BUCKET_NAME}}/globalConfigsWorks.js type=text/javascript></script>';"
      
```

A dev environment sample file is linked [here](https://github.com/egovernments/DIGIT-DevOps/blob/8f80d072be92a8a3cbcac438ca3abdd5e999d17b/deploy-as-code/helm/environments/works-dev.yaml#L587). Note that you will have to modify this for your deployment.

### **GlobalConfig**&#x20;

This section contains a config that is applicable globally to all UI modules. These need to be configured prior to service specific UI configurations.

#### Steps to create a globalconfig.js file:

* Create a config file(globalconfigs.js) with the below-mentioned config (see code below).
* Configure all the images/logo required in the S3 and add links as footerBWLogoURL , footerLogoURL
* Mention the state tenant ID as stateTenantId
* If any User roles have to be made invalid add as invalidEmployeeRoles
* Then push this global config file into your S3 bucket as globalconfigs.js
* Mention the globalconfig file URL into your [`Environment config`](ui-configuration.md#devops-configuration)&#x20;



```
var globalConfigs = (function () {
      var stateTenantId = 'pg'
      var gmaps_api_key = '<<INSERT_GMAP_GENERATED_TOKEN>>';
      var finEnv = 'uat'
      var centralInstanceEnabled = false;
      var footerBWLogoURL = '{{INSERT_YOUR_AWS_BUCKET_NAME}}/digit-footer-bw.png';
      var footerLogoURL = '{{INSERT_YOUR_AWS_BUCKET_NAME}}/digit-footer.png';
      var digitHomeURL = 'https://www.digit.org/'
      var assetS3Bucket = '{{INSERT_YOUR_AWS_BUCKET_NAME}}';


      var getConfig = function (key) {
        if (key === 'STATE_LEVEL_TENANT_ID') {
          return stateTenantId;
        }
        else if (key === 'GMAPS_API_KEY') {
          return gmaps_api_key;
        }
        else if (key === 'FIN_ENV') {
          return finEnv;
        } else if (key === 'ENABLE_SINGLEINSTANCE') {
          return centralInstanceEnabled;
        } else if (key === 'DIGIT_FOOTER_BW') {
          return footerBWLogoURL;
        } else if (key === 'DIGIT_FOOTER') {
          return footerLogoURL;
        } else if (key === 'DIGIT_HOME_URL') {
          return digitHomeURL;
        } else if (key === 'S3BUCKET') {
          return assetS3Bucket;
        } else if (key === "JWT_TOKEN"){
          return "ZWdvdi11c2VyLWNsaWVudDo=";
        }
      };


      return {
        getConfig
      };
}());
```
