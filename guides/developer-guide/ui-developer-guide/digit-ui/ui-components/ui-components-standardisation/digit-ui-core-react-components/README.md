---
description: >-
  Migration guide to aid users in shifting from the "react-components" package
  to the "components-core" package
---

# DIGIT UI Core React Components

## **Introduction** <a href="#yy16fmgmik0e" id="yy16fmgmik0e"></a>

This document details the essential modifications needed in the modules for smooth integration of components from the "components-core" package. It offers precise guidelines on utilizing FormComposerV2 and InboxSearchComposer, along with updates made in the configs.

Topics covered:

* [Overview](./#xoaiwtanhl6r)
* [Install](./#jzh2thqrkpa1)
* [Apply](./#obzg60wefrmr)
* [Modifications to the Project Module](./#p26wo0qmf5u3)
* [Conclusion](./#a49vgx5zo9hx)

## **Overview** <a href="#xoaiwtanhl6r" id="xoaiwtanhl6r"></a>

In the components-core package, several enhancements have been implemented to improve code clarity and address issues related to pixel inconsistencies. Previously, there were challenges associated with pixel-based sizing, leading to inconsistencies across different devices and screen resolutions. To mitigate this, the codebase has been updated to utilize rems as the primary unit of measurement. This transition to rems offers several advantages over pixels, including improved scalability and responsiveness across various viewport sizes.

By adopting rems, the components' styling is now more consistent and adaptable, providing a seamless user experience across different platforms and devices.

Furthermore, the components, namely TextInput, TextArea, Radio, Button, Checkbox, Toggle, Dropdown, Multiselectdropdown, InfoCard, and Toast, now offer different variants. Adding variants for these components makes them more flexible, serving a wider range of purposes and meeting different design needs effectively.

These are some of the updates made in the components-core package.

<table><thead><tr><th width="154">Atom</th><th width="210">Variants</th><th>State</th></tr></thead><tbody><tr><td><a href="input-field.md">TextInput</a></td><td><p>Text</p><p>Date</p><p>Time</p><p>Geolocation</p><p>Numeric</p><p>Prefix</p><p>Suffix</p><p>Password</p><p>Search</p></td><td><p>Default</p><p>Filled</p><p>Disabled</p><p>NonEditable</p><p>Focus</p><p>Error</p><p>Label</p><p>Character Count</p><p>Inner Label</p><p>Info</p><p>Help Text/ Description</p></td></tr><tr><td><a href="input-field.md">TextArea</a></td><td></td><td><p>Default</p><p>Filled</p><p>Disabled</p><p>NonEditable</p><p>Focus</p><p>Error</p><p>Label</p><p>Character Count</p><p>Inner Label</p><p>Info</p><p>Help Text/ Description</p><p>resizeSmart</p></td></tr><tr><td><a href="radio.md">Radio</a></td><td>Radio Selection</td><td><p>Default</p><p>Disabled</p><p>Selected</p><p>PreSelected</p></td></tr><tr><td><a href="toggle.md">Toggle</a></td><td>Toggle</td><td><p>Default</p><p>Disabled</p><p>Selected</p><p>PreSelected</p></td></tr><tr><td><a href="button.md">Button</a></td><td><p>Primary</p><p>Secondary</p><p>Teritiary</p><p>Link</p></td><td><p>Active</p><p>Disabled</p><p>Label</p><p>Interactions</p></td></tr><tr><td><a href="dropdown.md">Dropdown</a></td><td><p>Default</p><p>Nested</p><p>Tree select</p><p>Profile</p><p>Profile with nested text</p><p>Nested Text</p></td><td><p>Default</p><p>Disabled</p><p>Selected</p><p>Interactions</p></td></tr><tr><td><a href="dropdown.md">MultiSelect Dropdown</a></td><td><p>Default</p><p>Nested</p><p>Tree Multiselect</p><p>Nested Text Multiselect</p></td><td><p>Default</p><p>Disabled</p><p>Selected</p><p>Interactions</p></td></tr><tr><td><a href="checkbox.md">Checkbox</a></td><td><p>Default</p><p>Checked</p></td><td><p>Active</p><p>Disabled</p><p>Label</p><p>Interactions</p></td></tr><tr><td><a href="toast.md">Toast</a></td><td><p>Success</p><p>Warning</p><p>Failure</p></td><td></td></tr><tr><td><a href="info-card.md">Info Card</a></td><td><p>Default</p><p>Success</p><p>Warning</p><p>Error</p></td><td></td></tr></tbody></table>

## **Install - Steps** <a href="#jzh2thqrkpa1" id="jzh2thqrkpa1"></a>

To install:

```
npm install -save @egovernments/digit-ui-components-core
```

Add the dependency in the frontend/micro-ui/web/package.json

```
"@egovernments/digit-ui-components-core":"0.0.1"
```

## **Apply** <a href="#obzg60wefrmr" id="obzg60wefrmr"></a>

Syntax for importing any components:

```
import {TextInput, Dropdown} from "@egovernenets/digit-ui-components-core"
```

Syntax for importing FormComposerV2:

```
import {FormComposerV2} from "@egovernenets/digit-ui-components-core"
```

```
<React.Fragment>
<Header >{t("CREATE_HEADER")}</Header>
<FormComposerV2
label={t("PROCEED")}
config={configs.map((config) => {
return {
...config,
body: config.body.filter((a) => !a.hideInEmployee),
};
})}
defaultValues={sessionFormData}
onFormValueChange={onFormValueChange}
onSubmit={onFormSubmit}
/>
</React.Fragment>
```

|   |
| - |

### **Modifications To The Project Module** <a href="#p26wo0qmf5u3" id="p26wo0qmf5u3"></a>

In the micro-ui/web/micro-ui-internals/packages/modules/Project/src/pages/employee/CreateProject/CreateProjectForm.js:

| **import** {FormComposerV2} **from** "@egovernenets/digit-ui-components-core" |
| ----------------------------------------------------------------------------- |

```
return (
<React.Fragment>
<Header className="works-header-create">{isModify ? t("COMMON_MODIFY_PROJECT") : t("WORKS_CREATE_PROJECT")}</Header>
{createProjectConfig && (
<FormComposerV2
label={!isModify ? "WORKS_CREATE_PROJECT" : "WORKS_MODIFY_PROJECT"}
config={config?.form?.map((config) => {
return {
...config,
body: config?.body.filter((a) => !a.hideInEmployee),
};
})}
onSubmit={handleSubmit}
submitInForm={false}
inline={false}
className="form-no-margin"
defaultValues={sessionFormData}
showWrapperContainers={false}
noBreakLine={true}
showNavs={config?.metaData?.showNavs}
showFormInNav={true}
showMultipleCardsWithoutNavs={false}
showMultipleCardsInNavs={false}
horizontalNavConfig={navTypeConfig}
currentFormCategory={currentFormCategory}
onFormValueChange={onFormValueChange}
cardClassName="mukta-header-card"
/>
)}
</React.Fragment>
);
```

In the micro-ui/web/micro-ui-internals/packages/modules/Project/package.json :

Add “@egovernments/digit-ui-components-core”:”0.0.1” in the dependencies.

And when you import any component the syntax for the import statement is:

```
import {TextInput, Dropdown} from "@egovernenets/digit-ui-components-core"
```

In the micro-ui/web/micro-ui-internals/packages/modules/Project/src/pages/employee/ProjectWMSSearch:

```
import {InboxSearchComposer} from "@egovernenets/digit-ui-components-core"
```

```
<div className ="inbox-search-wrapper">
<InboxSearchComposer configs={configs}></InboxSearchComposer>
</div>
```

### **Conclusion** <a href="#a49vgx5zo9hx" id="a49vgx5zo9hx"></a>

Verify these components in the sample module:

[Sample module Integrated with new components](https://unified-dev.digit.org/core-ui/employee/user/login)

These are some of the modifications that need to be done in the modules to use the components from the components-core package.
