---
description: >-
  Migration guide to aid users in shifting from the "react-components" package
  to the "ui-components" package
---

# DIGIT UI Core React Components

Topics covered:

* [Overview](digit-ui-core-react-components.md#xoaiwtanhl6r)
* [Components List](digit-ui-core-react-components.md#xoaiwtanhl6r-1)
* [DIGIT UI Components : Variants & Features](digit-ui-core-react-components.md#xoaiwtanhl6r-2)
* [Component Mapping](digit-ui-core-react-components.md#jzh2thqrkpa1)
* [Install](digit-ui-core-react-components.md#jzh2thqrkpa1)
* [Apply](digit-ui-core-react-components.md#obzg60wefrmr)
* [References & Resources For Migration](digit-ui-core-react-components.md#p26wo0qmf5u3)
* [Old Components, Core and Libraries Versions](digit-ui-core-react-components.md#a49vgx5zo9hx)
* [CSS Versions](digit-ui-core-react-components.md#a49vgx5zo9hx-1)
* [Conclusion](digit-ui-core-react-components.md#a49vgx5zo9hx)

## **Overview** <a href="#xoaiwtanhl6r" id="xoaiwtanhl6r"></a>

This document details the essential modifications needed in the modules for smooth integration of components from the "ui-components" package.&#x20;

In the ui-components package, several enhancements have been implemented to improve code clarity and address issues related to pixel inconsistencies,responsiveness,duplicate components in the library,difference between figma and the developed UI, writing custom code over existing code, localization issues etc. Previously, there were challenges associated with pixel-based sizing, leading to inconsistencies across different devices and screen resolutions. To mitigate this, the codebase has been updated to utilize rems as the primary unit of measurement. This transition to rems offers several advantages over pixels, including improved scalability and responsiveness across various viewport sizes.

Adopting rems ensures the components' styling is more consistent and adaptable, providing a seamless user experience across different platforms and devices.

Furthermore, Most of the components offer different variants. Adding variants for these components makes them more flexible, serving a wider range of purposes and meeting different design needs effectively.

## **Components List** <a href="#xoaiwtanhl6r" id="xoaiwtanhl6r"></a>

These are the components present in the ui-components package.

| Groups              | Components                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Foundations**     | <p>Animations<br>Typography<br>Iconography<br>Colors<br>Spacers</p>                                                                                                                                                                                                                                                                                                                                                                                        |
| **Atoms**           | <p>Accordion<br>ActionButton<br>AlertCard<br>Backlink <br>BreadCrumb<br>Button<br>CheckBox<br>Chip<br>Divider<br>Dropdown<br>ErrorMessage<br>FileUpload<br>InfoButton<br>LabelFieldPair<br>Loader<br>Menu<br>MultiSelectDropdown<br>OTPInput<br>Panels<br>RadioButtons<br>SelectionTag<br>Stepper<br>StringManipulator<br>SummaryCardFieldPair<br>Switch<br>Tab<br>Tag<br>TextArea<br>TextBlock<br>TextInput<br>Timeline<br>Toast<br>Toggle<br>Tooltip</p> |
| **Molecules**       | <p>AccordionList<br>BottomSheet<br>ButtonGroup<br>Card<br>FilterCard<br>FormCard<br>Footer<br>Hamburger<br>LandingPageCard<br>MenuCard<br>MetricCard<br>PanelCard<br>PopUp<br>ResultsDataTable<br>SideNav<br>SidePanel<br>SummaryCard<br>TableMolecule<br>TimelineMolecule<br>TooltipWrapper</p>                                                                                                                                                           |
| **Molecule Groups** | <p>LandingPageWrapper<br>MenuCardWrapper</p>                                                                                                                                                                                                                                                                                                                                                                                                               |
| **Organisms**       | <p>FormComposerV2<br>InboxSearchComposer</p>                                                                                                                                                                                                                                                                                                                                                                                                               |

## **DIGIT UI Components : Variants & Features** <a href="#xoaiwtanhl6r" id="xoaiwtanhl6r"></a>

The table below lists the components available in the new component library along with their supported variants, states, and additional features. This serves as a reference for understanding the capabilities of each component when integrating them.

<table><thead><tr><th width="199">Component</th><th width="165">Variants</th><th>States and Features</th></tr></thead><tbody><tr><td><strong>Animations</strong></td><td>Success<br>Error<br>Warning<br>Warning2<br>LoaderPrimary<br>LoaderPrimary2<br>LoaderWhite</td><td></td></tr><tr><td><strong>Typography</strong></td><td>Body<br>Button<br>Caption<br>Heading<br><br>Label<br>Link</td><td>Body L, Body S, Body XS<br>Button L, Button M, Button S<br>Caption L, Caption M, Caption S<br>Heading XL, Heading L, Heading M,Heading S,Heading XS<br>Label<br>Link L, LInk S, Link XS</td></tr><tr><td><strong>Colors</strong></td><td>Primary<br><br><br>Text<br><br><br>Alert<br><br><br><br><br><br><br><br><br><br>Generic<br><br><br><br><br>Paper</td><td>digitv2.lightTheme.primary-1 (#C84C0E)<br>digitv2.lightTheme.primary-2 ( #0B4B66)<br>digitv2.lightTheme.primary-bg (#FBEEE8)<br><br>digitv2.lightTheme.text-primary (#363636)<br>digitv2.lightTheme.text-secondary (#787878)<br>digitv2.lightTheme.text-disabled (#C5C5C5)<br><br>digitv2.lightTheme.alert-error (#B91900)<br>digitv2.lightTheme.alert-errorbg (#FFF5F4)<br>digitv2.lightTheme.alert-success (#00703C)<br>digitv2.lightTheme.alert-successbg (#F1FFF8)<br>digitv2.lightTheme.alert-info (#0057BD)<br>digitv2.lightTheme.alert-infobg (#DEEFFF)<br>digitv2.lightTheme.alert-warning (#9E5F00)<br>digitv2.lightTheme.alert-warning-bg (#FFF9F0)<br><br>digitv2.lightTheme.generic-background (#EEEEEE)<br>digitv2.lightTheme.generic-divider (#D6D5D4)<br>digitv2.lightTheme.generic-inputborder (#505A5F)<br><br>digitv2.lightTheme.paper-primary (#FFFFFF)<br>digitv2.lightTheme.paper-secondary (#FAFAFA)</td></tr><tr><td><strong>Spacers</strong></td><td>Spacer1<br>Spacer2<br>Spacer3<br>Spacer4<br>Spacer5<br>Spacer6<br>Spacer7<br>Spacer8<br>Spacer9<br>Spacer10<br>Spacer11<br>Spacer12</td><td>digitv2.spacers.spacer1<br>digitv2.spacers.spacer2<br>digitv2.spacers.spacer3<br>digitv2.spacers.spacer4<br>digitv2.spacers.spacer5<br>digitv2.spacers.spacer6<br>digitv2.spacers.spacer7<br>digitv2.spacers.spacer8<br>digitv2.spacers.spacer9<br>digitv2.spacers.spacer10<br>digitv2.spacers.spacer11<br>digitv2.spacers.spacer12</td></tr><tr><td><strong>Accordion</strong></td><td>Basic<br>Nested Accordion</td><td>Basic<br>With Stroke<br>With Divider<br>With Stroke and Divider<br>With Icon<br>With Number</td></tr><tr><td><strong>AlertCard</strong></td><td>Info<br>Success<br>Warning<br>Error</td><td>With Actions<br>Widgets Alignment</td></tr><tr><td><strong>Action Button</strong></td><td>Primary<br>Secondary<br>Teritiary<br>Link</td><td>State : Default / Disabled<br>ActionButton : Dropdown / Dropup<br>searchable : True / False</td></tr><tr><td><strong>BackLink</strong></td><td>BackLink1<br>BackLink2<br>BackLInk3</td><td>Basic<br>Disabled</td></tr><tr><td><strong>BreadCrumb</strong></td><td>Basic<br>Collapsed</td><td>With Icons<br>With Custom Seperators</td></tr><tr><td><strong>Button</strong></td><td>Primary<br>Secondary<br>Teritiay<br>Link</td><td>State - Default / Disabled<br>Size - Large, Medium, Small<br>With Icon<br>Icon Position - Prefix / Suffix</td></tr><tr><td><strong>CheckBox</strong></td><td>Unchecked<br>Intermediate<br>Checked</td><td>Label Alignment - Left / Right<br>State - Default / Disabled</td></tr><tr><td><strong>Chip</strong></td><td>Basic<br>Error</td><td>With Icon<br>With Close</td></tr><tr><td><strong>Divider</strong></td><td>Small<br>Medium<br>Large</td><td></td></tr><tr><td><strong>Dropdown</strong></td><td>Basic<br>Categorical<br>Nested Text<br>Profile<br>Profile with Nested Text<br>Tree Dropdown</td><td>State - Deafult / Disabled<br>Searchable - True / False</td></tr><tr><td><strong>Panels</strong></td><td>Success<br>Error</td><td></td></tr><tr><td><strong>FileUpload</strong></td><td>Uploader Field<br>Uploader Widget<br>Image Upload</td><td>SIngle / Multiple Upload<br>WIth Tag / WIth Preview</td></tr><tr><td><strong>Loader</strong></td><td>Basic<br>Page Loader<br>Overlay Loader</td><td></td></tr><tr><td><strong>Multiselect Dropdown</strong></td><td>Basic<br>Categorical<br>Nested Text<br>Tree Multiselect</td><td>State - Default / Disabled<br>Searchable - True / False<br>With Chips<br>WIth Select All<br>WIth Category Select All</td></tr><tr><td><strong>OTPInput</strong></td><td>6 Characters<br>4 Characters</td><td>With Masking <br>Label Alignement - Above / Inline</td></tr><tr><td><strong>RadioButtons</strong></td><td>Basic</td><td>State - Default / Disabled / Non Editable<br>Label ALignment - Left / Right</td></tr><tr><td><strong>Selection Tag</strong></td><td>Single Select<br>Multi Select</td><td>With Container<br></td></tr><tr><td><strong>Stepper</strong></td><td>Horizontal<br>Vertical</td><td>Vertical -  With Divider</td></tr><tr><td><strong>Switch</strong></td><td>Basic<br>With Symbol</td><td>State - Default / Disabled<br>Label Alignment - Left / Right</td></tr><tr><td><strong>Tag</strong></td><td>Basic<br>Success<br>Error<br>Warning</td><td>With Stroke<br>With Icon<br>With OnClick</td></tr><tr><td><strong>Tab</strong></td><td>Basic</td><td></td></tr><tr><td><strong>TextBlock</strong></td><td>Basic</td><td></td></tr><tr><td><strong>TextInput</strong></td><td>Simple Text<br>Text With Prefix<br>Text WIth Suffix<br>Password<br>Numeric Counter<br>Date<br>Time<br>Location<br>Search</td><td><p>Default</p><p>Filled</p><p>Disabled</p><p>Non Editable</p><p>Focus</p><p>Error</p><p>Label</p><p>Character Count</p><p>Inner Label</p><p>Info</p><p>Help Text</p></td></tr><tr><td><strong>Timeline</strong></td><td>Inprogress<br>Upcoming<br>Completed</td><td>State - Default / Failed<br>With Connector<br>Elements Alignment - vertical / inline<br></td></tr><tr><td><strong>Toast</strong></td><td>Success<br>Error<br>Warning<br>Info</td><td>With transition time</td></tr><tr><td><strong>Toggle</strong></td><td>Basic</td><td></td></tr><tr><td><strong>Tooltip</strong></td><td>Dark Theme<br>LIght Theme</td><td>With Arrow<br>Position - BottomStart / Bottom / BottomEnd / TopStart / Top / TopEnd / LeftStart / Left / LeftEnd / RightStart / Right / RightEnd<br></td></tr><tr><td><strong>TextArea</strong></td><td></td><td><p>Default</p><p>Filled</p><p>Disabled</p><p>NonEditable</p><p>Focus</p><p>Error</p><p>Label</p><p>Character Count</p><p>Inner Label</p><p>Info</p><p>Help Text<br>resizeSmart</p></td></tr><tr><td><strong>AccordionList</strong></td><td>Basic</td><td>With Divider<br>WIth Multiple Open</td></tr><tr><td><strong>PopUp</strong></td><td>Basic<br>Alert</td><td></td></tr><tr><td><strong>Card</strong></td><td>Basic<br>Form Card<br>Summary Card</td><td>Card Style - Primary / Secondary</td></tr><tr><td><strong>FormCard</strong></td><td></td><td>Columns - 1 / 2<br>Divider - True / False</td></tr><tr><td><strong>SummaryCard</strong></td><td></td><td>Layout - Horizontal / Vertical <br>Columns - 1 / 2<br>Divider - True / False</td></tr><tr><td><strong>BottomSheet</strong></td><td>Basic<br>WIth Actions</td><td></td></tr><tr><td><strong>ButtonGroup</strong></td><td>Basic</td><td>Auto Sort - True/ False<br>Size - Large / Medium / Small<br>Equal Buttons - True / False</td></tr><tr><td><strong>Header</strong></td><td>Dark <br>Light</td><td></td></tr><tr><td><strong>SidePanel</strong></td><td>Static<br><br><br><br><br>Dynamic</td><td>With  Close <br>As Sections<br>Background Active<br>Position - Left / Right <br><br>With Nudge<br>Draggable</td></tr><tr><td><strong>PanelCard</strong></td><td>Success<br>Error</td><td></td></tr><tr><td><strong>FilterCard</strong></td><td>Horizontal <br>Vertical</td><td>With Heading<br>With Close<br>As Popup</td></tr><tr><td><strong>Footer</strong></td><td>Basic<br>Flex</td><td>Alignment - Left / Right</td></tr><tr><td><strong>Hamburger</strong></td><td>Dark <br>LIght</td><td>Enable Search<br>Universal Actions<br>Profile</td></tr><tr><td><strong>LandingPageCard</strong></td><td>Basic</td><td>Icon - Default / Filled<br>Metric Alignment - Left / Centre<br>Icon Alignment - Left / Right</td></tr><tr><td><strong>MenuCard</strong></td><td>Menu1</td><td></td></tr><tr><td><strong>MetricCard</strong></td><td>Horizontal<br>Vertical<br>Mixed</td><td>Dividers - Vertical / Horizontal / Both</td></tr><tr><td><strong>SideNav</strong></td><td>Dark<br>Light</td><td>Enable Search<br>Universal Actions<br>Selection Color - Complementary / Analogous</td></tr><tr><td><strong>TableMolecule</strong></td><td>Basic</td><td></td></tr><tr><td><strong>TimelineMolecule</strong></td><td>Basic<br>Collapsable</td><td></td></tr><tr><td><strong>TooltipWrapper</strong></td><td>Basic</td><td></td></tr><tr><td><strong>LandingPageWrapper</strong></td><td>Basic</td><td></td></tr><tr><td><strong>MenuCardWrapper</strong></td><td>Basic</td><td></td></tr></tbody></table>

## Component Mapping <a href="#jzh2thqrkpa1" id="jzh2thqrkpa1"></a>

The following table lists some of the old components and their corresponding replacements in the new library.&#x20;

| react-components (old) | ui-components (new)               |
| ---------------------- | --------------------------------- |
| ActionBar              | Footer                            |
| BackButton             | BackLink                          |
| Banner                 | Panels                            |
| CitizenInfoLabel       | AlertCard                         |
| Hamburger              | HamburgerButton                   |
| Header                 | HeaderComponent                   |
| LoaderWithGap          | Loader                            |
| RemovableTag           | Chip                              |
| Table                  | Table Molecule / ResultsDataTable |
| TopBar                 | Header                            |
| UploadFile             | FileUpload                        |
| WorkFlowTimeline       | TimelineMolecule                  |

## **Install** <a href="#jzh2thqrkpa1" id="jzh2thqrkpa1"></a>

To install:

Add the dependency in the frontend/micro-ui/web/package.json

```
"@egovernments/digit-ui-components":"0.2.0"
```

## **Apply** <a href="#obzg60wefrmr" id="obzg60wefrmr"></a>

Syntax for importing any components:

```
import {TextInput, Dropdown} from "@egovernenets/digit-ui-components"
```

## **References & Resources for Migration** <a href="#p26wo0qmf5u3" id="p26wo0qmf5u3"></a>

Refer to the Sample Module Screens integrated with new ui-components library : [https://github.com/egovernments/DIGIT-Frontend/tree/sample/micro-ui/web/micro-ui-internals/packages/modules/sample/src/pages/employee/uiComponentsSample](https://github.com/egovernments/DIGIT-Frontend/tree/sample/micro-ui/web/micro-ui-internals/packages/modules/sample/src/pages/employee/uiComponentsSample)\
\
Refer to the [https://github.com/egovernments/DIGIT-UI-LIBRARIES/blob/develop/react/ui-components/CHANGELOG.md](https://github.com/egovernments/DIGIT-UI-LIBRARIES/blob/develop/react/ui-components/CHANGELOG.md) for version updates

{% embed url="https://unified-dev.digit.org/storybook/?path=/story/intro--intro" %}

## **Other Core Dependencies Versions**  <a href="#a49vgx5zo9hx" id="a49vgx5zo9hx"></a>

We have integrated this new component library with our core module module, so use the below version for latest core module with upgraded components

```
"@egovernments/digit-ui-react-components" : "1.8.19"
"@egovernments/digit-ui-libraries": "1.8.11"
"@egovernments/digit-ui-module-core": "1.8.32"
```

## **CSS Versions**  <a href="#a49vgx5zo9hx" id="a49vgx5zo9hx"></a>

```
<link rel="stylesheet" href="https://unpkg.com/@egovernments/digit-ui-css@1.8.23/dist/index.css" />
<link rel="stylesheet" href="https://unpkg.com/@egovernments/digit-ui-components-css@0.2.0/dist/index.css" />
```

## **Conclusion** <a href="#a49vgx5zo9hx" id="a49vgx5zo9hx"></a>

These are some of the modifications that need to be done in the modules to use the components from the ui-components package.
