# Frequent issues, errors and their fixes

## Compile-time issues

### 1. node-sass error

After making these initial upgrades and changes, we attempted to run the application. However, we encountered a "node-sass" error during compilation.

**Debugging the Issue**

To diagnose the issue, we examined the dependency tree of node-sass using the following co

npm list node-sass

This command revealed multiple direct and indirect dependencies relying on node-sass.

**Solution: Removing Conflicting Dependencies**

To resolve the error, we removed all dependencies related to node-sass, including:

* digit-ui-css
* react-scripts (which was no longer needed after the migration to Webpack)

After these fixes, the application compiled successfully.

## Run-Time errors

After successfully compiling the application, we encountered a few additional errors that required resolution.

#### 1. Error: "Digit Not Defined"

**Issue:**

After upgrading the Example App to React 19, the application failed to recognize "Digit", causing the screen to break with the following error:

Uncaught ReferenceError: Digit is not defined

**Root Cause:**

The error occurred due to changes in the execution order of modules. The previous approach, which worked before the upgrade, was no longer compatible with the updated React 19 environment.

**Solution:**

To resolve this issue, we restructured the execution order using lazy loading. This ensures that modules are loaded dynamically and in the correct sequence.

Below is the updated index.js file for the Example App:

```
import React, { useEffect, useState, lazy, Suspense } from "react";
import ReactDOM from "react-dom/client"; // Use createRoot from React 18
import { initGlobalConfigs } from "./globalConfig";
import {initAssignmentComponents} from "@egovernments/digit-ui-module-assignment"
// import {initWorkbenchComponents} from "@egovernments/digit-ui-module-workbench"
import { BrowserRouter } from "react-router-dom";
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";
import { Hooks } from "@egovernments/digit-ui-libraries";


// Ensure Digit is defined before using it
window.Digit = window.Digit || {};
window.Digit.Hooks = Hooks; 
const queryClient = new QueryClient();
const DigitUILazy = lazy(() =>
  import("@egovernments/digit-ui-module-core").then((module) => ({ default: module.DigitUI }))
);import { initLibraries } from "@egovernments/digit-ui-libraries";


const enabledModules = ["assignment", "HRMS", "Workbench"];


const initTokens = (stateCode) => {
  console.log(window.globalConfigs, "window.globalConfigs");


  const userType =
    window.sessionStorage.getItem("userType") ||
    process.env.REACT_APP_USER_TYPE ||
    "CITIZEN";
  const token =
    window.localStorage.getItem("token") ||
    process.env[`REACT_APP_${userType}_TOKEN`];


  const citizenInfo = window.localStorage.getItem("Citizen.user-info");
  const citizenTenantId =
    window.localStorage.getItem("Citizen.tenant-id") || stateCode;
  const employeeInfo = window.localStorage.getItem("Employee.user-info");
  const employeeTenantId = window.localStorage.getItem("Employee.tenant-id");


  const userTypeInfo =
    userType === "CITIZEN" || userType === "QACT" ? "citizen" : "employee";
  window.Digit.SessionStorage.set("user_type", userTypeInfo);
  window.Digit.SessionStorage.set("userType", userTypeInfo);


  if (userType !== "CITIZEN") {
    window.Digit.SessionStorage.set("User", {
      access_token: token,
      info: userType !== "CITIZEN" ? JSON.parse(employeeInfo) : citizenInfo,
    });
  }


  window.Digit.SessionStorage.set("Citizen.tenantId", citizenTenantId);


  if (employeeTenantId && employeeTenantId.length) {
    window.Digit.SessionStorage.set("Employee.tenantId", employeeTenantId);
  }
};


const initDigitUI = () => {
  initGlobalConfigs(); // Ensure global configs are set first
  // console.log("initWorkbenchComponents", initWorkbenchComponents)
  // initWorkbenchComponents();
  window.contextPath =
  window?.globalConfigs?.getConfig("CONTEXT_PATH") || "digit-ui";
  
  const stateCode = Digit?.ULBService?.getStateId();
  
  const root = ReactDOM.createRoot(document.getElementById("root")); // ✅ React 18 uses createRoot()
  root.render(
    <BrowserRouter><QueryClientProvider client={queryClient
      
    }><MainApp stateCode={stateCode} enabledModules={enabledModules} /></QueryClientProvider></BrowserRouter>);
};


const MainApp = ({ stateCode, enabledModules }) => {
  const [isReady, setIsReady] = useState(false);
  const [loaded, setLoaded] = useState(false);
  
  
  
  useEffect(() => {
    
    initLibraries().then(() => {
      console.log(Digit,window?.Digit);
      // initAssignmentComponents();
      
      setIsReady(true)
    });
    // initWorkbenchComponents();
    
  }, []);


  useEffect(() => {
    initTokens(stateCode);
     setLoaded(true);
  }, [stateCode,isReady]);


  if (!loaded) {
    return <div>Loading...</div>;
  }


  return (
    <Suspense fallback={<div>Loading...</div>}>
    {window.Digit && (
      <DigitUILazy
        stateCode={stateCode}
        enabledModules={enabledModules}
        defaultLanding="home"
      />
    )}
  </Suspense>
  );
};


// Start the app
initDigitUI();


```

Note: Instead of root.render(), we’re using ReactDOM.createRoot() as per the latest React syntax changes.

***

#### 2. QueryClient Error \[Temporary Fix]

**Issue:**

After resolving the "Digit Not Defined" error, we successfully accessed Digit in the window object, but encountered QueryClient errors.

**Root Cause:**

Inside the core module, even though the application was wrapped inside QueryClientProvider, queryClient errors persisted. This was likely due to different contexts between the modules/packages.

**Solution:**

To resolve this, we imported the libraries module locally and extracted the Hooks from it inside the core module. Instead of setting up the hooks inside the libraries init function, we moved them into the core module and removed them from libraries.

Below are the changes made inside the core module:

```
import { BodyContainer } from "@egovernments/digit-ui-components";
import { Loader } from "@egovernments/digit-ui-components";
import React from "react";
import { getI18n } from "react-i18next";
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";
import { Provider } from "react-redux";
import { BrowserRouter as Router } from "react-router-dom";
import { DigitApp, DigitAppWrapper } from "./App";
import SelectOtp from "./pages/citizen/Login/SelectOtp";
import ChangeCity from "./components/ChangeCity";
import ChangeLanguage from "./components/ChangeLanguage";
import { useState } from "react";
import ErrorBoundary from "./components/ErrorBoundaries";
import getStore from "./redux/store";
import PrivacyComponent from "./components/PrivacyComponent";
import OtpComponent from "./pages/employee/Otp/OtpCustomComponent";
// import {useInitStore} from "../libraries/src/hooks/store"
// import {initWorkbenchComponents} from "@egovernments/digit-ui-module-workbench"
import { initWorkbenchComponents } from "../../workbench/src/Module";
import Hooks from "../../../libraries/src/hooks";
import { initI18n } from "@egovernments/digit-ui-libraries/src/translations";


console.log("inside module.js of core")
console.log(Digit.Hooks);


const DigitUIWrapper = ({ stateCode, enabledModules, defaultLanding }) => {
  console.log("inside DigitUIWrapper of core");
  window.Digit["Hooks"] = Hooks || {};
  const { isLoading, data: initData={} } = Digit.Hooks.useInitStore(stateCode, enabledModules);
  if (isLoading) {
    return <Loader page={true} />;
  }
  const data=getStore(initData) || {};
  const i18n = getI18n();
  initWorkbenchComponents();
  if(!Digit.ComponentRegistryService.getComponent("PrivacyComponent")){
    Digit.ComponentRegistryService.setComponent("PrivacyComponent", PrivacyComponent);
  }
  return (
    <Provider store={data}>
      <Router>
        <BodyContainer>
          {Digit.Utils.getMultiRootTenant() ? (
            <DigitAppWrapper
              initData={initData}
              stateCode={stateCode}
              modules={[
                {
                  "module": "assignment",
                  "code": "assignment",
                  "active": true,
                  "order": 13,
                  "tenants": [
                    {
                      "code": "mz"
                    }
                  ]
                },
                {
                  "module": "HRMS",
                  "code": "HRMS",
                  "active": true,
                  "order": 4,
                  "tenants": [
                    {
                      "code": "mz"
                    }
                  ]
                }
              ]}
              appTenants={initData.tenants}
              logoUrl={initData?.stateInfo?.logoUrl}
              logoUrlWhite={initData?.stateInfo?.logoUrlWhite}
              defaultLanding={defaultLanding}
            />
          ) : (
            <DigitApp
              initData={initData}
              stateCode={stateCode}
              modules={initData?.modules}
              appTenants={initData.tenants}
              logoUrl={initData?.stateInfo?.logoUrl}
              defaultLanding={defaultLanding}
            />
          )}
        </BodyContainer>
      </Router>
    </Provider>
  );
};


export const DigitUI = ({ stateCode, registry, enabledModules, moduleReducers, defaultLanding }) => {
  console.log("inside digitui of core");
  var Digit = window.Digit || {};
  initI18n();
  const [privacy, setPrivacy] = useState(Digit.Utils.getPrivacyObject() || {});
  const userType = Digit.UserService.getType();
  const queryClient = new QueryClient({
    defaultOptions: {
      queries: {
        staleTime: 15 * 60 * 1000,
        gcTime: 50 * 60 * 1000,
        retry: false,
        retryDelay: (attemptIndex) => Infinity,
        /*
          enable this to have auto retry incase of failure
          retryDelay: attemptIndex => Math.min(1000 * 3 ** attemptIndex, 60000)
         */
      },
    },
  });


  const ComponentProvider = Digit.Contexts.ComponentProvider;
  const PrivacyProvider = Digit.Contexts.PrivacyProvider;


  const DSO = Digit.UserService.hasAccess(["FSM_DSO"]);


  return (
    <QueryClientProvider client={queryClient}>
      <ErrorBoundary>
          <ComponentProvider.Provider value={registry}>
            <PrivacyProvider.Provider
              value={{
                privacy: privacy?.[window.location.pathname],
                resetPrivacy: (_data) => {
                  Digit.Utils.setPrivacyObject({});
                  setPrivacy({});
                },
                getPrivacy: () => {
                  const privacyObj = Digit.Utils.getPrivacyObject();
                  setPrivacy(privacyObj);
                  return privacyObj;
                },
                /*  Descoped method to update privacy object  */
                updatePrivacyDescoped: (_data) => {
                  const privacyObj = Digit.Utils.getAllPrivacyObject();
                  const newObj = { ...privacyObj, [window.location.pathname]: _data };
                  Digit.Utils.setPrivacyObject({ ...newObj });
                  setPrivacy(privacyObj?.[window.location.pathname] || {});
                },
                /**
                 * Main Method to update the privacy object anywhere in the application
                 *
                 * @author jagankumar-egov
                 *
                 * Feature :: Privacy
                 *
                 * @example
                 *    const { privacy , updatePrivacy } = Digit.Hooks.usePrivacyContext();
                 */
                updatePrivacy: (uuid, fieldName) => {
                  setPrivacy(Digit.Utils.updatePrivacy(uuid, fieldName) || {});
                },
              }}
            >
              <DigitUIWrapper stateCode={stateCode} enabledModules={enabledModules} defaultLanding={defaultLanding} />
            </PrivacyProvider.Provider>
          </ComponentProvider.Provider>
      </ErrorBoundary>
      </QueryClientProvider>
  );
};


const componentsToRegister = {
  SelectOtp,
  ChangeCity,
  ChangeLanguage,
  PrivacyComponent,
  OtpComponent,
};


export const initCoreComponents = () => {
  Object.entries(componentsToRegister).forEach(([key, value]) => {
    Digit.ComponentRegistryService.setComponent(key, value);
  });
};


```

After implementing this fix, we were finally able to see the login screen from the core module, though the login inputs were not functioning properly.

***

#### 3. Login Screen Frozen

**Issue:**

After resolving the queryClient errors, the login screen became visible but the login inputs were unresponsive.

**Root Cause:**

The issue occurred due to an error in the FormComposer component, which prevented user inputs from registering properly.

**Solution:**

The issue was fixed by updating the FormComposer component. Below are the code changes made to resolve this:

//I’ll add the code here soon

After implementing this fix, the login inputs started functioning correctly.

***

#### 4. Localization Issue

**Issue:**

The localization API was being called and stored in localStorage, but it was not working properly.

**Root Cause:**

The execution order of localization functions was incorrect. Previously, i18n was initialized inside the libraries module, which caused issues in execution.

**Solution:**

To fix this issue, we imported i18n inside Module.js of the core module instead of using it in libraries. This change ensured that localization was correctly set up.

Below are the code changes made inside the core module:

```
import { initI18n } from "@egovernments/digit-ui-libraries/src/translations";


const DigitUIWrapper = ({ stateCode, enabledModules, defaultLanding }) => {
  console.log("inside DigitUIWrapper of core");
  window.Digit["Hooks"] = Hooks || {};
  const { isLoading, data: initData={} } = Digit.Hooks.useInitStore(stateCode, enabledModules);
  if (isLoading) {
    return <Loader page={true} />;
  }
  const data=getStore(initData) || {};
  const i18n = getI18n();
  initWorkbenchComponents();
  if(!Digit.ComponentRegistryService.getComponent("PrivacyComponent")){
    Digit.ComponentRegistryService.setComponent("PrivacyComponent", PrivacyComponent);
  }
  return (
    <Provider store={data}>
      <Router>
        <BodyContainer>
          {Digit.Utils.getMultiRootTenant() ? (
            <DigitAppWrapper
              initData={initData}
              stateCode={stateCode}
              modules={[
                {
                  "module": "assignment",
                  "code": "assignment",
                  "active": true,
                  "order": 13,
                  "tenants": [
                    {
                      "code": "mz"
                    }
                  ]
                },
                {
                  "module": "HRMS",
                  "code": "HRMS",
                  "active": true,
                  "order": 4,
                  "tenants": [
                    {
                      "code": "mz"
                    }
                  ]
                }
              ]}
              appTenants={initData.tenants}
              logoUrl={initData?.stateInfo?.logoUrl}
              logoUrlWhite={initData?.stateInfo?.logoUrlWhite}
              defaultLanding={defaultLanding}
            />
          ) : (
            <DigitApp
              initData={initData}
              stateCode={stateCode}
              modules={initData?.modules}
              appTenants={initData.tenants}
              logoUrl={initData?.stateInfo?.logoUrl}
              defaultLanding={defaultLanding}
            />
          )}
        </BodyContainer>
      </Router>
    </Provider>
  );
};
```

After implementing this fix, localization started working as expected.

### 5. QueryClient Error \[Revisit - Permanent Fix]

**Issue:**

Issue here is same as discussed in point number 2 but the solution discussed in point number 2 for QueryClient Error was a temporary fix and is not recommended at all because we can’t have libraries in local all the time and then import the methods from local library to local.

**Solution:**

To resolve this,\
(a) We simply added @tanstack/react-query" in externals of webpack config of each module/package. For ex:

```
externals: {
    react: {
      commonjs: 'react',
      commonjs2: 'react',
      amd: 'react',
      root: 'React',
    },
    'react-dom': {
      commonjs: 'react-dom',
      commonjs2: 'react-dom',
      amd: 'react-dom',
      root: 'ReactDOM',
    },
    'react-i18next': 'react-i18next',
    'react-router-dom': 'react-router-dom',
    "@tanstack/react-query": "@tanstack/react-query"
  },
```

(b) Also, we need to add @tanstack/react-query in peer dependencies of package.json as we don’t want duplicate instances of @tanstack/react-query to be installed. We want a centralized @tanstack/react-query which will be handled at root level (package.json of micro-ui-internals)

#### 6. App crash on any particular action, ex: props.OnChange is not a function

**Issue:**

Sometimes while navigating through the app, you may encounter a situation where on a particular click or change in input field the app gets crashed and it throws errors like : props.OnChange is not a function.

**Root Cause:**

The issue comes from mostly formcomposer and inboxsearchcomposer where react-hook-form library is being frequently used.

**Solution:**

After hours and hours of debugging, we found that it’s just about syntax changes introduced in the latest version of react-hook-form. We can’t directly use props in render like this : render(props)\
\
It should be destructured to field and then can access onChange from field like : render({field})\
Here you can use, field.props → Valid syntax\
\
Since we were upgrading to the latest dependencies, we updated react-hook-form to version 7 from 6 and didn’t handle the syntax.\
\
To fix this issue, you have two options: either use the latest version with correct valid syntax or just stick with the older version i.e, 6.15.8.\
In my case, I switched back to the older version and it works fine with react19.

#### 7. Package “xyz” not found, during build

**Issue:**

While build and deployment through github workflows or jenkins pipeline we might face this error : Package “xyz” not found.

**Root Cause:**

This issue arises because the system is unable to identify the “dist” file of a particular package or module.

**Solution:**

Please make sure we have correct main and module in package.json and correct output in webpack config.\
\
Incorrect Method :&#x20;

```
Package.json

"main": "dist/main.js",
  "module": "dist/main.js",

Webpack config

output: {
    filename: "Main.js",
```

\
correct Method :&#x20;

```
Package.json

"main": "dist/main.js",
  "module": "dist/main.js",

Webpack config

output: {
    filename: "main.js",
```

#### 8. Incorrect Proxy Issue:

After build and deployment(or during development in some cases), you might find any route is not working and is leading to “can’t get” or “not found” on the webpage.

**Root Cause:**

This issue arises due to incorrect proxy setup in webpack config of example where all the proxies rest.

**Solution:**

Just make sure that whatever environment you’re using, that proxy url should match with your webpack target proxy url.\
For ex :\
Your env is using REACT\_APP\_PROXY\_API=[https://unified-qa.digit.org](https://unified-qa.digit.org) then you should also use [https://unified-qa.digit.org](https://unified-qa.digit.org) in webpack config as target.

```
target: "https://unified-qa.digit.org",
```
