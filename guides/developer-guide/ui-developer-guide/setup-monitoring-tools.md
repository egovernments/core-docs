---
description: Monitor and trace user activity
---

# Setup Monitoring Tools

To monitor and trace user activity on the client side, we need to enable telemetry in the local or development environment.

<details>

<summary>Local Environment</summary>

To enable it into local development we need to add the javascript code block of telemetry into the index.html\
\
`micro-ui → web → public → index.html`\
\
GitHub Link: [https://github.com/egovernments/DIGIT-OSS/blob/master/frontend/micro-ui/web/public/index.html](https://github.com/egovernments/DIGIT-OSS/blob/master/frontend/micro-ui/web/public/index.html)\
\
Script:

```
<script src=https://unpkg.com/@egovernments/telemetry@0.0.2/dist/egov-telemetry-1557467338.js type=text/javascript>
</script>
```

```javascript
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
    <!-- <script src="https://s3.ap-south-1.amazonaws.com/egov-dev-assets/globalConfigs.js"></script> -->
    <script src=https://unpkg.com/@egovernments/telemetry@0.0.2/dist/egov-telemetry-1557467338.js type=text/javascript>
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

Once the script was added to the index.html, restart the server and go to the network tab of the developer console and filter for telemetry.

</details>

<details>

<summary>Dev Environment</summary>

To enable it in the dev environment (where DIGIT is deployed. Could be UAT or staging or prod), we need to add the javascript code block of telemetry into the Helm environment file used for deploying DIGIT.\
For example, for the development environment, we use dev.yaml.

Path:- DIGIT-DevOps/deploy-as-code/helm/environments/dev.yaml\
\
Link:-[DIGIT-DevOps/dev.yaml at 1505924733cc56f85912b3add1f21815d8f62b7a · egovernments/DIGIT-DevOps](https://github.com/egovernments/DIGIT-DevOps/blob/1505924733cc56f85912b3add1f21815d8f62b7a/deploy-as-code/helm/environments/dev.yaml#L394)

```
<script src=https://unpkg.com/@egovernments/telemetry@0.0.2/dist/egov-telemetry-1557467338.js type=text/javascript>
</script>
```

Add the script injection to the employee and citizen modules in the environment file. This will inject it and deploy it into the environment.

```
employee:
  dashboard-url: "https://dashboard-pbuat.egovernments.org/s/w---s/app/kibana#/dashboard/4e687470-f3c7-11e8-8d09-b151e2b1cf8e?embed=true&_g=(refreshInterval%3A(pause%3A!f%2Cvalue%3A300000)%2Ctime%3A(from%3Anow-15m%2Cmode%3Aquick%2Cto%3Anow))"
  custom-js-injection: |
    sub_filter.conf: "
      sub_filter  '<head>' '<head>
      <script src=https://unpkg.com/@egovernments/telemetry@0.0.2/dist/egov-telemetry-1557467338.js type=text/javascript></script>
      <script src=https://s3.ap-south-1.amazonaws.com/egov-uat-assets/globalConfigs.js type=text/javascript></script>
      ';"

citizen:
  custom-js-injection: |
    sub_filter.conf: "
      sub_filter  '<head>' '<head>
      <script src=https://unpkg.com/@egovernments/telemetry@0.0.2/dist/egov-telemetry-1557467338.js type=text/javascript></script>
      <script src=https://s3.ap-south-1.amazonaws.com/egov-uat-assets/globalConfigs.js type=text/javascript></script>
      ';"

digit-ui:
  custom-js-injection: |
    sub_filter.conf: "
      sub_filter  '<head>' '<head>
      <script src=https://s3.ap-south-1.amazonaws.com/egov-uat-assets/globalConfigs.js type=text/javascript></script>
      ';"
```



</details>

{% hint style="info" %}
Whichever **environment file** has been used to deploy DIGIT, please make sure the above code blocks are added to the file. Dev has been used here as an example. This can differ based on the environment.
{% endhint %}

Redeploy the citizen, employee, and digit-ui modules using Helm. For example, to redeploy the citizen module, identify the docker image ID from the product release charts.

`/DIGIT-DevOps/config-as-code/product-release-charts/DIGIT/dependancy_chart-digit-<version>.yaml`

If you have deployed DIGIT v2.6, use the 2.6 release chart. If 2.7, use the 2.7 release chart. Search for the docker image ID of the citizen, employee and digit-UI modules and copy those.&#x20;

Then, run the following commands to redeploy the citizen module with the updated variables in the environment file. This will replace the new values during deployment and configure it appropriately:

```
 go run main.go deploy -c -e <environment_file.yaml> egovio/citizen:v1.5.0-c1825dd69-291
```

Repeat this exercise for the employee module. Redeploy the digit-ui module based on the instructions [here](build-and-deploy.md). \
\
Once the deployment is successful, we can track it into the Network tab by filter telemetry.



[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this website by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
