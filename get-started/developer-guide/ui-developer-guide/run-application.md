# Run Application

{% tabs %}
{% tab title="Old Folder Structure" %}
## Overview

Once the local setup is completed, the next step is to run the application locally. This document provides the steps on how to run the digit-ui on a local machine.

## Steps

### Configure Environment File

The new folder structure looks something like this: \
![](<../../../.gitbook/assets/image (562).png>)

You can refer this [console branch](https://github.com/egovernments/DIGIT-Frontend/tree/console) to understand the architecture more deeply.

**Step 1:** To run the application in the local environment, add the `.env` file in the web folder -

```
micro-ui/web
```

**Step 2:** Copy the following content and add it to the .env file. If the user is a citizen, configure the .env file as shown below:

```js-templates
SKIP_PREFLIGHT_CHECK=true
REACT_APP_USER_TYPE=EMPLOYEE
REACT_APP_EMPLOYEE_TOKEN=c835932f-2ad4-4d05-83d6-49e0b8c59f8a
REACT_APP_CITIZEN_TOKEN=7cd58aae-30b3-41ed-a1b3-3417107a993c
REACT_APP_PROXY_API=https://unified-dev.digit.org
REACT_APP_PROXY_ASSETS=https://unified-dev.digit.org
REACT_APP_GLOBAL=https://egov-dev-assets.s3.ap-south-1.amazonaws.com/globalConfigsWorkbenchDev.js
```

**Step 3:** To run the application as an employee, update the value of the param to - `REACT_APP_USER_TYPE=EMPLOYEE.`

**Step 4:** To direct the front end to different environments, update the `REACT_APP_GLOBAL` variable and add the GlobalConfig environment file corresponding to that environment.

To learn more about global config visit [How to configure globalconfig](https://core.digit.org/guides/developer-guide/ui-developer-guide/ui-configuration#globalconfig).

Update both `REACT_APP_PROXY_API` and `REACT_APP_PROXY_ASSETS` to the environment URL.

### Initialise & Run Application

Before initializing the frontend app locally, ensure that you are in the specified directory.

```
micro-ui/web
```

**Step 1:** To initialise the Yarn execute the below command -

```
sudo yarn install
```

**Step 2:** Once the yarn initialization is successful execute the below command -

```
sudo yarn run start
```

**Step 3:** Running this command will start the application.

### Login As <a href="#login-as" id="login-as"></a>

There are two types of login -

1. **Employee:** If you log in as an employee, the below screen is displayed.

<figure><img src="../../../.gitbook/assets/4a3187e5-57cc-481e-967e-e1041e300bf4 (1).png" alt=""><figcaption></figcaption></figure>

**HomePage Employee:** Once the employee is logged in, users are redirected to the employee home page.

<figure><img src="../../../.gitbook/assets/f20e9d17-e5cc-4e8f-b2b7-22ad190263df.png" alt=""><figcaption></figcaption></figure>

On the home page, users can see the cards mCollect, HRMS, NOC, Property Tax, etc These cards need to be added. Refer to the instructions on the [link here](run-application.md#configure-environment-file-citizen-1) to create an employee card.

2. **HomePage Citizen:** Once the citizens are logged in successfully, users are redirected to the citizen homepage.

<figure><img src="../../../.gitbook/assets/96fe0433-39bb-4ae9-8a0c-54b21c295ace.png" alt=""><figcaption></figcaption></figure>

#### HomePage Citizen

<figure><img src="../../../.gitbook/assets/5d4cd419-bb70-47fb-976b-c797415d618c.png" alt=""><figcaption></figcaption></figure>

Click on the [link here](run-application.md#configure-environment-file-citizen) to create a card for your module on the home page under "Citizen Services".

### Troubleshoot

Refer to [this](ui-configuration-devops.md#global-configuration) section to learn about globalConfig file.

if you do not have a global config and AWS credentials are not present, then create a temporary local config under the path:

```
micro-ui/web/public/index.html
```

Include this between the head tags

```
 <script>
  var globalConfigs = (function () {
  var stateTenantId = 'dev'
  var gmaps_api_key = 'AIzaSyCslxyiD1nuQuoshbu_E3WkIV8J2SUA6KI';
  var contextPath = 'workbench-ui';
  var configModuleName = 'commonHCMUiConfig';
  var centralInstanceEnabled = false;
  var localeRegion = "IN";
  var localeDefault = "en";
  var mdmsContext = "egov-mdms-service";
  var footerBWLogoURL =
  "https://egov-uat-assets.s3.ap-south-1.amazonaws.com/digit-footer-bw.png";
var footerLogoURL =
  "https://egov-uat-assets.s3.ap-south-1.amazonaws.com/digit-footer.png";
  var digitHomeURL = 'https://www.digit.org/';
  var assetS3Bucket = 'egov-uat-asset';
  var hrmsContext = "health-hrms";
  var projectContext= "health-project";
  var invalidEmployeeRoles = ["CBO_ADMIN", "ORG_ADMIN", "ORG_STAFF", "SYSTEM"]
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
    } else if (key === 'CONTEXT_PATH') {
      return contextPath;
    } else if (key === 'UICONFIG_MODULENAME') {
      return configModuleName;
    } else if (key === "LOCALE_REGION") {
      return localeRegion;
    } else if (key === "LOCALE_DEFAULT") {
      return localeDefault;
    } else if (key === "MDMS_CONTEXT_PATH") {
      return mdmsContext;
    } else if (key === "PROJECT_SERVICE_PATH") {
      return projectContext;
    } else if (key === "HRMS_CONTEXT_PATH") {
      return hrmsContext;
    } else if (key === "MDMS_V2_CONTEXT_PATH") {
      return mdmsContext;
    } else if (key === "MDMS_V1_CONTEXT_PATH") {
      return mdmsContext;
    } if (key === 'INVALIDROLES') {
      return invalidEmployeeRoles;
    }
  };
  return {
    getConfig
  };
}());
    </script>
```
{% endtab %}

{% tab title="New Folder Structure" %}
## Overview

Once the local setup is completed, the next step is to run the application locally. This document provides the steps on how to run the digit-ui on a local machine.

## Steps

### Configure Environment File

**Step 1:** To run the application in the local environment, add the `.env` file in the `example` folder -

```
micro-ui/web/
```

**Step 2:** Copy the following content and add it to the .env file. If the user is a citizen, configure the .env file as shown below:

```js-templates
SKIP_PREFLIGHT_CHECK=true
REACT_APP_USER_TYPE=EMPLOYEE
REACT_APP_EMPLOYEE_TOKEN=c835932f-2ad4-4d05-83d6-49e0b8c59f8a
REACT_APP_CITIZEN_TOKEN=7cd58aae-30b3-41ed-a1b3-3417107a993c
REACT_APP_PROXY_API=https://unified-dev.digit.org
REACT_APP_PROXY_ASSETS=https://unified-dev.digit.org
REACT_APP_GLOBAL=https://egov-dev-assets.s3.ap-south-1.amazonaws.com/globalConfigsWorkbenchDev.js
```

**Step 3:** To run the application as an employee, update the value of the param to - `REACT_APP_USER_TYPE=EMPLOYEE.`

**Step 4:** To direct the front end to different environments, update the `REACT_APP_GLOBAL` variable and add the GlobalConfig environment file corresponding to that environment.

To learn more about global config visit [How to configure globalconfig](https://core.digit.org/guides/developer-guide/ui-developer-guide/ui-configuration#globalconfig).

Update both `REACT_APP_PROXY_API` and `REACT_APP_PROXY_ASSETS` to the environment URL.

### Initialise & Run Application

Before initializing the frontend app locally, ensure that you are in the specified directory.

```
micro-ui/web/
```

**Step 1:** To initialise the Yarn execute the below command -

```
sudo yarn install
```

**Step 2:** Once the yarn initialization is successful execute the below command -

```
sudo yarn run start
```

**Step 3:** Running this command will start the application.

### Login As <a href="#login-as" id="login-as"></a>

There are two types of login -

1. **Employee:** If you log in as an employee, the below screen is displayed.

<figure><img src="../../../.gitbook/assets/4a3187e5-57cc-481e-967e-e1041e300bf4 (1).png" alt=""><figcaption></figcaption></figure>

**HomePage Employee:** Once the employee is logged in, users are redirected to the employee home page.

<figure><img src="../../../.gitbook/assets/f20e9d17-e5cc-4e8f-b2b7-22ad190263df.png" alt=""><figcaption></figcaption></figure>

On the home page, users can see the cards mCollect, HRMS, NOC, Property Tax, etc These cards need to be added. Refer to the instructions on the [link here](run-application.md#configure-environment-file-citizen-1) to create an employee card.

2. **HomePage Citizen:** Once the citizens are logged in successfully, users are redirected to the citizen homepage.

<figure><img src="../../../.gitbook/assets/96fe0433-39bb-4ae9-8a0c-54b21c295ace.png" alt=""><figcaption></figcaption></figure>

#### HomePage Citizen

<figure><img src="../../../.gitbook/assets/5d4cd419-bb70-47fb-976b-c797415d618c.png" alt=""><figcaption></figcaption></figure>

Click on the [link here](run-application.md#configure-environment-file-citizen) to create a card for your module on the home page under "Citizen Services".

### Troubleshoot

Refer to [this](ui-configuration-devops.md#global-configuration) section to learn about globalConfig file.

if you do not have a global config and AWS credentials are not present, then create a temporary local config under the path:

```
micro-ui/web/example/public/index.html
```

Include this between the head tags

```
 <script>
  var globalConfigs = (function () {
  var stateTenantId = 'dev'
  var gmaps_api_key = 'AIzaSyCslxyiD1nuQuoshbu_E3WkIV8J2SUA6KI';
  var contextPath = 'workbench-ui';
  var configModuleName = 'commonHCMUiConfig';
  var centralInstanceEnabled = false;
  var localeRegion = "IN";
  var localeDefault = "en";
  var mdmsContext = "egov-mdms-service";
  var footerBWLogoURL =
  "https://egov-uat-assets.s3.ap-south-1.amazonaws.com/digit-footer-bw.png";
var footerLogoURL =
  "https://egov-uat-assets.s3.ap-south-1.amazonaws.com/digit-footer.png";
  var digitHomeURL = 'https://www.digit.org/';
  var assetS3Bucket = 'egov-uat-asset';
  var hrmsContext = "health-hrms";
  var projectContext= "health-project";
  var invalidEmployeeRoles = ["CBO_ADMIN", "ORG_ADMIN", "ORG_STAFF", "SYSTEM"]
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
    } else if (key === 'CONTEXT_PATH') {
      return contextPath;
    } else if (key === 'UICONFIG_MODULENAME') {
      return configModuleName;
    } else if (key === "LOCALE_REGION") {
      return localeRegion;
    } else if (key === "LOCALE_DEFAULT") {
      return localeDefault;
    } else if (key === "MDMS_CONTEXT_PATH") {
      return mdmsContext;
    } else if (key === "PROJECT_SERVICE_PATH") {
      return projectContext;
    } else if (key === "HRMS_CONTEXT_PATH") {
      return hrmsContext;
    } else if (key === "MDMS_V2_CONTEXT_PATH") {
      return mdmsContext;
    } else if (key === "MDMS_V1_CONTEXT_PATH") {
      return mdmsContext;
    } if (key === 'INVALIDROLES') {
      return invalidEmployeeRoles;
    }
  };
  return {
    getConfig
  };
}());
    </script>
```

Link to [example](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/micro-ui-internals/example/public/index.html).
{% endtab %}
{% endtabs %}
