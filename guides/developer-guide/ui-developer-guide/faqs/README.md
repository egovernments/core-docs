# FAQs

**Required setup things?**\
i) Install Vs Code -

* [vs code for windows](https://code.visualstudio.com/download)
* [vs code for Linux](https://code.visualstudio.com/download)

VS Code Extension -

* [GitLense](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)
* [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
* [Tailwind CSS](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss)

ii) Install Node JS -

* [Node Js For Windows](https://nodejs.org/en/download/)
* [Node Js For Linux](https://nodejs.org/en/download/)

iii) Install Postman - Postman is the tool we use to hit and test the APIs exposed by various services that we have. To install postman, follow the following links -

* [Postman for Windows](https://www.postman.com/downloads/)
* [Postman for Linux](https://dl.pstmn.io/download/latest/linux64)

**2) How to install Yarn?**

Install Yarn -

[Yarn For Linux](https://linuxhint.com/install\_yarn\_ubuntu/)

```
npm install --global yarn
yarn --version
```

**3) How To add Globalconfig in Digit UI Environment?**

Local Environment: To enable it into local development we need to add the javascript code block of globalconfig.js into the index.html

Path:- `micro-ui/web/public/index.html`

Link:- [https://github.com/egovernments/DIGIT-Dev/blob/master/frontend/micro-ui/web/public/index.html](https://github.com/egovernments/DIGIT-Dev/blob/master/frontend/micro-ui/web/public/index.html)

Script:-

```
<script src="https://path/to/public/s3/bucket/globalConfigs.js"></script>
```

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8"/>
    <link rel="icon" href="https://cdn.jsdelivr.net/npm/@egovernments/digit-ui-css/img/browser-icon.png"/>
    <link href="https://fonts.googleapis.com/css2?family=Roboto+Condensed:wght@400;500;700&family=Roboto:wght@400;500;700&display=swap" rel='stylesheet' type='text/css'>
    <link rel="stylesheet" href="https://unpkg.com/@egovernments/digit-ui-css@1.4.111/dist/index.css"/>
    <!-- <link rel="stylesheet" href="https://unpkg.com/@egovernments/digit-ui-css/dist/index.css"/> -->
    <meta name="viewport" content="width=device-width, initial-scale=1"/>
    <meta name="theme-color" content="#00bcd1"/>
    <title>mSeva</title>
     <script src="https://path/to/public/s3/bucket/globalConfigs.js"></script> 
   
</script>
  </head>
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
    <!--
      This HTML file is a template.
      If you open it directly in the browser, you will see an empty page.
      You can add webfonts, meta tags, or analytics to this file.
      The build step will place the bundled scripts into the <body> tag.
      To begin the development, run `npm start` or `yarn start`.
      To create a production bundle, use `npm run build` or `yarn build`.
    -->
  </body>
</html>

```

Dev Environment: To enable it in the dev environment we need to add the javascript code block of telemetry into the\
Path:- DIGIT-DevOps/deploy-as-code/helm/environments/dev.yam

Link:-[ https://github.com/egovernments/DIGIT-Dev/blob/master/frontend/micro-ui/web/public/index.html  ](https://github.com/egovernments/DIGIT-Dev/blob/master/frontend/micro-ui/web/public/index.html)

```
<script src=https://path/to/public/s3/bucket/globalConfigs.js type=text/javascript></script>
```

```
employee:
  dashboard-url: "https://dashboard-pbuat.egovernments.org/s/w---s/app/kibana#/dashboard/4e687470-f3c7-11e8-8d09-b151e2b1cf8e?embed=true&_g=(refreshInterval%3A(pause%3A!f%2Cvalue%3A300000)%2Ctime%3A(from%3Anow-15m%2Cmode%3Aquick%2Cto%3Anow))"
  custom-js-injection: |
    sub_filter.conf: "
      sub_filter  '<head>' '<head>
      <script src=https://path/to/public/s3/bucket/globalConfigs.js type=text/javascript></script>
      ';"

citizen:
  custom-js-injection: |
    sub_filter.conf: "
      sub_filter  '<head>' '<head>
      <script src=https://path/to/public/s3/bucket/globalConfigs.js type=text/javascript></script>
      ';"

digit-ui:
  custom-js-injection: |
    sub_filter.conf: "
      sub_filter  '<head>' '<head>
      <script src=https://path/to/public/s3/bucket/globalConfigs.js type=text/javascript></script>
      ';"

```

**4) How to Register New Module in Digit UI?**\
Creating config into mdms:-

If you are creating a new module then, first we need to enable that module as true in citymodule.json\
and [update the Module in citymodule.json](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/tenant/citymodule.json).

```
 {
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
    },


```

&#x20;Suppose your module name is BR(Birth-Registration) then change the module and code as BR. and update the citymodule.json file.\
or

[Install Dependency](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/2206990337)\
\
**5) In Digit UI Where do we need to add the .env file?**\
Add the .env file in the example folder -&#x20;

If the User is a citizen then we will configure the .env file as follow:-

```
SKIP_PREFLIGHT_CHECK=true
REACT_APP_USER_TYPE=CITIZEN
REACT_APP_EMPLOYEE_TOKEN=c835932f-2ad4-4d05-83d6-49e0b8c59f8a
REACT_APP_CITIZEN_TOKEN=7cd58aae-30b3-41ed-a1b3-3417107a993c
REACT_APP_PROXY_API=https://dev.companyname.org
REACT_APP_PROXY_ASSETS=https://dev.companyname.org
REACT_APP_GLOBAL=https://path/to/public/s3/bucket/globalConfigs.js
REACT_APP_CENTRAL_GLOBAL=https://path/to/public/s3/bucket/statebglobalConfigs.js
REACT_APP_QA_GLOBAL=https://path/to/public/s3/bucket/egov-dev-assets/globalConfigs.js
REACT_APP_UAT_GLOBAL=https://path/to/public/s3/bucket/egov-uat-assets/globalConfigs.js
REACT_APP_STATEB_GLOBAL=https://path/to/public/s3/bucket/statebglobalConfigs.js
staging=https://staging.companyname.org
```

If the User is an Employee then we configure the .env as follows:-

```
SKIP_PREFLIGHT_CHECK=true
REACT_APP_USER_TYPE=EMPLOYEE
REACT_APP_EMPLOYEE_TOKEN=c835932f-2ad4-4d05-83d6-49e0b8c59f8a
REACT_APP_CITIZEN_TOKEN=7cd58aae-30b3-41ed-a1b3-3417107a993c
REACT_APP_PROXY_API=https://dev.companyname.org
REACT_APP_PROXY_ASSETS=https://dev.companyname.org
REACT_APP_GLOBAL=https://path/to/public/s3/bucket/globalConfigs.js
REACT_APP_CENTRAL_GLOBAL=https://path/to/public/s3/bucket/statebglobalConfigs.js
REACT_APP_QA_GLOBAL=https://path/to/public/s3/bucket/egov-dev-assets/globalConfigs.js
REACT_APP_UAT_GLOBAL=https://path/to/public/s3/bucket/egov-uat-assets/globalConfigs.js
REACT_APP_STATEB_GLOBAL=https://path/to/public/s3/bucket/statebglobalConfigs.js
staging=https://staging.companyname.org
```

**6) In Digit UI Where do we need to add the .env file when we run the react app from micro-ui/web?**

&#x20; Add the .env file in the micro-ui/web/src/

```
REACT_APP_STATE_LEVEL_TENANT_ID=pb
REACT_APP_PROXY_URL=https://dev.companyname.org
```





[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this website by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
