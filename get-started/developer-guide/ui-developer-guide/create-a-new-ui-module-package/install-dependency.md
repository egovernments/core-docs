# Install Dependency

## Overview

Once the project structure is ready, it is time to install and configure the module dependencies in the Master Data Management Service (MDMS). Follow the steps below to finalise these.

## Steps

After creating the `Sample` module and its `package.json` file, you need to ensure that this module is enabled in the `citymodule.json` file in the MDMS (Master Data Management Service) configuration. If it is not enabled, you need to update the MDMS configuration accordingly. You need to add this module to the root tenant in your environment from your branch.

```
modulename : tenant
mastername : citymodule
```

file location&#x20;

{% hint style="info" %}
```
https://github.com/<<YOUR ORG NAME>>/egov-mdms-data/blob/<<BRANCH WHERE THE ENVIRONMENTS IS POINTED TO>>/data/<<ROOT TENANT OF YOUR ENVIRONMENT>>/tenant/citymodule.json
```
{% endhint %}

for reference : [citymodule.json](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/tenant/citymodule.json).

For illustration here, add the following module (Sample) as given below:

```
  "citymodule": [{
      "module": "SAMPLE",
      "code": "<<REPLACE WITH YOUR MODULECODE>>",
      "active": true,
      "order": 1,
      "tenants": [
        {
          "code": "<<REPLACE WITH YOUR TENANTS>>"
        }
      ]
    }],

```

2. Register the **Sample UI module** in three places so that it will be available to the developer at runtime as well as at the time of deployment. Below are the three places where the module needs to be registered:

`micro-ui/web/micro-ui-internals/package.json`\
`micro-ui/web/micro-ui-internals/example/package.json`

3. **Micro-ui-internals:-** Open the `micro-ui-internals` `package.json` file and add the following inside the scripts:

```
"scripts": { 
    "dev:sample": "cd packages/modules/sample && yarn start",
    "build:sample": "cd packages/modules/sample && yarn build",
  },
```

4. In the example/package.json, add the following line:

```
"@egovernments/digit-ui-module-Sample":"0.0.1",
```

5. In the web/package.json, add the following line:

```
"@egovernments/digit-ui-module-Sample":"0.0.1",
```



The next step is to initailise the module.js, refer [here](module.js.md) to know more about the setup
