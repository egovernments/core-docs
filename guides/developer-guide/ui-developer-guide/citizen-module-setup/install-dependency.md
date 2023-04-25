# Install Dependency

## Add MDMS (Master Data Management Service) Configuration

When creating a new module, the module needs to be enabled in `citymodule.json.` A sample module is available for reference here: [citymodule.json](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/tenant/citymodule.json).

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

The birth registration UI module needs to be registered in three places so that it will be available for the developer at runtime as well as at the time of deployment.&#x20;

Below are the three places where the module needs to be registered:

* `micro-ui/web/micro-ui-internals/package.json`\
  `micro-ui/web/micro-ui-internals/example/package.json`\
  `micro-ui/web/micro-ui-internalsWeb/package.json`
* **Micro-ui-internals:-**\
  Now open the micro-ui-internals package.json file and add this module as a dependency.

```
"dev:br": "cd packages/modules/br && yarn start",
"build:br": "cd packages/modules/br && yarn build", 
```

* In the example/package.json, add the following line:

```
"@egovernments/digit-ui-module-br":"^1.0.0",
```

* In the web/package.json, add the following line:

```
"@egovernments/digit-ui-module-br":"1.0.0",
```

&#x20;

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this website by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
