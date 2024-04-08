# Common Hooks

We can create customized versions of React hooks such as `useCustomAPIMutationHook` to adjust how our application interacts with APIs. By crafting these custom hooks, we can tailor how data is fetched and managed, ensuring it aligns with our specific needs.

This custom hook, `useCustomAPIMutationHook`, facilitates making API calls with mutation operations in React applications using the `react-query` library. It handles mutation requests to a specified URL, including parameter and body customization, while providing loading indicators and data management functionalities, thereby simplifying API interaction and state management in components.

Create `useCustomAPIMutationHook` under the following path:

```
micro-ui-internals/packages/libraries/src/hooks/useCustomAPIMutationHook.js
```

```
import { useQueryClient, useMutation } from "react-query";
import { CustomService } from "../services/elements/CustomService";

 const requestCriteria = [
      "/user/_search",             // API details
    {},                            //requestParam
    {data : {uuid:[Useruuid]}},    // requestBody
    {} ,                           // privacy value 
    {                              // other configs
      enabled: privacyState,
      cacheTime: 100,
      select: (data) => {
                                    // format data
        return  _.get(data, loadData?.jsonPath, value);
      },
    },
  ];
  const mutation = Digit.Hooks.useCustomAPIMutationHook(...requestCriteria);


while mutating use the following format 

mutation.mutate({
          params: {},
          body: { "payload": {
                   // custom data
                } 
          }},
          {
            onError : ()=> { // custom logic},
            onSuccess : ()=> { // custom logic}
          }
        );


const useCustomAPIMutationHook = ({ url, params, body, config = {}, plainAccessRequest, changeQueryName = "Random" }) => {
  const client = useQueryClient();

  const { isLoading, data, isFetching, ...rest } = useMutation(
    (data) => CustomService.getResponse({ url, params: { ...params, ...data?.params }, body: { ...body, ...data?.body }, plainAccessRequest }),
    {
      cacheTime: 0,
      ...config,
    }
  );
  return {
    ...rest,
    isLoading,
    isFetching,
    data,
    revalidate: () => {
      data && client.invalidateQueries({ queryKey: [url].filter((e) => e) });
    },
  };
};

export default useCustomAPIMutationHook;
```

#### Overriding the hook

To override the `useCustomAPIMutationHook`, you would need to create a new custom hook with the desired enhancements.When considering overriding `useCustomAPIMutationHook`, users should first identify specific modifications required, such as adding additional parameters or altering data processing logic. Then, they can create a new custom hook, preserving the original hook's functionality while incorporating these modifications to better suit their application's needs.

We need to replace the usage of the original hook throughout the codebase with the new custom hook. This ensures that wherever the original hook was used, the modified functionality of the custom hook will be applied instead.

There is a hook called `useCustomMDMSV2`, which is used for getting data from a Multi-Domain Master Service (MDMS) API. This hook makes it easier to request data, handle loading, and prepare the received data for use in React applications.

`useCustomMDMSV2`

Create the hook under the following path:

```
micro-ui-internals/packages/modules/Sample/src/hooks/useCustomMDMSV2.js
```

```
export const useCustomMDMSV2 = ({ tenantId, schemaCode, select, changeQueryName = "Random",filters={},config={} }) => {
  
  const requestCriteria = {
    url: "/mdms-v2/v2/_search",
    body: {
      tenantId,
      MdmsCriteria: {
        // tenantId, //changing here to send user's tenantId always whether stateId or city
        tenantId: Digit.ULBService.getCurrentTenantId(),
        filters: filters,
        schemaCode: schemaCode,
        isActive: true,
        limit: 100
      },
    },
    config: {
      select: select
        ? select
        : (response) => {
            //mdms will be an array of master data
            const { mdms } = response;
            //first filter with isActive
            //then make a data array with actual data
            //refer the "code" key in data(for now) and set options array , also set i18nKey in each object to show in UI
            const options = mdms?.map((row) => {
              return {
                i18nKey: Digit.Utils.locale.getTransformedLocale(`${row?.schemaCode}_${row?.data?.code}`),
                ...row.data,
              };
            });
            return options;
          },
          ...config
    },
    changeQueryName,
  };
  const { isLoading, data } = Digit.Hooks.useCustomAPIHook(requestCriteria);
  return { isLoading, data };
};
```





<details>

<summary>Creating  New Hook</summary>

We can also create custom hooks like `useIndividualView` to simplify tasks like fetching data for specific screens.

Create the hook  `useIndividualView` under the following path:

```
micro-ui-internals/packages/modules/sample/src/hooks/useIndividualView.js
```

```
import { useQuery } from "react-query";
import { sampleService } from "./services/sampleService";
import { searchTestResultData } from "./services/searchTestResultData";

export const useIndividualView = ({t,individualId,tenantId,config={} }) =>{
  //console.log(props);
  console.log(individualId,'test');
  return useQuery(["Individual Details"], () => searchTestResultData({ t, individualId, tenantId }), config);
};
```

This `searchTestResultData` function is used within the `useIndividualView` hook to fetch data related to a specific individual. It utilizes an asynchronous operation to send a request to a server endpoint, retrieves the response, and then processes the data to extract relevant details. The extracted details are then returned, providing necessary information for rendering the individual's view within the application.\
\
Create the Function `searchTestResultData` under the following path:

```
micro-ui-internals/packages/modules/sample/src/hooks/services/searchTestResultData.js
```

```
export const searchTestResultData = async ({ t, individualId, tenantId }) => {
  
  const response = await Digit.CustomService.getResponse({
    url: "/individual/v1/_search",
   
    params: {
      tenantId: "pg.citya",
      offset: 0,
      limit: 10,
      
    },
    body: {
        Individual: {
          "tenantId": "pg.citya",
          "individualId": individualId,
        },
      },
   
  });
  console.log("response", response);

 
  return {
    details: [
      {
         sections: [
           {
            type: "DATA",
             values: [
              {
                key: "Applicant name",
                value: response?.Individual?.[0]?.name?.givenName || "NA",
              },
              {
                key: "Applicant Id",
                value: response?.Individual?.[0]?.identifiers?.[0].individualId || "NA",
              },
               {
                 key : "Adress",
                value : response?.Individual?.[0]
             }
            ],
          }
         ],
       },
     ],
   };
        }
```

Reference of using this hook on a view screen:\


[ViewIndividual.js](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/micro-ui-internals/packages/modules/sample/src/configs/ViewIndividual.js)



</details>



<details>

<summary>Registering the Hooks</summary>

In order to register  hooks in your application, they should be exported from an `index.js` file like this. Ensure that each custom hook is correctly exported within this file for seamless integration and usage across your application.\
\
Create an`index.js`  file under the following path:

```
micro-ui-internals/packages/modules/sample/src/hooks/index.js
```

```
const sample = {
  useIndividualView
};

const Hooks = {
  sample,
};
```

Refer the file below:\
[index.js](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/micro-ui-internals/packages/modules/sample/src/hooks/index.js)\


</details>
