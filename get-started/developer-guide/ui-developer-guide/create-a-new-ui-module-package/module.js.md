# Module.js

Next, we need to register the `SampleModule` in the `module.js` file.The `module.js` file is the entry file for the module. We can illustrate rendering a plain screen with the text "**Sample Module**"  using a simple`<div>` element within the SampleModule component. This demonstrates how to create a basic screen using the module setup, which can later be customized or expanded as needed.



Add the following code in the Module.js file which we have already created.

```
import { Loader} from "@egovernments/digit-ui-react-components";
import React from "react";

export const SampleModule = ({ stateCode, userType, tenants }) => {
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
  return ( <Switch>
  <AppContainer className="ground-container">
           <div>Sample Module </div> 

  </AppContainer>
  </Switch>)
  
const componentsToRegister = {
  SampleModule,
};
export const initSampleComponents = () => {
  overrideHooks();
  updateCustomConfigs();
  Object.entries(componentsToRegister).forEach(([key, value]) => {
    Digit.ComponentRegistryService.setComponent(key, value);
  });
};

```

* We need to initialize our module's custom hooks, configurations, and register components using `initSampleComponents()` here.

Refer the file below:

[Module.js](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/micro-ui-internals/packages/modules/sample/src/Module.js)



<details>

<summary>Linking the Newly created module in Main App</summary>

* After creating module code we need to enable it in two places:

1. **For Deployment** \
   &#x20;In app.js we import the SampleModule, initSampleComponents,  and enable the Sample module.\
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

2. **For Local development** \
   In index.js, we will import the SampleModule, initSampleComponents,  and enable the  Sample module.\
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

* If you have a local server running, please stop it. Restart by running `yarn install` followed by `yarn start` at the `micro-ui-internals` level .

Hurray!  Now you can see the screen displayed below by visiting the given URL:

```
http://localhost:3000/digit-ui/employee/sample
```

<figure><img src="../../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

Refer below sections for deeper understanding

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td></td><td>Reusable Components</td><td></td><td><a href="import-required-components.md">import-required-components.md</a></td></tr><tr><td></td><td>Reusable Hooks</td><td></td><td><a href="common-hooks.md">common-hooks.md</a></td></tr><tr><td></td><td>Employee Module Setup</td><td></td><td><a href="../employee-module-setup/">employee-module-setup</a></td></tr></tbody></table>
