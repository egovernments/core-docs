# Creation of new Create Form (Create Screen)

<details>

<summary>Routing</summary>

Routing in a  application is essential for navigation and managing different views or pages based on the URL.

Create the index.js under the following path:

<pre><code><strong>micro-ui-internals/packages/modules/sample/src/pages/employee/index.js
</strong></code></pre>

\
In `index.js,` we will add the private route and we mention the path and component name which component we need to show or render when we hit that route.

```
 <PrivateRoute path={`${path}/sample-create`} component={() => <Create></Create>} />
 <PrivateRoute path={`${path}/inbox`} component={() => <Inbox></Inbox>} />       
```

Reference for routing and index.js file is given below:

[Index.js](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/micro-ui-internals/packages/modules/sample/src/pages/employee/index.js)

</details>

<details>

<summary>Create Application Form</summary>

1. Create a form where users can enter all required information and submit the form.
2. Update the Index.js file with routes

<!---->

3. `Index.js` will import the **FormcomposerV2**. Inside this add the heading, label, and form components. The configuration file that will contain the actual form schema is mapped in the section below. The config file needs to be imported in the create screen.

```
import { newConfig } from "../../configs/IndividualCreateConfig";
const configs = newConfig?newConfig:newConfig;
```

Example of a Create Screen is given below. Create a page IndividualCreate.js under the following path:

```
micro-ui-internals/packages/modules/sample/src/configs/IndividualCreateConfig.js
```

```
import React, { useState } from "react";
import { useTranslation } from "react-i18next";
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

Reference for the create screen:\
[IndividualCreate.js](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/micro-ui-internals/packages/modules/sample/src/pages/employee/IndividualCreate.js)

</details>

<details>

<summary>Filling in config.js<br></summary>

Create a file called newConfig.js under the following path:

```
micro-ui-internals/packages/modules/br/src/components/newConfig.js
```

This file defines the form meta-data and structure. The form heading goes into the "head" field. Components inside the form go into the body field.

This config file is being imported in the Create screen

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



Example for the config file is as given below:

[Config.js](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/micro-ui-internals/packages/modules/sample/src/configs/IndividualCreateConfig.js)

</details>

<details>

<summary>Custom Component</summary>

If we want, we can create custom components in our application. These components are designed specifically to address our unique requirements.\
1\) First we need to add that custom componet in Module.js file

```
const componentsToRegister = {
  SampleModule,
  SampleCard,
  ViewEstimatePage: ViewEstimateComponent,
};

```

Refer the file below:\
[Module.js](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/micro-ui-internals/packages/modules/sample/src/Module.js)\
\
2\) Create the Custom component \
This `ViewEstimateComponent` is an example of a custom component tailored to display estimate details and enable specific workflow actions within an application.\
Create `ViewEstimateComponent`file under the following path:

```
micro-ui-internals/packages/modules/sample/src/components/ViewEstimateComponent.js
```

Reference for the Custom Component is given below:

[ViewEstimateComponent](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/micro-ui-internals/packages/modules/sample/src/components/ViewEstimateComponent.js)\


3\)Give the same Component name in the config file for the field where you need that

Example of a page using this component\
[SampleView.js](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/micro-ui-internals/packages/modules/sample/src/pages/employee/SampleView.js)

</details>

<details>

<summary>Enable Module in the UI framework</summary>

Once we enable the Sample module in app.js and index.js, the module will be available in the UI. Click on [http://localhost:3000/digit-ui/employee](http://localhost:3000/digit-ui/employee) to see the UI.



</details>

<details>

<summary>Integration with Backend API</summary>

We have done with the UI part for the Emplopyee module. Now, we will see how to integrate it with the backend API.\


**Hooks**\
**We** will use  hooks in our code to pass the data to the backend.Custom hook which can make Api call and format response. \
Refer the link:\
[Common Hooks](https://app.gitbook.com/o/-MEQmzNGXk5ajuZujG7E/s/egsIWleSdyH9rMLJ8ShI/\~/changes/95/guides/developer-guide/ui-developer-guide/create-a-new-ui-module-package/common-hooks)

We have setup the backend service, and now we will use the hooks or service to send the data to the backend after submitting the form.

This On Submit function should be added in the Create screen.

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

Refer the file below:\
[IndividualCreate.js](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/micro-ui-internals/packages/modules/sample/src/pages/employee/IndividualCreate.js)\
\
Once the integration is done the data will be saved into the database.



</details>
