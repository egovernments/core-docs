# Write Employee Module Code

Before starting with Employee Module Code**,** make sure you have set up the [Project Structure](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/2206957569), [installed dependencies](../create-a-new-ui-module-package/install-dependency.md) and [imported the required components](../create-a-new-ui-module-package/import-required-components.md).

This section will walk you through the code that needs to be developed for the application. Detailed user screen wireframes should be available at this point for development.

<details>

<summary>Employee Module Card</summary>

In the Employee module, we create the "Sample card" to show the Create Application form.&#x20;

#### SampleCard

In SampleCard.js we are reusing the components that are already present in the DIGIT-UI-component. Import the Icon and EmployeeModuleCard.

```jsx
import { HRIcon, EmployeeModuleCard, AttendanceIcon, PropertyHouse } from "@egovernments/digit-ui-react-components";
import React from "react";
import { useTranslation } from "react-i18next";

const SampleCard = () => {
 
  const { t } = useTranslation();

  const propsForModuleCard = {
    Icon: <PropertyHouse />,
    moduleName: t("Sample"),
    kpis: [

    ],
    links: [
   
     
      {
        label: t("Inbox"),
        link: `/${window?.contextPath}/employee/sample/inbox`,

      },
      {
        label: t("Create Individual"),
        link: `/${window?.contextPath}/employee/sample/create-individual`,

      },
    ],
  };

  return <EmployeeModuleCard {...propsForModuleCard} />;
};

export default SampleCard;

```



</details>

<details>

<summary>Set Up Routes</summary>

Routing in a  application is essential for navigation and managing different views or pages based on the URL.

Create the index.js under the following path:\
`micro-ui-internals/packages/modules/sample/src/pages/employee/index.js`\
\
In `index.js,` we will add the private route and we mention the path and component name which component we need to show or render when we hit that route.\
\
`<PrivateRoute path={${path}/sample-create} component={() => } /> <PrivateRoute path={${path}/inbox} component={() => } />`\
\
Reference for routing and index.js file is given below:

[Index.js](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/micro-ui-internals/packages/modules/sample/src/pages/employee/index.js)

</details>

<details>

<summary>Registering All Components &#x26; Modules</summary>

`module.js` is the entry point where we can register all components and modules.

Create module.js under the following path:

```
micro-ui-internals/packages/modules/sample/src/Module.js
```

```jsx
import { Loader} from "@egovernments/digit-ui-react-components";
import React from "react";
import { useRouteMatch } from "react-router-dom";
import { default as EmployeeApp } from "./pages/employee";
import SampleCard from "./components/SampleCard";

export const SampleModule = ({ stateCode, userType, tenants }) => {
 
  const { path, url } = useRouteMatch();
  const tenantId = Digit.ULBService.getCurrentTenantId();
  const moduleCode = ["sample", "common","workflow"];
  const language = Digit.StoreData.getCurrentLanguage();
  const { isLoading, data: store } = Digit.Services.useStore({
    stateCode,
    moduleCode,
    language,
  });

  if (isLoading) {
    return <Loader />;
  }
  return <EmployeeApp path={path} stateCode={stateCode} userType={userType} tenants={tenants} />;
};

const componentsToRegister = {
  SampleModule,
  SampleCard
};
export const initSampleComponents = () => {
  Object.entries(componentsToRegister).forEach(([key, value]) => {
    Digit.ComponentRegistryService.setComponent(key, value);
  });
};
```

After registering all components, links and module code we need to enable it in two places:

1\)  In app.js we import the SampleModule, initSampleComponents, and and enable the Sample module.\
Add App.js file under the following path:\
\
`micro-ui/web/src/App.js`

```jsx
const enabledModules = [
  "sample"
];

const moduleReducers = (initData) => ({
  initData,
});

const initDigitUI = () => {
  window.Digit.ComponentRegistryService.setupRegistry({});
  window.Digit.Customizations = {
    PGR: {},
    commonUiConfig: UICustomizations,
  };
  initSampleComponents();

};

initLibraries().then(() => {
  initDigitUI();
});
```

\
Reference for the App.js file is given below:\
[App.js](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/src/App.js)\
\
\
2\) In index.js, we will import the SampleModule, initSampleComponents,  and enable the Sample module.\
create the index.js file under the following path:\
`micro-ui-internals/example/src/index.js`

```jsx

 const enabledModules = [
  "Sample"
];

const initDigitUI = () => {
  window.contextPath = window?.globalConfigs?.getConfig("CONTEXT_PATH") || "digit-ui";
  window.Digit.Customizations = {
    commonUiConfig: UICustomizations
  };
  initSampleComponents();
```

Reference for the Index.js file is given below:\
[Index.js](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/micro-ui-internals/example/src/index.js)

</details>



\


[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this website by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
