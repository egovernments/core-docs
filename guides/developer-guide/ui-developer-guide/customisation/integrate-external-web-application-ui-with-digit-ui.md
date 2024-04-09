---
description: Steps to integrate external UI with DIGIT UI
---

# Integrate External Web Application/UI With DIGIT UI

## Overview

This document provides the steps on how to integrate another UI into the DIGIT UI using iframe.

## **Steps**

1. Enable the [Utilities](https://www.npmjs.com/package/@egovernments/digit-ui-module-utilities/v/0.0.6) module.
   * [x] [Add these MDMS](https://core.digit.org/guides/developer-guide/ui-developer-guide/citizen-module-setup/install-dependency#add-mdms-master-data-management-service-configuration) configurations to enable the Utilities module.
   * [x] Add the [mentioned change](https://core.digit.org/guides/developer-guide/ui-developer-guide/citizen-module-setup/write-citizen-module-code#enable-module-in-the-ui-framework)s in your web/src/App.js and web/package.json to enable the module in the Build.
2. Once the Utilities module is enabled, add the following changes to the master (file path given below). &#x20;

[Reference](https://github.com/egovernments/works-mdms-data/blob/DEV/data/pg/common-masters/uiCommonConstants.json) Master details: data/pg/commonmasters/uiCommonConstants.json

```
  "uiCommonConstants": [
      {
         "shg": {
            "iframe-routes": {
               "home": {
                  "routePath": "/works-shg-app/",
                  "isOrigin": true
               }
            }
         }
      }
   ]
```

Here -

* **shg** is the path name to access inside digit-ui;
* **home** is the route to access it;
* whatever is mentioned inside **routePath** should be the Application/Pod name that is expected  to be shown inside the digit-ui;

3. Once the MDMS changes are applied, access the new application using the following route - `<SERVER_URL>/digit-ui/employee/utilities/iframe/<PATH_NAME>/<ROUTE_NAME>`

**Examples: New Web Application (UI - any framework)**

<figure><img src="../../../../.gitbook/assets/Screenshot 2023-07-25 at 10.55.25 AM.png" alt=""><figcaption><p>shg app built through flutter</p></figcaption></figure>

**DIGIT UI**

<figure><img src="../../../../.gitbook/assets/Screenshot 2023-07-25 at 10.54.28 AM.png" alt=""><figcaption><p>integrated the other app through iframe</p></figcaption></figure>
