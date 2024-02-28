---
description: Writing citizen module logic
---

# Write Citizen Module Code

## Overview

This section will walk you through the code that needs to be developed for the application.&#x20;

## Steps

Detailed user screen wireframes should be available at this point for development.

<details>

<summary>Create Application Form</summary>

1. Create a form where users can enter all required information and submit the form.&#x20;
2. Create a file called index.js in the path below:

`/web/micro-ui/internals/packages/module/br/src/pages/citizen/create/index.js`

3. `index.js` will import the **Formcomposer**. Inside this add the heading, label, and form components. The configuration file that will contain the actual form schema is mapped below in the following two lines. The newConfig.json file details are mentioned in the below sections.

```jsx
import { newConfig } from "../../../components/config/config";
const configs = newConfig?newConfig:newConfig;
```

```jsx
import { FormComposer } from "@egovernments/digit-ui-react-components";
import React from "react";
import { useTranslation } from "react-i18next";

import { newConfig } from "../../../components/config/config";

const Create = () => {
 
  const { t } = useTranslation();
  const configs = newConfig?newConfig:newConfig;

  return (
    <FormComposer
    heading={t("Create Birth Registration")}
    label={t("ES_COMMON_APPLICATION_SUBMIT")}
    config={configs.map((config) => {
      return {
        ...config,
        body: config.body.filter((a) => !a.hideInEmployee),
      };
    })}
  
    fieldStyle={{ marginRight: 0 }}
  />
  );
};

export default Create;
```

</details>

<details>

<summary>Filling in config.js</summary>

Create a file called config.js under the following path:

`/micro-ui/web/micro-ui-internals/packages/modules/br/src/components/config.js`

This file defines the form meta-data and structure. The form heading goes into the "head" field. Components inside the form go into the body field.

This form config has already been mapped in the `index.js` file and therefore will be rendered onto the screen.&#x20;

```
export const newConfig =[
    {
        "head": "Birth-Details",
        "body": [
         
            {
                type: "component",
                component: "BrSelectName",
                key: "BrSelectName",
                withoutLabel: true,
              },
              {
                type: "component",
                component: "BRSelectGender",
                key: "BRSelectPhoneGender",
                withoutLabel: true,
              },
              {
                type: "component",
                component: "BRSelectPhoneNumber",
                key: "BRSelectPhoneNumber",
                withoutLabel: true,
              },
              {
                type: "component",
                component: "BRSelectEmailId",
                key: "BRSelectEmailId",
                withoutLabel: true,
              },
          
              {
                type: "component",
                component: "BrSelectAddress",
                key: "BrSelectAddress",
                withoutLabel: true,
              },
              {
                type: "component",
                component: "SelectCorrespondenceAddress",
                key: "SelectCorrespondenceAddress",
                withoutLabel: true,
              },
        ]
    },

];
```

Components that we are using in `newConfig.js`:-\
\
[BrSelectName](https://github.com/egovernments/DIGIT-OSS/blob/a235f1eedef56652055d450924e8772e75bd1ac6/frontend/micro-ui/web/micro-ui-internals/packages/modules/br/src/pagecomponents/BrSelectName.js)\
[BrSelectGender](https://github.com/egovernments/DIGIT-OSS/blob/a235f1eedef56652055d450924e8772e75bd1ac6/frontend/micro-ui/web/micro-ui-internals/packages/modules/br/src/pagecomponents/BRSelectGender.js)\
[BrSelectPhoneNumber](https://github.com/egovernments/DIGIT-OSS/blob/a235f1eedef56652055d450924e8772e75bd1ac6/frontend/micro-ui/web/micro-ui-internals/packages/modules/br/src/pagecomponents/BrSelectPhoneNumber.js)\
[BrSelectEmailId](https://github.com/egovernments/DIGIT-OSS/blob/a235f1eedef56652055d450924e8772e75bd1ac6/frontend/micro-ui/web/micro-ui-internals/packages/modules/br/src/pagecomponents/SelectEmailId.js)\
[BrSelectAddress](https://github.com/egovernments/DIGIT-OSS/blob/a235f1eedef56652055d450924e8772e75bd1ac6/frontend/micro-ui/web/micro-ui-internals/packages/modules/br/src/pagecomponents/BrSelectAddress.js)\
[SelectCorrespondenceAddress](https://github.com/egovernments/DIGIT-OSS/blob/a235f1eedef56652055d450924e8772e75bd1ac6/frontend/micro-ui/web/micro-ui-internals/packages/modules/br/src/pagecomponents/SelectCorrespondenceAddress.js)



</details>

<details>

<summary>Routing</summary>

After adding the `config.js` and `create/index.js` , add routing for the birth registration form.&#x20;

Create the index.js into `br/src/pages/citizen/index.js` where we will add the private route. In `index.js`, we mention the path and component name which component we need to show or render when we hit that route.

```jsx
import { AppContainer, BackButton,PrivateRoute } from "@egovernments/digit-ui-react-components";
import React from "react";
import {  Switch, useRouteMatch } from "react-router-dom";

import { useTranslation } from "react-i18next";



const App = () => {
  const { path, url, ...match } = useRouteMatch();
  const { t } = useTranslation();

  const Create = Digit?.ComponentRegistryService?.getComponent("BRCreate");
  const Response = Digit?.ComponentRegistryService?.getComponent("Response");
  
  return (
    <span className={"pt-citizen"}>
      <Switch>
        <AppContainer>
        <BackButton>Back</BackButton> 
        
          <PrivateRoute path={`${path}/birth`} component={Create} />
          <PrivateRoute path={`${path}/response`} component={Response} />
        </AppContainer>
      </Switch>
    </span>
  );
};

export default App;

```

**Add a card on the citizen landing screen:**

![](<../../../../.gitbook/assets/image (225).png>)

Once the form is created and routing is added, we add the module card on our Digit-UI landing page for citizens.&#x20;



</details>

<details>

<summary><strong>Filling in module.js</strong></summary>

`module.js` is the entry point of every module e.g:- ( Birth-Registration, Property Tax ) so here we need to register all the components, links, code etc..

```jsx
import {  CitizenHomeCard, PTIcon } from "@egovernments/digit-ui-react-components";
import React, { useEffect } from "react";
import { useTranslation } from "react-i18next";
import { useRouteMatch } from "react-router-dom";
import CitizenApp from "./pages/citizen";
import Create from "./pages/citizen/create/index";
import EmployeeApp from "./pages/employee";
import BrSelectName from "./pagecomponents/BrSelectName";
import BRSelectPhoneNumber from "./pagecomponents/BrSelectPhoneNumber";
import BRSelectGender from "./pagecomponents/BRSelectGender";
import BRSelectEmailId from "./pagecomponents/SelectEmailId";
import BRSelectPincode from "./pagecomponents/BRSelectPincode";
import BrSelectAddress from "./pagecomponents/BrSelectAddress";
import SelectCorrespondenceAddress from "./pagecomponents/SelectCorrespondenceAddress";
import SelectDocuments from "./pagecomponents/SelectDocuments";
import BRCard from "./components/config/BRCard";
import BRManageApplication from "./pages/employee/BRManageApplication";
import RegisterDetails from "./pages/employee/RegisterDetails";
import Response from "./pages/citizen/create/Response";

const componentsToRegister = {
 Response,
  RegisterDetails,
  BRManageApplication,
  BRCard,
  SelectDocuments,
  SelectCorrespondenceAddress,
  BrSelectAddress,
  BRSelectPincode,
  BRSelectEmailId,
  BRSelectGender,
  BRSelectPhoneNumber,
  BrSelectName,
  BRCreate : Create,
};

export const BRModule = ({ stateCode, userType, tenants }) => {
  const { path, url } = useRouteMatch();

  const moduleCode = "BR";
  const language = Digit.StoreData.getCurrentLanguage();
  const { isLoading, data: store } = Digit.Services.useStore({ stateCode, moduleCode, language });

  if (userType === "citizen") {
    return <CitizenApp path={path} stateCode={stateCode} />;
  }

  return <EmployeeApp path={path} stateCode={stateCode} />;
};

export const BRLinks = ({ matchPath, userType }) => {
  const { t } = useTranslation();


  const links = [
  
    {
      link: `${matchPath}/birth`,
      i18nKey: t("Create BirthRegistration"),
    },
   
   
  ];

  return <CitizenHomeCard header={t("BirthRegistration")} links={links} Icon={() => <PTIcon className="fill-path-primary-main" />} />;
};

export const initBRComponents = () => {
  Object.entries(componentsToRegister).forEach(([key, value]) => {
    Digit.ComponentRegistryService.setComponent(key, value);
  });
};


```





</details>

<details>

<summary>Enable Module in the UI framework</summary>

After registering all components, links and module code we need to enable it in two places:\
1\) `Web/Src/app.js` : In app.js we import the BRModule, initBRComponents, and BRLinks and enable the BR module.

```jsx
import React from 'react';

import { initDSSComponents } from "@egovernments/digit-ui-module-dss";
import { PaymentModule, PaymentLinks, paymentConfigs } from "@egovernments/digit-ui-module-common";
import { DigitUI } from "@egovernments/digit-ui-module-core";
import { initLibraries } from "@egovernments/digit-ui-libraries";
import { initEngagementComponents } from "@egovernments/digit-ui-module-engagement";
import {initCustomisationComponents} from "./Customisations";
import { initCommonPTComponents } from "@egovernments/digit-ui-module-commonpt";
import { BRModule ,initBRComponents ,BRLinks} from "@egovernments/digit-ui-module-br";

initLibraries();
//"WS" removed the ws enabledModules ;
const enabledModules = ["Payment","QuickPayLinks", "DSS","Engagement", "BR"];
window.Digit.ComponentRegistryService.setupRegistry({
  ...paymentConfigs,
  PaymentModule,
  PaymentLinks,
  BRModule,
  BRLinks,

});

initBRComponents();
initDSSComponents();
initEngagementComponents();

initCustomisationComponents();

function App() {
  const stateCode = window.globalConfigs?.getConfig("STATE_LEVEL_TENANT_ID") || process.env.REACT_APP_STATE_LEVEL_TENANT_ID;
  if (!stateCode) {
    return <h1>stateCode is not defined</h1>
  }
  return (
    <DigitUI stateCode={stateCode} enabledModules={enabledModules}  />
  );
}

export default App;

```

2\) `web/micro-ui-internals/example/src/index.js` :\
In index.js, we will import the BRModule, initBRComponents, and BRLinks and enable the BR module.

```jsx
import React from "react";
import ReactDOM from "react-dom";
import { initLibraries } from "@egovernments/digit-ui-libraries";
import { BRModule, initBRComponents ,BRLinks} from "@egovernments/digit-ui-module-br";
import { initDSSComponents } from "@egovernments/digit-ui-module-dss";
import { PaymentModule, PaymentLinks, paymentConfigs } from "@egovernments/digit-ui-module-common";
import { initEngagementComponents } from "@egovernments/digit-ui-module-engagement";
import { DigitUI } from "@egovernments/digit-ui-module-core";
import "@egovernments/digit-ui-css/example/index.css";



var Digit = window.Digit || {};

const enabledModules = [ "Payment","QuickPayLinks", "DSS","Engagement","BR"];

const initTokens = (stateCode) => {
  const userType = window.sessionStorage.getItem("userType") || process.env.REACT_APP_USER_TYPE || "CITIZEN";

  const token =window.localStorage.getItem("token")|| process.env[`REACT_APP_${userType}_TOKEN`];
 
  const citizenInfo = window.localStorage.getItem("Citizen.user-info")
 
  const citizenTenantId = window.localStorage.getItem("Citizen.tenant-id") || stateCode;

  const employeeInfo = window.localStorage.getItem("Employee.user-info");
  const employeeTenantId = window.localStorage.getItem("Employee.tenant-id");

  const userTypeInfo = userType === "CITIZEN" || userType === "QACT" ? "citizen" : "employee";
  window.Digit.SessionStorage.set("user_type", userTypeInfo);
  window.Digit.SessionStorage.set("userType", userTypeInfo);

  if (userType !== "CITIZEN") {
    window.Digit.SessionStorage.set("User", { access_token: token, info: userType !== "CITIZEN" ? JSON.parse(employeeInfo) : citizenInfo });
  } else {
    // if (!window.Digit.SessionStorage.get("User")?.extraRoleInfo) window.Digit.SessionStorage.set("User", { access_token: token, info: citizenInfo });
  }

  window.Digit.SessionStorage.set("Citizen.tenantId", citizenTenantId);
 
 if(employeeTenantId && employeeTenantId.length) window.Digit.SessionStorage.set("Employee.tenantId", employeeTenantId);
};

const initDigitUI = () => {
  window?.Digit.ComponentRegistryService.setupRegistry({

    PaymentModule,
    BRModule,
    PaymentLinks,
    BRLinks,
 
  });


  initDSSComponents();
  initEngagementComponents();
  initBRComponents();



  
  const stateCode = window?.globalConfigs?.getConfig("STATE_LEVEL_TENANT_ID") || "pb";
  initTokens(stateCode);

  const registry = window?.Digit.ComponentRegistryService.getRegistry();
  ReactDOM.render(<DigitUI stateCode={stateCode} enabledModules={enabledModules} />, document.getElementById("root"));
};

initLibraries().then(() => {
  initDigitUI();
});

```

Once we enable the BR module in app.js and index.js, the module will be available in the UI. Click on [http://localhost:3000/digit-ui/citizen](http://localhost:3000/digit-ui/citizen) to see the UI.

In `modules/core/src/pages/citizen/Home/index.js,` add the following:

```
{
        name: t("Birth-Registration"),
        Icon: <OBPSIcon />,
        onClick: () => history.push("/digit-ui/citizen/br-home"),
      },
```

Once we add the link to the homepage,we can see the birth-registration module on our Digit-UI Homepage.&#x20;

Now, let's add the homepage card for the citizen module.

```jsx
import {
    Calender, CardBasedOptions, CaseIcon, ComplaintIcon, DocumentIcon, HomeIcon, Loader, OBPSIcon, PTIcon, StandaloneSearchBar, WhatsNewCard
} from "@egovernments/digit-ui-react-components";
import React from "react";
import { useTranslation } from "react-i18next";
import { useHistory } from "react-router-dom";

const Home = () => {
  const { t } = useTranslation();
  const history = useHistory();
  const tenantId = Digit.ULBService.getCitizenCurrentTenant(true);
  const { data: { stateInfo } = {}, isLoading } = Digit.Hooks.useStore.getInitData();

  const conditionsToDisableNotificationCountTrigger = () => {
    if (Digit.UserService?.getUser()?.info?.type === "EMPLOYEE") return false;
    if (!Digit.UserService?.getUser()?.access_token) return false;
    return true;
  };

  const { data: EventsData, isLoading: EventsDataLoading } = Digit.Hooks.useEvents({
    tenantId,
    variant: "whats-new",
    config: {
      enabled: conditionsToDisableNotificationCountTrigger(),
    },
  });

  if (!tenantId) {
    history.push(`/digit-ui/citizen/select-language`);
  }

  const allCitizenServicesProps = {
    header: t("DASHBOARD_CITIZEN_SERVICES_LABEL"),
    sideOption: {
      name: t("DASHBOARD_VIEW_ALL_LABEL"),
      onClick: () => history.push("/digit-ui/citizen/all-services"),
    },
    options: [
     
     
      {
        name: t("Birth-Registration"),
        Icon: <OBPSIcon />,
        onClick: () => history.push("/digit-ui/citizen/br-home"),
      },
     
    ],
    styles: { display: "flex", flexWrap: "wrap", justifyContent: "flex-start", width: "100%" },
  };
  const allInfoAndUpdatesProps = {
    header: t("CS_COMMON_DASHBOARD_INFO_UPDATES"),
    sideOption: {
      name: t("DASHBOARD_VIEW_ALL_LABEL"),
      onClick: () => {},
    },
    options: [
      {
        name: t("CS_HEADER_MYCITY"),
        Icon: <HomeIcon />,
      },
      {
        name: t("EVENTS_EVENTS_HEADER"),
        Icon: <Calender />,
        onClick: () => history.push("/digit-ui/citizen/engagement/events"),
      },
      {
        name: t("CS_COMMON_DOCUMENTS"),
        Icon: <DocumentIcon />,
        onClick: () => history.push("/digit-ui/citizen/engagement/docs"),
      },
      {
        name: t("CS_COMMON_SURVEYS"),
        Icon: <DocumentIcon />,
        onClick: () => history.push("/digit-ui/citizen/engagement/surveys/list"),
      },
     
    ],
    styles: { display: "flex", flexWrap: "wrap", justifyContent: "flex-start", width: "100%" },
  };

  return isLoading ? (
    <Loader />
  ) : (
    <div className="HomePageWrapper">
      <div className="BannerWithSearch">
        <img src={stateInfo?.bannerUrl} />
        <div className="Search">
          <StandaloneSearchBar placeholder={t("CS_COMMON_SEARCH_PLACEHOLDER")} />
        </div>
      </div>

      <div className="ServicesSection">
        <CardBasedOptions {...allCitizenServicesProps} />
        <CardBasedOptions {...allInfoAndUpdatesProps} />
      </div>

      {conditionsToDisableNotificationCountTrigger() ? (
        EventsDataLoading ? (
          <Loader />
        ) : (
          <div className="WhatsNewSection">
            <div className="headSection">
              <h2>{t("DASHBOARD_WHATS_NEW_LABEL")}</h2>
              <p onClick={() => history.push("/digit-ui/citizen/engagement/whats-new")}>{t("DASHBOARD_VIEW_ALL_LABEL")}</p>
            </div>
            <WhatsNewCard {...EventsData?.[0]} />
          </div>
        )
      ) : null}
    </div>
  );
};

export default Home;

```





</details>

<details>

<summary>Integration with Backend API</summary>

We have done with the UI part for the citizen module. Now, we will see how to integrate it with the backend API.

**Service**

We create a service where we mention the API's call e.g:- POST, GET, PUT, PATCH, etc.\
basically, we will create a request inside the request we pass the data, URL, method, auth, and other params.

```javascript
import Urls from "../atoms/urls";
import { Request } from "../atoms/Utils/Request";

const BRService = {
  
  create: (data, tenantId) =>
    Request({
      data: data,
      url: Urls.br.create,
      useCache: false,
      method: "POST",
      auth: true,
      userService: true,
      params: { tenantId },
    }),
    get: (data, tenantId) =>
    Request({
      data: data,
      url: Urls.br.get,
      useCache: false,
      method: "GET",
      auth: true,
      userService: true,
      params: { tenantId },
    }),
};

export default BRService;

```

In Request, we pass the URL so that the URL we mention or add into the `service/atoms/url.js`

```javascript
br: {
    create: "https://62f0e3e5e2bca93cd23f2ada.mockapi.io/user",
    get:"https://62f0e3e5e2bca93cd23f2ada.mockapi.io/user",
    
  },
```

**Hooks**

Once BRService is created with all requests then will create a Hook and that hook we will use in our code to pass the data to the backend.

```jsx
import { useQuery, useMutation } from "react-query";

import BRService from "../../services/elements/BR";

export const useBRCreate = (tenantId, config = {}) => {
  return useMutation((data) => BRService.create(data, tenantId));
};

export default useBRCreate;

```

After creating Service and Hooks we need to register it into `packages/ libraries/src/index.js`

```jsx
import Enums from "./enums/index";
import mergeConfig from "./config/mergeConfig";
import { useStore } from "./services/index";
import { initI18n } from "./translations/index";
import { Storage, PersistantStorage } from "./services/atoms/Utils/Storage";
import { UserService } from "./services/elements/User";
import { ULBService } from "./services/molecules/Ulb";
import Hooks from "./hooks";
import { subFormRegistry } from "./subFormRegistry";
import BRService from "./services/elements/BR";

const setupLibraries = (Library, props) => {
  window.Digit = window.Digit || {};
  window.Digit[Library] = window.Digit[Library] || {};
  window.Digit[Library] = { ...window.Digit[Library], ...props };
};

const initLibraries = () => {
  setupLibraries("SessionStorage", Storage);
  setupLibraries("PersistantStorage", PersistantStorage);
  setupLibraries("UserService", UserService);
  setupLibraries("ULBService", ULBService);

  setupLibraries("Config", { mergeConfig });
  setupLibraries("Services", { useStore });

  setupLibraries("BRService", BRService);
  

  return new Promise((resolve) => {
    initI18n(resolve);
  });
};

export { initLibraries, Enums, Hooks, subFormRegistry };

```

We have setup the backend service, and now we will use the hooks or service to send the data to the backend after submitting the form.

Add the onSubmit function in this file: (`br/src/pages/citizen/create/index.js`) and in that function, we are passing the user’s entered data to the BRService that we have created.

```jsx
import { FormComposer, Loader } from "@egovernments/digit-ui-react-components";
import React, {  useState } from "react";
import { useTranslation } from "react-i18next";
import { useHistory } from "react-router-dom";
import { newConfig } from "../../../components/config/config";

const Create = () => {
  const tenantId = Digit.ULBService.getCurrentTenantId();
  const { t } = useTranslation();
  const history = useHistory();
  

  const onSubmit = (data) => {

    let Users = [
      {

        user: {
          babyFirstName: data?.BrSelectName?.babyFirstName,
          babyLastName: data?.BrSelectName?.babyLastName,
          fatherName: data?.BrSelectName?.fatherName,
          motherName: data?.BrSelectName?.motherName,
          gender: data?.BrSelectGender?.gender,
          doctorName: data?.BrSelectName?.doctorName,
          hospitalName: data?.BrSelectName?.hospitalName,
          placeOfBirth: data?.BrSelectName?.placeOfBirth,
          applicantMobileNumber: data?.BRSelectPhoneNumber?.applicantMobileNumber,
          altMobileNumber: data?.BRSelectPhoneNumber?.altMobileNumber,
          emailId: data?.BRSelectEmailId?.emailId,
          permanentAddress: data?.BrSelectAddress?.permanentAddress,
          permanentCity: data?.BrSelectAddress?.permanentCity,
          correspondenceCity: data?.SelectCorrespondenceAddress?.correspondenceCity,
          correspondenceAddress: data?.SelectCorrespondenceAddress?.correspondenceAddress,
          bloodGroup: data?.SelectCorrespondenceAddress?.bloodGroup,
          tenantId: tenantId,
        },
        
      },
    ];
      /* use customiseCreateFormData hook to make some chnages to the Employee object */
     Digit.BRService.create(Users, tenantId).then((result,err)=>{
       let getdata = {...data , get: result }
       onSelect("", getdata, "", true);
       console.log("daaaa",getdata);
     })
     .catch((e) => {
     console.log("err");
    });

    history.push("/digit-ui/citizen/br/response");

    console.log("getting data",Users)
    
  };
 
  
  /* use newConfig instead of commonFields for local development in case needed */

  const configs = newConfig?newConfig:newConfig;

  return (
    <FormComposer
    heading={t("Create Birth Registration")}
    label={t("ES_COMMON_APPLICATION_SUBMIT")}
    config={configs.map((config) => {
      return {
        ...config,
        body: config.body.filter((a) => !a.hideInEmployee),
      };
    })}
    onSubmit={onSubmit}
    fieldStyle={{ marginRight: 0 }}
  />
  );
};

export default Create;

```





</details>

Once the integration is done the data will be saved into the database.

\


[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this website by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
