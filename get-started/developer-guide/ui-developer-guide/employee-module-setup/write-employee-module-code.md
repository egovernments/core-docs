# Write Employee Module Code

## Introduction

This guide provides a step-by-step approach to creating an employee module screen with essential functionality. Learn how to set up the module, create a sample card, and integrate links for individual search and create pages. Following these steps ensures modularity and reusability in your code, making it easier to manage and scale.

## Steps

Create a **Sample card** within the **Sample module.** This card will display links to pages within the module, such as **Individual Create** and **Individual Search**.

Create a **SampleCard.js** file under the following path:

```
/micro-ui-internals/packages/modules/sample/src/components/SampleCard.js
```

```
const SampleCard = () => {
 
  const { t } = useTranslation();

  const propsForModuleCard = {
    Icon: <PropertyHouse />,
    moduleName: t("Sample"),
    kpis: [

    ],
    links: [
      {
        label: t("Individual Search"),
        link: `/${window?.contextPath}/employee/sample/search-individual`,

      },
      {
        label: t("Individual Create"),
        link: `/${window?.contextPath}/employee/sample/create-individual`,

      },

  return <EmployeeModuleCard {...propsForModuleCard} />;
};

export default SampleCard;
```

Refer to the file here: [SampleCard.js](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/micro-ui-internals/packages/modules/sample/src/components/SampleCard.js)

* Register the `SampleCard`inside the `Module.js` file.

```
const componentsToRegister = {
  SampleModule,
  SampleCard,
};
```

* Hurray! Now you can see the Sample Card with 2 links on the screen as visible in the below screenshot:

<div align="left">

<figure><img src="../../../../.gitbook/assets/image (7).png" alt="" width="204"><figcaption></figcaption></figure>

</div>

Nothing is rendered when clicking on the label. We need to set up the routes to fix this.

<details>

<summary>Set Up Routes</summary>

* Routing in an application is essential for navigation and managing different views or pages based on the URL.
* Utilize a new file, **index.js**, to add all the routes for navigation. In the `index.js` file, we can create an `App` component where all the routes are defined. Then, in the `module.js` file, we import this `App` component as `EmployeeApp` and use it to render the screens within the module. This approach helps to organize the routing logic effectively, keeping the `module.js` file focused on the module's specific functionality.

Create the index.js under the following path:\
`micro-ui-internals/packages/modules/sample/src/pages/employee/index.js`

* In `index.js`, add the private route specifying the path and component name to render upon accessing that route. Ensure all components are correctly imported into this file.

```javascript
const App = ({ path, stateCode, userType, tenants }) => {
  return (
        <PrivateRoute path={`${path}/create-individual`} component={() => <IndividualCreate />} />
        <PrivateRoute path={`${path}/search-individual`} component={() => <IndividualSearch></IndividualSearch>} />
  );
};

export default App;
```

Reference for Routing and index.js file is available here: [Index.js](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/micro-ui-internals/packages/modules/sample/src/pages/employee/index.js)

* After adding routes in `index.js`, call them from `module.js`. The `module.js` file acts as the entry point, initializing components, hooks, and configurations. It renders the `EmployeeApp` component, which contains the routes and ensures the correct page is displayed.

In the Module.js add the following:

```
import { default as EmployeeApp } from "./pages/employee";

if (isLoading) {
    return <Loader />;
  }
  return <EmployeeApp path={path} stateCode={stateCode} userType={userType} tenants={tenants} />;
};
```

* The Sample Card is now visible with routes to the Respective Pages.
* One link is for the **Create Individual s**creen**,** and the other is for the I**ndividual Search**. You can view the code for the Create screen or set up the Create page by referring to the link here - [Create-Screen](creation-of-new-create-form-create-screen.md)

</details>

<details>

<summary>Registering  Components</summary>

* After registering all components, links and module code we need to enable it in two places:

1. In `micro-ui/web/src/App.js`, import the `SampleModule`, `initSampleComponents`, and enable the Sample module. Add App.js file under the following path: `micro-ui/web/src/App.js`

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

The reference for the App.js file is available here: [App.js](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/src/App.js)

2. In `index.js`, import `SampleModule`, initialize `initSampleComponents`, and enable the `Sample` module.\
   Create the index.js file under the following path:\
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

Reference for the Index.js file is available here: [Index.js](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/micro-ui-internals/example/src/index.js)

</details>

