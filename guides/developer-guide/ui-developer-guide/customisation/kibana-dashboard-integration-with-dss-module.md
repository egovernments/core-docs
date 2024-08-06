# Kibana Dashboard Integration With DSS Module

## Overview

A new component called `KibanaCard.js` has been introduced to render Kibana DSS based on the configuration provided in `dashboardConfig`. This document outlines the steps to integrate the Kibana Dashboard with the DSS module.&#x20;

## Configuration

In the `dashboardConfig`, a new configuration has been added to render Kibana DSS. The configuration includes details that specify which Kibana dashboards to render.

```
{
    "row": 1,
    "name": "DSS_KIBANA_MAPS",      // name of the config
    "vizArray": [
        {
            "id": 401,
            "name": "DSS_HEALTH_KIBANA_SCREEN",
            "label": "DSS_HEALTH_KIBANA_SCREEN",
            "vizType": "chart",     // vizType set to chart  
            "noUnit": true,
            "isCollapsible": false,
            "charts": [
                {
                    "id": "checklistCompletionRateOfDistrictSupervisor",
                    "name": "DSS_HEALTH_SUPERVISION_DISTRICT_SUPERVISORS_CHECKLISTS_COMPLETION_RATE",
                    "code": "",
                    "moduleName": "smc",  // moduleName is needed to fetch Kibana url
                    "pageName": "national", // moduleName is needed to fetch Kibana url
                    "chartType": "kibanaComponent",  // chart type set to kibanaComponent to render Kibana DSS
                    "filter": "",
                    "headers": []
                }
            ]
        }
    ]
}
```

So here **moduleName** refers to the module name in uiConstants master and **pageName** refers to the iframe routes route information.

## Rendering KibanaCard

Based on the configuration, we render the `KibanaCard` component, passing `moduleName` and `pageName` as props.

````
```
      case "kibanaComponent":
        return <KibanaCard moduleName={chart?.moduleName} pageName={chart?.pageName} filters={value}></KibanaCard>;

```
````

## Internal Implementation

Within `KibanaCard`, we utilize the `IFrameInterface` component. This component receives the following props passed from `KibanaCard.`

```javascript
const IFrameInterface = (props) => {
    const { stateCode, moduleName, pageName, filters } = props;
    ....
}
```

We can define kibana dashboard URL in common-masters in uiCommonConstants.json config. Below are the examples of the structure

```
{
  "tenantId": "mz",
  "moduleName": "common-masters",
  "uiCommonConstants": [
    {
       "smc": {
        "iframe-routes": {
          "hcm": {
            "routePath": "/kibana/app/dashboards?auth_provider_hint=anonymous1#/view/b1ce8523-30cd-4966-aa8d-c3ac9561ebb2?embed=true&hide-filter-bar=true&_g=(time:(from:now-15m,to:now))&_a=()",
            "isOrigin": true,
            "title": "DASHBOARD_HCM",
            "overwriteTimeFilter": true,
            "Authorization":true,
            "base-kibana-path":"/kibana/"
          }
        }
      }
    }
  ]
}
```

This component calls `MDMS-V2` common-masters  to fetch the URL of the Kibana dashboard and render it using an iframe.

```
<IFrameInterface
        wrapperClassName="dss-kibana-iframe-wrapper"
        className="dss-kibana-iframe"
        moduleName={moduleName}
        pageName={pageName}
        stateCode={stateCode}
        filters={filters}
      />
```

Additionally, if a date range filter is set by the user, we update the Kibana URL to reflect this. The following logic is applied to construct the `contextPath`:

```
const contextPath = pageObject?.["routePath"] 
  ? (pageObject?.["overwriteTimeFilter"] && filters?.range?.startDate && filters?.range?.endDate 
    ? pageObject["routePath"].replace("from:now-15m", `from:'${new Date(filters?.range?.startDate).toISOString()}'`).replace("to:now", `to:'${new Date(filters?.range?.endDate).toISOString()}'`)
    : pageObject["routePath"]) 
  : "";

```

#### File Path

[KibanaCard](https://github.com/egovernments/DIGIT-Frontend/blob/2b964f458158a48e07fb18de966b450ef12a1576/micro-ui/web/micro-ui-internals/packages/modules/dss/src/components/KibanaCard.js)

[IFrameInterface](https://github.com/egovernments/DIGIT-Frontend/blob/73e29783cb061758f66cea040b10358e3cb69c93/micro-ui/web/micro-ui-internals/packages/modules/utilities/src/pages/employee/IFrameInterface/index.js)

### MDMS

[uiCommonConstant.json](https://github.com/egovernments/health-campaign-mdms/blob/DEMO/data/mz/common-masters/uiCommonConstants.json)

### **Configuration**&#x20;

[MasterDashboardConfig.json](https://github.com/egovernments/health-campaign-config/blob/DEMO/egov-dss-dashboards/dashboard-analytics/MasterDashboardConfig.json)

API to fetch common constants

URL: [https://health-demo.digit.org/mdms-v2/v1/\_search?tenantId=mz\
](https://health-demo.digit.org/mdms-v2/v1/\_search?tenantId=mz)

Payload:

```
{
    "MdmsCriteria": {
        "tenantId": "mz",
        "moduleDetails": [
            {
                "moduleName": "common-masters",
                "masterDetails": [
                    {
                        "name": "uiCommonConstants"
                    }
                ]
            }
        ]
    },
    "RequestInfo": {
        "apiId": "",
        "authToken": "",
        "msgId": ""
    }
}

```

Response:&#x20;

```
{
    "common-masters": {
        "uiCommonConstants": [
            {
                "id": "common-masters.uiCommonConstants.elastic.iframe-routes",
                "smc": {
                    "iframe-routes": {
                        "district": {
                            "title": "DISTRICT_DASHBOARD",
                            "isOrigin": true,
                            "routePath": "/kibana/app/dashboards?auth_provider_hint=anonymous1#/view/d90add16-5c45-4479-871b-e76c1a862f6f?embed=true&hide-filter-bar=true&_g=(time:(from:'2023-11-21T00:00:00.000Z',to:'2024-07-26T18:29:59.999Z'))&_a=(filters:!(('$state':(store:appState),meta:(alias:!n,disabled:!f,index:'5ac095ba-7c5e-4114-ac2b-efebb55901b0',key:Data.boundaryHierarchy.province.keyword,negate:!f,params:(query:Fintabo),type:phrase),query:(match_phrase:(Data.boundaryHierarchy.province.keyword:Fintabo)))))",
                            "Authorization": true,
                            "base-kibana-path": "/kibana/",
                            "overwriteTimeFilter": true
                        },
                        "national": {
                            "title": "NATIONAL_DASHBOARD",
                            "isOrigin": true,
                            "routePath": "/kibana/app/dashboards?auth_provider_hint=anonymous1#/view/719c74b6-3d4e-461c-8dff-6010a8494164?embed=true&hide-filter-bar=true&_g=(refreshInterval:(pause:!t,value:60000),time:(from:'2023-11-21T00:00:00.000Z',to:'2024-07-26T18:29:59.999Z'))&_a=()",
                            "Authorization": true,
                            "base-kibana-path": "/kibana/",
                            "overwriteTimeFilter": true
                        },
                        "province": {
                            "title": "PROVINCE_DASHBOARD",
                            "isOrigin": true,
                            "routePath": "/kibana/app/dashboards#/view/fcccd77a-df16-4e06-aa97-024b53393928?embed=true&hide-filter-bar=true&_g=(filters:!(),refreshInterval:(pause:!t,value:60000),time:(from:now-15m,to:now))",
                            "Authorization": true,
                            "base-kibana-path": "/kibana/",
                            "overwriteTimeFilter": true
                        }
                    }
                },
                "elastic": {
                    "iframe-routes": {
                        "hf": {
                            "title": "LOCALITY_DASHBOARD",
                            "isOrigin": true,
                            "routePath": "/kibana/app/dashboards#/view/50edb03b-6235-49e1-9083-7afca204763c?_g=(filters:!(),refreshInterval:(pause:!t,value:60000),time:(from:now-15m,to:now))"
                        },
                        "home": {
                            "isOrigin": true,
                            "routePath": "/kibana/login"
                        },
                        "district": {
                            "title": "DISTRICT_DASHBOARD",
                            "isOrigin": true,
                            "routePath": "/kibana/app/dashboards#/view/a37931ea-d3ae-4155-9f0a-eca95339c5bd?_g=(filters:!(),refreshInterval:(pause:!t,value:60000),time:(from:now-15m,to:now))"
                        },
                        "national": {
                            "title": "NATIONAL_DASHBOARD",
                            "isOrigin": true,
                            "routePath": "/kibana/app/dashboards#/view/b1ce8523-30cd-4966-aa8d-c3ac9561ebb2?_g=(filters:!(),refreshInterval:(pause:!t,value:60000),time:(from:now-15m,to:now))"
                        },
                        "province": {
                            "title": "PROVINCE_DASHBOARD",
                            "isOrigin": true,
                            "routePath": "/kibana/app/dashboards#/view/fcccd77a-df16-4e06-aa97-024b53393928?_g=(filters:!(),refreshInterval:(pause:!t,value:60000),time:(from:now-15m,to:now))"
                        }
                    }
                }
            }
        ]
    }
}
```
