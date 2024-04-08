# Module.js



<details>

<summary>Registering the module and components</summary>

Module.js is the entry point where we can register all components and modules.So here we need to register all the components, links, code etc.This file serves as a central place for initializing modules within your application.\
\
Create a file Module.js under the following path:

```
micro-ui-internals/packages/modules/sample/src/Module.js
```

```
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


```

\
**Component Registration**: React applications often consist of numerous components responsible for rendering UI elements and encapsulating functionality. Registering these components allows them to be easily accessed and rendered within different parts of the application.So these components are registered in Module.js

```
const componentsToRegister = {
SampleModule,
  SampleCard
};
init <modulename >component
export const initSampleComponents = () => {
  Object.entries(componentsToRegister).forEach(([key, value]) => {
    Digit.ComponentRegistryService.setComponent(key, value);
  });
};


```

Refer the file below:\
[Module.js](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/micro-ui-internals/packages/modules/sample/src/Module.js)

\


</details>

<details>

<summary>UICustomizations</summary>

The UICustomizations object serves as a repository for middle ware functions that customize the user interface behaviour based on different module names within the application. These functions intercept UI-related operations, such as payload updates,inbox module configuration, and customization of search configurations, facilitating dynamic and modular UI customization in the application. Create UICustomizations under the following path:

Create UICustomizations.js under the following path:

```
micro-ui-internals/packages/modules/sample/src/configs/UICustomizations.js
```

```
import { Link, useHistory } from "react-router-dom";
import _ from "lodash";
import React from "react";

//create functions here based on module name set in mdms(eg->SearchProjectConfig)
//how to call these -> Digit?.Customizations?.[masterName]?.[moduleName]
// these functions will act as middlewares
// var Digit = window.Digit || {};

const businessServiceMap = {};

const inboxModuleNameMap = {};

export const UICustomizations = {};
```



The UICustomizations object is linked to the module.js file by importing it into the relevant components or modules and calling its functions to customize the user interface behavior based on module names and other parameters, facilitating UI in the application.

Refer the link below:\
[UICusttomisations](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/micro-ui-internals/packages/modules/sample/src/configs/UICustomizations.js)\
\


</details>



