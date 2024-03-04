# Install Dependency

## Overview

Once the project structure is ready, it is time to install and configure the module dependencies in the Master Data Management Service (MDMS). Follow the steps below to finalise these.

## Steps

#### Add MDMS (Master Data Management Service) Configuration

1. Enable the module in `citymodule.json`before creating a new module. A sample module is available for reference here: [citymodule.json](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/tenant/citymodule.json).

For the purpose of illustration here, add the following module (birth registration) as given below:

```
  "citymodule": [{
      "module": "BR",
      "code": "BR",
      "active": true,
      "order": 1,
      "tenants": [
        {
          "code": "pb.jalandhar"
        },
        {
          "code": "pb.nawanshahr"
        },
        {
          "code": "pb.amritsar"
        }
      ]
    }],

```

2. Register the birth registration UI module in three places so that it will be available to the developer at runtime as well as at the time of deployment. Below are the three places where the module needs to be registered:

`micro-ui/web/micro-ui-internals/package.json`\
`micro-ui/web/micro-ui-internals/example/package.json`\
`micro-ui/web/micro-ui-internalsWeb/package.json`

3. **Micro-ui-internals:-** Open the micro-ui-internals package.json file and add this module as a dependency.

```
"dev:br": "cd packages/modules/br && yarn start",
"build:br": "cd packages/modules/br && yarn build", 
```

4. In the example/package.json, add the following line:

```
"@egovernments/digit-ui-module-br":"^1.0.0",
```

5. In the web/package.json, add the following line:

```
"@egovernments/digit-ui-module-br":"1.0.0",
```

