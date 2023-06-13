---
description: UI configuration for the application
---

# UI Configuration (DevOps)

## **Overview**

This page provides details about the Digit UI configuration required to enable it in any environment

### **DevOps Configuration**

#### **Build Configuration**

{% hint style="info" %}
eGov recommends [CD/CI be set up](https://urban.digit.org/installation/jenkins-setup) before developing on top of DIGIT. This ensures that new modules can be developed and deployed in a streamlined way. DIGIT ships with CI as code as part of the DevOps repository. Please run the [CI installer to setup DIGIT CD/CI](https://urban.digit.org/installation/jenkins-setup) prior to developing on DIGIT.&#x20;
{% endhint %}

**Step 1:** Add entry in build-config.yaml file in the **master** branch of the forked repository. This will set up the job pipeline in Jenkins. Make sure to also add the same config to the feature branch you are working on.\
Refer  [build-config.yaml](https://github.com/egovernments/DIGIT-OSS/blob/6faf040bfecdc9b023e5578adf1e8c3480c8458b/build/build-config.yml#L734)

add the following content for digit-ui

```yaml
  - name: builds/digit-dev/frontend/micro-ui/digit-ui
    build:
      - work-dir: frontend/micro-ui/
        dockerfile: frontend/micro-ui/web/docker/Dockerfile
        image-name: digit-ui
```

**Step 2:** Go to the Jenkins build the page, select "Job Builder" and click on "Build now". This will pull the config from build\_config.yaml and identify all modules that need to be built.&#x20;

**Step 3**: Once the build is done, go to your Jenkins build page. The service will appear under the repository path in which it has been added, i.e. if the service is added under frontend, it will show up in the frontend section as below,



<figure><img src="../../../.gitbook/assets/Screenshot 2023-06-13 at 12.10.44 PM.png" alt=""><figcaption><p>build ui docker image from jenkins</p></figcaption></figure>

&#x20;**To know more about** [**Build**](https://core.digit.org/guides/developer-guide/ui-developer-guide/build-and-deploy#build) **and** [**deployment**](https://core.digit.org/guides/developer-guide/ui-developer-guide/build-and-deploy#deploy) **process visit**&#x20;

{% content-ref url="build-and-deploy.md" %}
[build-and-deploy.md](build-and-deploy.md)
{% endcontent-ref %}

#### **Helmchart Configuration**

**Step 1:** Add an entry in the helm chart of the frontend directory in the **master** branch of the forked [DIGIT-DevOps](https://github.com/egovernments/DIGIT-DevOps) repository.&#x20;

deploy-as-code/helm/charts/frontend/digit-ui

[Reference Directory](https://github.com/egovernments/DIGIT-DevOps/tree/master/deploy-as-code/helm/charts/frontend/digit-ui)

#### **Environment Configuration**

In the DevOps repository of your organization, locate the following `"deploy-as-code/helm/environments/works-dev.yaml"`. Inside the environment YAML file used to deploy the Works platform, please add the following block of code:   &#x20;

<pre class="language-yaml"><code class="lang-yaml"><strong>digit-ui:
</strong>  custom-js-injection: |
    sub_filter.conf: "
      sub_filter  '&#x3C;head>' '&#x3C;head>
      &#x3C;script src={{INSERT_YOUR_AWS_BUCKET_NAME}}/globalConfigs.js type=text/javascript>&#x3C;/script>';"
</code></pre>

A dev environment sample file is linked [here](https://github.com/egovernments/DIGIT-DevOps/blob/efaf8d4335995d2c46c136d06a04e4ea2c2ef581/deploy-as-code/helm/environments/uat.yaml#L430). Note that you will have to modify this for your deployment.

### **GlobalConfig**&#x20;

This section contains a config that is applicable globally to all UI modules. These need to be configured prior to service-specific UI configurations.

#### Steps to create a globalconfig.js file:

* Create a config file(globalconfigs.js) with the below-mentioned config (see code below).
* Configure all the images/logo required in the S3 and add links as footerBWLogoURL , footerLogoURL
* Mention the state tenant ID as stateTenantId
* If any User roles have to be made invalid add as invalidEmployeeRoles
* Then push this global config file into your S3 bucket as globalconfigs.js\

* Mention the globalconfig file URL into your [`Environment config`](ui-configuration-devops.md#environment-configuration)&#x20;

```
var globalConfigs = (function () {
  var stateTenantId = '<<INSERT_STATE_TENANT_ID>>'
  var gmaps_api_key = '<<INSERT_GMAP_GENERATED_TOKEN>>';
  var centralInstanceEnabled = false;
  var footerBWLogoURL = '{{INSERT_YOUR_AWS_BUCKET_NAME}}/digit-footer-bw.png';
  var footerLogoURL = '{{INSERT_YOUR_AWS_BUCKET_NAME}}/digit-footer.png';
  var digitHomeURL = 'https://www.digit.org/'
  var assetS3Bucket = '{{INSERT_YOUR_AWS_BUCKET_NAME}}';
  var invalidEmployeeRoles = ["CBO_ADMIN","STADMIN","ORG_ADMIN","ORG_STAFF"] 
  var configModuleName = 'commonMuktaUiConfig'; 

   var getConfig = function (key) {
     if (key === 'STATE_LEVEL_TENANT_ID') {
       return stateTenantId;
     }
     else if (key === 'GMAPS_API_KEY') {
       return gmaps_api_key;
     }
     else if (key === 'ENABLE_SINGLEINSTANCE') {
       return centralInstanceEnabled;
     } else if (key === 'DIGIT_FOOTER_BW') {
       return footerBWLogoURL;
     } else if (key === 'DIGIT_FOOTER') {
       return footerLogoURL;
     } else if (key === 'DIGIT_HOME_URL') {
       return digitHomeURL;
     } else if (key === 'S3BUCKET') {
       return assetS3Bucket;
     } else if (key === 'CONTEXT_PATH'){
	return contextPath;
     } else if (key === 'UICONFIG_MODULENAME'){
	return configModuleName;
     } else if (key === 'INVALIDROLES'){
	return invalidEmployeeRoles;
     }
   };
 
 
   return {
     getConfig
   };
 }());

```

#### Configure AWS S3 Bucket

The S3 bucket has to be configured by the DevOps team, to store all the assets being used in the Application like Logos, globalConfigs, etc.

Steps Creating a New AWS Bucket

1. Create a new AWS S3 Bucket&#x20;
2. Update the Bucket Policy with the following content, to make the bucket public \


```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::works-dev-asset/*"
        }
    ]
}
```

3. Update the Cross-origin resource sharing (CORS) configuration with the following content

```json
[
    {
        "AllowedHeaders": [
            "*"
        ],
        "AllowedMethods": [
            "GET",
            "PUT",
            "POST",
            "DELETE"
        ],
        "AllowedOrigins": [
            "*"
        ],
        "ExposeHeaders": [
            "x-amz-server-side-encryption",
            "x-amz-request-id",
            "x-amz-id-2"
        ],
        "MaxAgeSeconds": 3000
    }
]
```

4. To proxy the Same Bucket in any environment make the below change in the environment configuration in the DevOps repo ie [environment.yaml](https://github.com/egovernments/DIGIT-DevOps/blob/master/deploy-as-code/helm/environments/uat.yaml#LL48C11-L48C12)\
   In the configmaps, under egov-config ->  data:

&#x20;      add the `s3-assets-bucket: "pg-egov-assets"`

```
 configmaps:
    egov-config:
      data:
        s3-assets-bucket: "(pg-egov-assets|egov-playground-assets|egov-uat-assets)"
```

5. After adding the proxy in the enironment file, restart the `s3-proxy` build in the environment with config enabled.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-06-13 at 12.56.30 PM.png" alt=""><figcaption><p>Sample S3 Bucket with Public access</p></figcaption></figure>
