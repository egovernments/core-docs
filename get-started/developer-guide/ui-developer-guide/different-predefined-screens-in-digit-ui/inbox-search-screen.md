---
description: >-
  Approach to render Inbox and Search screen content based on config passed via
  MDMS data.
---

# Inbox/Search Screen

## **Overview**

The inbox service is an event-based service designed to:

* Fetch pre-aggregated data of municipal services and workflows.
* Perform complex search operations.
* Return applications and workflow data in a paginated manner.
* Provide the total count of entries matching the search criteria.

This page outlines the following:

* Rendering the Inbox or Search screen based on configurations.
* Dynamically calling APIs using details provided in configurations.

## Common Components Used

#### InboxSearchComposer

InboxSearchComposer is a container component for the inbox and search screens. It consists of four child components, which can be rendered conditionally.                                                                                                    &#x20;

<table><thead><tr><th width="260">Prop Name</th><th>Description</th><th data-hidden></th></tr></thead><tbody><tr><td>configs</td><td>Config fetched from MDMS data</td><td></td></tr></tbody></table>

#### InboxSearchLinks

The InboxSearchLinks component is used to render titles and links in the inbox.

<table><thead><tr><th width="213">Prop Name</th><th>Description</th><th data-hidden></th></tr></thead><tbody><tr><td>headerText</td><td>Config fetched from MDMS data</td><td></td></tr><tr><td>links</td><td>Links to navigate to other screens</td><td></td></tr><tr><td>customClass</td><td>Class to update styling</td><td></td></tr><tr><td>logoIcon</td><td>Icon name and class to render in component</td><td></td></tr></tbody></table>

#### SearchComponent

The SearchComponent is used to render search or filter forms. It includes 'clear' and 'search' buttons for user interaction.

<table><thead><tr><th width="209">Prop Name</th><th>Description</th><th data-hidden></th></tr></thead><tbody><tr><td>uiConfig</td><td>Config to render search/filter form</td><td></td></tr><tr><td>header</td><td>Title of form</td><td></td></tr><tr><td>screenType</td><td>Type of parent screen, can be either ‘inbox’ or ‘search’</td><td></td></tr><tr><td>fullConfig</td><td>Entire config of screen which also includes API details </td><td></td></tr></tbody></table>

#### Results table

The Results table component is used to render a table with searched results.

<table><thead><tr><th width="207">Prop Name</th><th>Description</th><th data-hidden></th></tr></thead><tbody><tr><td>config</td><td>Config to render table</td><td></td></tr><tr><td>data</td><td>Search results need to be populated in table</td><td></td></tr><tr><td>isLoading</td><td>Flag to pass to handle loading state</td><td></td></tr><tr><td>isFetching</td><td>Flag to pass to handle loading state</td><td></td></tr><tr><td>fullConfig</td><td>Entire config of screen which also includes API details </td><td></td></tr></tbody></table>

#### RenderFormFields

The RenderFormFields component is used to render form fields specified in the 'fields' parameter of the configuration.

<table><thead><tr><th width="273">Prop Name</th><th>Description</th><th data-hidden></th></tr></thead><tbody><tr><td>fields</td><td>Config to render all form fields</td><td></td></tr><tr><td>control, formData, errors, register, setValue, getValues, setError, clearErrors</td><td>Props to handle all form actions like collectibe data, setting errors, clearing errors etc.</td><td></td></tr><tr><td>apiDetails</td><td>Includes all API details required to fetch data</td><td></td></tr></tbody></table>

### **Hooks Used**

To fetch inbox details, the `useCustomAPIHook` is utilized. This hook takes all necessary API details such as URL, query parameters, body, and config from the configuration (defined in MDMS).                                                                       &#x20;

{% embed url="https://github.com/egovernments/DIGIT-Works/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/libraries/src/hooks/useCustomAPIHook.js" %}

### Sample MDMS Data For Inbox&#x20;

{% embed url="https://github.com/egovernments/works-mdms-data/blob/DEV/data/pb/commonUiConfig/projectInboxConfig.json" %}

### Sample MDMS Data For Search

{% embed url="https://github.com/egovernments/works-mdms-data/blob/DEV/data/pb/commonUiConfig/SearchProjectConfig.json" %}

## Configure Screens - Steps

1. Create config based on the sections to be displayed on the screen. The basic structure for the Inbox and Search screens is given below.&#x20;

<figure><img src="../../../../.gitbook/assets/image (154).png" alt=""><figcaption><p>base search config</p></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (29).png" alt=""><figcaption><p>Base Inbox config</p></figcaption></figure>

2. Based on the flag given for each section its visibility is controlled. If the ‘show’ flag is true, then the section is visible, else it is hidden.&#x20;
3.  Add API details in the top section, this API will be called via _useCustomAPIHook_ and return the data. This consists of the below details.&#x20;

    <figure><img src="../../../../.gitbook/assets/image (55).png" alt=""><figcaption><p>Api details section</p></figcaption></figure>
4.  Add search form config which can be used in both inbox/search screen. It consists of UIconfig containing label info, styling info, default form values, and fields which need to be rendered in the form. Refer below&#x20;

    <figure><img src="../../../../.gitbook/assets/image (100).png" alt=""><figcaption><p>search </p></figcaption></figure>
5.  Add Links config consists of link info, logo to be shown and title. Refer below&#x20;

    <figure><img src="../../../../.gitbook/assets/image (137).png" alt=""><figcaption><p>Links</p></figcaption></figure>
6.  Add Filter form config which is similar to the search form. Refer below&#x20;

    <figure><img src="../../../../.gitbook/assets/image (30).png" alt=""><figcaption><p>Filter section</p></figcaption></figure>
7.  Add Table (Search result) config consists of labels, column data and related jsonpaths to access the data passed. Refer below&#x20;

    <figure><img src="../../../../.gitbook/assets/image (281).png" alt=""><figcaption><p>Results Table</p></figcaption></figure>
8.  To add any customisations on query params, request body, table columns or to add any custom validations in forms, related code can be added in the _UICustomisations_ file as below&#x20;

    <figure><img src="../../../../.gitbook/assets/image (27).png" alt=""><figcaption><p>Ui customisations for Search project screen</p></figcaption></figure>
9.  Once the above config is defined, created an index file/ Component in the pages folder. Fetch the config from MDMS and pass it to the _inboxSearchComposer_ component as below&#x20;

    <figure><img src="../../../../.gitbook/assets/image (271).png" alt=""><figcaption><p>Sample code for project search page</p></figcaption></figure>

## Limitations&#x20;

* This approach is followed only in Inbox and Search screens currently.
* Only one API can be called dynamically based on given configurations.

### Usage

To use the latest Inbox search composer it has to be imported from the React components or Utilities

React components

package

{% embed url="https://www.npmjs.com/package/@egovernments/digit-ui-react-components/v/1.5.25" %}

Utilities:

package

{% embed url="https://www.npmjs.com/package/@egovernments/digit-ui-module-utilities/v/0.0.6" %}

```jsx
 import { InboxSearchComposer } from "@egovernments/digit-ui-module-utilities";
or 
 import { InboxSearchComposer } from "@egovernments/digit-ui-module-utilities";


    <React.Fragment>
      <Header className="works-header-search">{t(updatedConfig?.label)}</Header>
      <div className="inbox-search-wrapper">
        <InboxSearchComposer configs={updatedConfig}></InboxSearchComposer>
      </div>
    </React.Fragment>
```
