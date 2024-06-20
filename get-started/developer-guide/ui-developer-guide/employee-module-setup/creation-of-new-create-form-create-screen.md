# Create Form - Create Screen

## Introduction

The guide walks you through the steps required to create and integrate a form within a micro-frontend architecture using the DIGIT framework. You will learn how to set up the form configuration, create a custom component, and integrate the form with backend APIs.&#x20;

## Steps

<details>

<summary>Create Application Form</summary>

1. Create a form where users can enter all required information and submit the form.
2. Update the Index.js file with routes.

<!---->

3. `Index.js` will import **FormcomposerV2**. Add the heading, label, and form components inside it. Import the configuration file containing the form schema mapping detail (refer to the code below) into the create screen.

```
import { newConfig } from "../../configs/IndividualCreateConfig";
const configs = newConfig?newConfig:newConfig;
```

An example of a Create Screen is given below. Create a page IndividualCreate.js under the following path:

```
/micro-ui-internals/packages/modules/sample/src/pages/employee/IndividualCreate.js
```

```
import React, { useState } from "react";
import { useTranslation } from "react-i18next";
import { useHistory } from "react-router-dom";
import { FormComposerV2 } from "@egovernments/digit-ui-react-components";
import useCustomAPIMutationHook from "../../hooks/useCustomAPIMutationHook";
import { newConfig } from "../../configs/IndividualCreateConfig";

const IndividualCreate = () => {
  const [toastMessage, setToastMessage] = useState("");
  const tenantId = Digit.ULBService.getCurrentTenantId();
  const { t } = useTranslation();
  const history = useHistory();
  const [gender, setGender] = useState("");
  const reqCreate = {
    url: `/individual/v1/_create`,
    params: {},
    body: {},
    config: {
      enable: false,
    },
  };

  const mutation = useCustomAPIMutationHook(reqCreate);

  const handleGenderChange = (e) => {
    setGender(e.target.value);
  };

  return (
    <div>
      <h1> Create Individual</h1>
      <FormComposerV2
        label={t("Submit")}
        config={newConfig.map((config) => {
          return {
            ...config,


          };
        })}
        defaultValues={{}}
        onSubmit={(data,) => onSubmit(data, )}
        fieldStyle={{ marginRight: 0 }}

      />
        {/* Toast Component */}
        {toastMessage && (
        <div style={{ backgroundColor: "lightblue", padding: "10px", borderRadius: "5px", marginTop: "10px" }}>
          <div>{toastMessage}</div>
        </div>
      )}
    </div>
  );
}

export default IndividualCreate;
```

Reference for the create screen: [IndividualCreate.js](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/micro-ui-internals/packages/modules/sample/src/pages/employee/IndividualCreate.js)

</details>

<details>

<summary>Filling in Config.js</summary>

#### File Creation Path

Create a file named `IndividualCreateConfig.js` in the following path:

```
/micro-ui-internals/packages/modules/sample/src/configs/IndividualCreateConfig.js
```

The configuration file outlines the form's meta-data and structure. The "head" field contains the form heading, while the form's components are placed in the "body" field.

This configuration file is imported into the Create screen.

```
 export const newConfig = [
    {
   head: "Create Individual",   
    body: [
        {
          inline: true,
          label: "Applicant Name",
          isMandatory: false,
          key: "applicantname",
          type: "text",
          disable: false,
          populators: { name: "applicantname", error: "Required", validation: { pattern: /^[A-Za-z]+$/i } },
        },
        {
          inline: true,
          label: "date of birth",
          isMandatory: false,
          key: "dob",
          type: "date",
          disable: false,
          populators: { name: "dob", error: "Required"},
        },


        {
          isMandatory: true,
          key: "genders",
          type: "dropdown",
          label: "Enter Gender",
          disable: false,
          populators: {
            name: "genders",
            optionsKey: "name",
            error: "required ",
            mdmsConfig: {
              masterName: "GenderType",
              moduleName: "common-masters",
              localePrefix: "COMMON_GENDER",
            },
          },
        },

        {
          label: "Phone number",
          isMandatory: true,
          key: "phno",
          type: "number",
          disable: false,
          populators: { name: "phno", error: "Required", validation: { min: 0, max: 9999999999 } },
        },
      ],
    },

```

An example of the configuration file is available here: [IndividualCreate-Config.js](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/micro-ui-internals/packages/modules/sample/src/configs/IndividualCreateConfig.js)

</details>

<details>

<summary>Custom Component</summary>

* To meet unique requirements, we can design custom components in our application.
*   Begin by creating a custom component featuring the necessary specifications. The Panel component displays responsive messages, similar to informational cards. This enables users to display dynamic text.

    Create a **Panel.js** file in the specified path.

```
micro-ui-internals/packages/modules/sample/src/components/Panel.js
```

* Refer to the code for the panel in the link here - [Panel.js](https://github.com/egovernments/DIGIT-UI-LIBRARIES/blob/develop/react/ui-components/src/atoms/Panels.js)
* Import the custom component in the Module.js file.

```
import Panel from "./components/Panel.js";
```

* Add the custom component to the Module.js file

```
const componentsToRegister = {
  SampleModule,
  SampleCard,
  Panel
};
```

* To include the **Panel** Component in your configuration file, specify the **component name** and **type** as "component". Refer to the code below to find how to do it:

```
{
  "label": "Panel Name",
  "type": "component",
  "isMandatory": false,
  "key": "panel",
  "component": "Panel",
  "customProps": {
    "module": "HCM"
  },
    "populators": {
      "name": "panel",
      "error": "sample error message for panel"
    },
    "validation": {
      "min": 1,   
      "max": 10 
    }
}

```

</details>

<details>

<summary>Enable Module in the UI framework</summary>

* Click on [http://localhost:3000/digit-ui/employee](http://localhost:3000/digit-ui/employee) to see the UI.
* Access the create form screen by navigating to the URL below.&#x20;

```
/sample/create-individual
```

* The screen is similar to the image below, illustrating the Create Form.

<img src="../../../../.gitbook/assets/image (5).png" alt="" data-size="original">

</details>

<details>

<summary>Integration with Backend API</summary>

We have completed the UI for the Employee module. Now, let's integrate it with the backend API.

**Hooks**\
We will implement custom hooks in our code to handle data transfers to the backend. These hooks will make API calls and format the responses accordingly.\
Refer to the link - [Common Hooks](https://app.gitbook.com/o/-MEQmzNGXk5ajuZujG7E/s/egsIWleSdyH9rMLJ8ShI/\~/changes/95/guides/developer-guide/ui-developer-guide/create-a-new-ui-module-package/common-hooks)

After setting up the backend service, we will use hooks or a service to send data to the backend upon form submission.

This On Submit function is added to the Create screen.

```
    const onSubmit = async(data) => {
    console.log(data, "data");
    setToastMessage("Form submitted successfully!");
    await mutation.mutate(
      {
        url: `/individual/v1/_create`,
        params: { tenantId: "pg.citya" },
        body: {
          Individual: {
            tenantId: "pg.citya",
            name: {
              givenName: data.applicantname,
            },
            dateOfBirth: null,
            gender: data.genders.code,
            mobileNumber: data.phno,
            address: [
              {
                tenantId: "pg.citya",
                pincode: data.pincode,
                city: data.city,
                street: data.street,
                doorNo: data.doorno,
                "locality":
                {
                  "code" : data.locality.code,
                },
                landmark: data.landmark,
                "type": "PERMANENT"
              },
            ],
            identifiers: null,
            skills: [
                {
                    "type": "DRIVING",
                    "level": "UNSKILLED"
                }
            ],
            "photograph": null,
            additionalFields: {
                "fields": [
                    {
                        "key": "EMPLOYER",
                        "value": "ULB"
                    }
                ]
            },
            isSystemUser: null,
            userDetails: {
                "username": "8821243212",
                "tenantId": "pg.citya",
                "roles": [
                    {
                        "code": "SANITATION_WORKER",
                        "tenantId": "pg.citya"
                    }
                ],
                "type": "CITIZEN"
            },
        },
      },
        config: {
          enable: true,
        },
      },
    );

    const configs = newConfig;

  };
```

Refer to the file here - [IndividualCreate.js](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/micro-ui-internals/packages/modules/sample/src/pages/employee/IndividualCreate.js)\
Once the integration is complete the data is saved into the database.

</details>
