# Utility - Pre-Process MDMS Configuration

## Overview

This utility is designed to transform the MDMS configuration into FormComposer and InboxFormComposer configurations. Typically, every UI configuration relies on certain parameters. These parameters might include dropdown dependencies or custom classes determined at runtime based on specific logic. However, since the configuration is in JSON format stored within MDMS, direct usage of variables is not feasible. To address this requirement, we've developed a utility capable of converting this JSON into a parameter-based JSON structure.

## Steps

This utility serves as an engine that accepts MDMS configurations along with dependent parameters. It then processes this data to generate a parameter-enabled configuration. This resultant configuration can be utilized by FormComposer and InboxFormComposer to render the UI elements accordingly.

Below is the method used to configure the MDMS -&#x20;

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

1. Pass the JSON path of the dependent key that requires runtime updates. In the example above, the target is on “populators.options”.&#x20;
2. Update the options at runtime based on certain logic.

{% hint style="info" %}
**Note :**

1. Make sure to pass the JSON path in an array.
2. The order in which these JSON path are passed is important. Later on, this order will be used to target the respective dependent object.
{% endhint %}

3. Once the configuration is complete, this will be added to MDMS. So, the next thing is to pass this config and its dependencies to the Pre-Process utility. The Namespace to access this utility :&#x20;

```
Digit.Utils.preProcessMDMSConfig(t, MDMSObject, dependencyObject);
```

The dependency Object contains multiple actions which the pre-process function runs for us.

1. Translate - This targets the JSON path and does translation for the passed data.
2. updateDependent - This targets the JSON path and update the dependencies.
3. convertStringToRegex -  This targets the JSON path and converts the String RegEx to RegExp based Regex.

Refer to the sample example below -&#x20;

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

In the example above, we are using the action “updatedependent” from pre-process utility.

* “Key” targets the input key name. This will help preprocess to target the right input field.
* “Value” - Each input within the configuration is associated with a JSON path, with each path targeting a dependent object. As previously demonstrated, we passed the JSON in a specific order within an array. Similarly, we must pass the corresponding dependent values in the same order to ensure alignment with the correct targets.

{% hint style="info" %}
**Note:** Ensure that the preprocessing call is optimized for performance. It should only be invoked when there is a change in the dependent values. As our dependent values are component states, the preprocessing should occur whenever the state changes, triggering a re-render of the component. To mitigate potential over-iterations, we employ useMemo to cache the result, ensuring efficient processing and minimizing unnecessary recalculations.
{% endhint %}

A similar utility is also developed for InboxSearchComposer. Refer to this same document for both utilities.
