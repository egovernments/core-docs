# Write Employee Module Code

* The next step is to create a **Sample card** within our **Sample module.** This card will display links to pages within the module, such as **Individual create** and **Individual search**.

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

Refer the file below:

[SampleCard.js](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/micro-ui-internals/packages/modules/sample/src/components/SampleCard.js)

* Additionally, we need to register the `SampleCard`inside the `Module.js` file.

```
const componentsToRegister = {
  SampleModule,
  SampleCard,
};
```

*   Hurray! Now you may be able to see the Sample Card with 2 links on the screen.


* It should be as in the image below:

<div align="left">

<figure><img src="../../../../.gitbook/assets/image (7).png" alt="" width="204"><figcaption></figcaption></figure>

</div>

* But if you try clicking that label, nothing will get rendered. So now we have to set up the routes for that.



<details>

<summary>Set Up Routes</summary>

* Routing in a  application is essential for navigation and managing different views or pages based on the URL.

<!---->

* We can utilize a new file, **index.js**, to add all the routes for navigation.In the `index.js` file, we can create an `App` component where all the routes are defined. Then, in the `module.js` file, we import this `App` component as `EmployeeApp` and use it to render the screens within the module. This approach helps to organize the routing logic effectively, keeping the `module.js` file focused on the module's specific functionality.

Create the index.js under the following path:\
`micro-ui-internals/packages/modules/sample/src/pages/employee/index.js`

* In `index.js,` we will add the private route and we mention the path and component name which component we need to show or render when we hit that route.Ensure that you import all your components correctly in this file.

```javascript
const App = ({ path, stateCode, userType, tenants }) => {
  return (
        <PrivateRoute path={`${path}/create-individual`} component={() => <IndividualCreate />} />
        <PrivateRoute path={`${path}/search-individual`} component={() => <IndividualSearch></IndividualSearch>} />
  );
};

export default App;
```

\
Reference for Routing and index.js file is given below:

[Index.js](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/micro-ui-internals/packages/modules/sample/src/pages/employee/index.js)

* After adding the routes in `index.js`, you need to call them from `module.js`. The `module.js` file serves as the entry point for the module, initializing all components, hooks, and configurations. It renders the `EmployeeApp` component, which contains the defined routes and ensures the correct pages are displayed.

In the Module.js add the following:

```
import { default as EmployeeApp } from "./pages/employee";

if (isLoading) {
    return <Loader />;
  }
  return <EmployeeApp path={path} stateCode={stateCode} userType={userType} tenants={tenants} />;
};
```

* Now you should be able to see the Sample Card with routes to the Respective Pages.
* One link is for the **Create Individual s**creen**,** and the other is for the I**ndividual Search** . You can view the code for the Create screen or set up the Create page by referring to the link provided below.

&#x20;      [Create-Screen](creation-of-new-create-form-create-screen.md)





</details>

<details>

<summary>Registering  Components</summary>

* After registering all components, links and module code we need to enable it in two places:

1. &#x20; In app.js we import the SampleModule, initSampleComponents,  and enable the Sample module.\
   Add App.js file under the following path:\
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
[App.js](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/src/App.js)

2. In index.js, we will import the SampleModule, initSampleComponents,  and enable the  Sample module.\
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

Reference for the Index.js file is given below:\
[Index.js](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/micro-ui-internals/example/src/index.js)

</details>

\


[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this website by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
