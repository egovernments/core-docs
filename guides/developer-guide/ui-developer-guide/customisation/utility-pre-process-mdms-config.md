# Utility - Pre-Process MDMS Config

Overview

This utility is developed to convert the MDMS config into FormComposer and InboxFormComposer config. Basically, every UI configuration needs some dependent parameters. These params could be a dropdown dependency or a custom class we want to pass at runtime based on some logic. Since the config is a JSON put into MDMS, we cannot use variables directly inside it. To handle this use case, we have written a utility that will convert this JSON to a param-based JSON.

How does this utility works ?

This utility is like an engine that takes MDMS config and dependent parameters and returns a param enabled config, which formcomposer and inbox form composer can use to render the UI elements.\


Below is the way we need to set the MDMS config -&#x20;

```json
{
             "isMandatory": true,
             "key": "noSubProject_ward",
             "type": "radioordropdown",
             "label": "PDF_STATIC_LABEL_ESTIMATE_WARD",
             "disable": false,
             "preProcess": {
               "updateDependent": [
                 "populators.options"
               ]
             },
             "populators": {
               "name": "noSubProject_ward",
               "optionsKey": "i18nKey",
               "error": "WORKS_REQUIRED_ERR",
               "required": false,
               "optionsCustomStyle": {
                 "top": "2.5rem"
               },
               "options": []
             }
           },

```

Here, we need to pass the JSON path of the dependent key we need to update at runtime. In the example above, we are targeting “populators.options”, So we want to update the options at runtime based on some logic.&#x20;

Note :

1. We always need to pass the JSON path in an array
2. Also, the order in which we are passing these JSON path are important. Later on, we will use this order to target the respective dependent object.

Now, once we set the config as above, we will put this config in MDMS. So, the next thing is to pass this config and its dependencies to the Pre-Process utility.

The Namespace to access this utility :&#x20;

```
Digit.Utils.preProcessMDMSConfig(t, MDMSObject, dependencyObject);
```

The dependency Object contains multiple actions which the pre-process function runs for us.

1. Translate - This targets the JSON path and does translation for the passed data.
2. updateDependent - This targets the JSON path and update the dependencies.
3. convertStringToRegex -  This targets the JSON path and converts the String RegEx to RegExp based Regex.

Below is the sample example -&#x20;

```jsx
const config = useMemo(
     () => Digit.Utils.preProcessMDMSConfig(t, createProjectConfig, {
       updateDependent : [
         {
           key : 'withSubProject_project_subScheme',
           value : [withSubProjectSubSchemeOptions]
         },
         {
           key : 'noSubProject_subScheme',
           value : [noSubProjectSubSchemeOptions]
         },
         {
           key : 'noSubProject_subTypeOfProject',
           value : [subTypeOfProjectOptions]
         },
         {
           key : 'noSubProject_ulb',
           value : [ULBOptions]
         },
         {
           key : 'noSubProject_ward',
           value : [wardsAndLocalities?.wards]
         },
         {
           key : 'noSubProject_locality',
           value : [filteredLocalities]
         },
         {
           key : "citizenInfoLabel",
           value : [showInfoLabel ? 'project-banner' : 'project-banner display-none']
         },
         {
           key : "noSubProject_endDate",
           value : [!isEndDateValid ? (() => isEndDateValid) : (()=>{})]
         },
         {
           key : "basicDetails_dateOfProposal",
           value : [new Date().toISOString().split("T")[0]]
         },
         {
           key : "basicDetails_projectID",
           value : [!isModify ? "none" : "flex"]
         }
       ]
     }),
     [withSubProjectSubSchemeOptions, noSubProjectSubSchemeOptions,
      subTypeOfProjectOptions, ULBOptions, wardsAndLocalities, filteredLocalities, showInfoLabel, isEndDateValid]);
```

&#x20;  &#x20;

In the example above, we are using the action “updatedependent” from pre-process utility.

* “Key” targets the input key name. This will help preprocess to target the right input field.
* “Value” - Every input in the confg has a json path set, where each JSON path target a dependent object. As we saw earlier, we were passing the JSON in order in an array. In the same way, we need to pass the respective dependent values in order, so as to keep the right target.

Note: Please make sure you are optimizing this pre-process call. Here, to optimize, we are only calling this when there is a change in the dependent values. Our dependent values are component states, so whenever the state changes, the component will re-render and the pre-process will run and return us a new config. Since there are chances of over iterations, we are using useMemo to cache the result.

A similar utility is also developed for InboxSearchComposer. Please refer to this document for both.

\
