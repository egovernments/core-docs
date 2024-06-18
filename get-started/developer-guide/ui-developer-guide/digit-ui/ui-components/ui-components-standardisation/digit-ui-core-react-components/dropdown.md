# Dropdown

## **Description** <a href="#id-3bsz0jtw0iwh" id="id-3bsz0jtw0iwh"></a>

A dropdown UI component is a user interface element that allows users to select one option from a list of choices. When the dropdown is clicked, it expands to reveal the list of options, and the user can click an item to select it. This component is often used in forms and navigation menus to save space and organize options efficiently.

## **Configuration** <a href="#id-3bsz0jtw0iwh" id="id-3bsz0jtw0iwh"></a>

#### **Config for Dropdown Component (using FormComposerV2)** <a href="#id-3bsz0jtw0iwh" id="id-3bsz0jtw0iwh"></a>

**Simple Dropdown**

```
{
isMandatory: false,
type: "dropdown",
key: "genders",
label: "With Icons",
disable: false,
populators: {
name: "dropdown-WIth Icons",
optionsKey: "name",
error: "",
required: true,
showIcon: true,
isSearchable:true,
options: [
{
code: "1",
name: "Option1",
icon: "Article",
},
{
code: "2",
name: "Option2",
icon: "Article",
},
{
code: "3",
name: "Option3",
icon: "Article",
},
],
}
}
```

To show the icons beside each option, set the showIcon prop to true. Send the icons as a string along with the required options. The dropdown is searchable but can be configured using the isSearchable prop.

To reset the option after selecting it, clear the option and click enter.

For more information: [StoryBook for simple dropdown](https://unified-dev.digit.org/storybook/?path=/story/atom-groups-dropdownfield--dropdown-with-icons)

**Nested Dropdown**

```
{
isMandatory: false,
type: "dropdown",
key: "genders",
label: "With Icons",
disable: false,
variant: "nesteddropdown",
populators: {
name: "nesteddropdown-With Icons",
optionsKey: "name",
error: "",
required: true,
showIcon:true,
isSearchable:true,
options: [
{
name: "Category A",
options: [
{ code: "Category A.Option A", name: "Option A", icon: "Article" },
{ code: "Category A.Option B", name: "Option B", icon: "Article" },
{ code: "Category A.Option C", name: "Option C", icon: "Article" },
],
code: "Category A",
},
{
name: "Category B",
options: [
{ code: "Category B.Option A", name: "Option A", icon: "Article" },
{ code: "Category B.Option 2", name: "Option 2", icon: "Article" },
{ code: "Category B.Option 3", name: "Option 3", icon: "Article" },
],
code: "Category B",
},
],
},
}
```

For the type dropdown with the "nesteddropdown" variant, options can be configured as shown above. Icons are optional but can be included if needed. The search results are displayed as per the main category names.

For more information: [Storybook for nesteddropdown varinat](https://unified-dev.digit.org/storybook/?path=/story/atom-groups-dropdownfield--nested-dropdown-with-icons)

**Tree Dropdown**

```
{
isMandatory: false,
type: "dropdown",
key: "genders",
label: "Default",
disable: false,
variant: "treedropdown",
populators: {
name: "treedropdown-Default",
optionsKey: "name",
error: "",
required: true,
options: [
{
name: "Category A",
options: [
{
code: "Category A.Option A",
name: "Option A",
options: [
{ code: "Category A.Option A.Option 1", name: "Option 1" },
{ code: "Category A.Option A.Option 2", name: "Option 2" },
],
},
{
code: "Category A.Option B",
name: "Option B",
options: [
{ code: "Category A.Option B.Option 1", name: "Option 1" },
{ code: "Category A.Option B.Option 2", name: "Option 2" },
],
},
],
code: "Category A",
},
{
name: "Category B",
options: [
{ code: "Category B.Option A", name: "Option A" },
{
code: "Category B.Option B",
name: "Option B",
options: [
{ code: "Category B.Option B.Option 1", name: "Option 1" },
{ code: "Category B.Option B.Option 2", name: "Option 2" },
],
},
],
code: "Category B",
},
{
name: "Category C",
options: [{ code: "Category C.Option A", name: "Option A" }],
code: "Category C",
},
],
},
}
```

Here's a simplified version of your explanation:

For the type dropdown with the "treedropdown" variant, options can be configured as shown in the configuration above. Currently, the treedropdown does not support icons. Clicking on the parent option displays the child options. The final child options are enabled for selection.

This version maintains the necessary details while being clear and concise.

For more information: [Storybook for treedropdown](https://unified-dev.digit.org/storybook/?path=/story/atom-groups-dropdownfield--tree-dropdown)

**NestedText Dropdown**

```
{
isMandatory: false,
type: "dropdown",
key: "genders",
label: "With Icon",
disable: false,
variant: "nestedtextdropdown",
populators: {
name: "nestedtextdropdown-With Icon",
optionsKey: "name",
error: "",
required: true,
showIcon:true,
options: [
{
code: "Option1",
name: "Option1",
icon: "Article",
description:"Lorem ipsum dolor sit amet, consectetur adipiscing elit,sed do eiusmod tempor ",
},
{
code: "Option2",
name: "Option2",
icon: "Article",
description:"Lorem ipsum dolor sit amet, consectetur adipiscing elit,sed do eiusmod tempor",
},
{
code: "Option3",
name: "Option3",
icon: "Article",
description:"Lorem ipsum dolor sit amet, consectetur adipiscing elit,sed do eiusmod tempor",
},
],
},
},
```

For the `type` dropdown with the variant `nestedtextdropdown`, use the above configuration details to define the options.

Use this variant when you need to describe each option.

For more information: [StoryBook for nestedtext dropdown](https://unified-dev.digit.org/storybook/?path=/story/atom-groups-dropdownfield--nested-text-drop-down-with-icon).

**Profile Dropdown**

```
{
isMandatory: false,
type: "dropdown",
key: "genders",
label: "With CustomIcon",
disable: false,
variant: "profiledropdown",
populators: {
name: "profiledropdown-With CustomIcon",
optionsKey: "name",
error: "",
required: true,
options: [
{
code: "Option1",
name: "Option1",
profileIcon:"
https://www.freeiconspng.com/uploads/am-a-19-year-old-multimedia-artist-student-from-manila-21.png
",

},
{
code: "Option2",
name: "Option2",
profileIcon:"
https://www.freeiconspng.com/uploads/am-a-19-year-old-multimedia-artist-student-from-manila-21.png
",

},
{
code: "Option3",
name: "Option3",
profileIcon:"
https://www.freeiconspng.com/uploads/am-a-19-year-old-multimedia-artist-student-from-manila-21.png
",

},
],
},
}
```

For the type dropdown with the "profiledropdown" variant, use the configuration details above to define the options.

You can set any image as a profileIcon as shown in the configuration.

For more information: [Storybook for profiledropdown](https://unified-dev.digit.org/storybook/?path=/story/atom-groups-dropdownfield--profile-dropdown-with-custom-icon)

**Profilenestedtext Dropdown**

```
{
isMandatory: false,
type: "dropdown",
key: "genders",
label: "ProfileDropdown",
disable: false,
variant: "profilenestedtext",
populators: {
name: "profiledropdown-With NestedText",
optionsKey: "name",
error: "",
required: true,
options: [
{
code: "Option1",
name: "Option1",
profileIcon:"
https://www.freeiconspng.com/uploads/am-a-19-year-old-multimedia-artist-student-from-manila-21.png
",
description:"Lorem ipsum dolor sit amet, consectetur adipiscing elit,sed do eiusmod tempor",
},
{
code: "Option2",
name: "Option2",
profileIcon:"

https://www.freeiconspng.com/uploads/am-a-19-year-old-multimedia-artist-student-from-manila-21.png
",
description:"Lorem ipsum dolor sit amet, consectetur adipiscing elit,sed do eiusmod tempor",

},
{
code: "Option3",
name: "Option3",
profileIcon:"
https://www.freeiconspng.com/uploads/am-a-19-year-old-multimedia-artist-student-from-manila-21.png
",
description:"Lorem ipsum dolor sit amet, consectetur adipiscing elit,sed do eiusmod tempor",
},
],
},
}
```

For more information: [Storybook for profilenestedtext dropdown](https://unified-dev.digit.org/storybook/?path=/story/atom-groups-dropdownfield--profile-with-nested-text-with-custom-icon)

#### **Config for MultiSelectDropdown Component (using FormComposerV2)** <a href="#id-2mnv8mqa41wp" id="id-2mnv8mqa41wp"></a>

**Simple MultiSelect Dropdown**

```
{
isMandatory: false,
key: "multiselect",
type: "multiselectdropdown",
label: "With Icons",
disable: false,
populators: {
name: "multiselectdropdown-With Icons",
optionsKey: "name",
error: "Error!",
required: false,
isDropdownWithChip: true,
showIcon:true,
clearLabel:"Clear All"
options: [
{
code: "Option1",
name: "Option1",
icon: "Article",
},
{
code: "Option2",
name: "Option2",
icon: "Article",
},
{
code: "Option3",
name: "Option3",
icon: "Article",
},
],
},
}
```

For a multi-select dropdown, set options in the format given in the above configuration.

Ignore these If icons are not needed. Else, set the showIcon to true. Set the isDropdownWithChip parameter to true to show chips once the options are selected.

Configure the clearLabel param to ensure the chips are cleared from the label.

For more information: [Storybook for multiselect dropdown](https://unified-dev.digit.org/storybook/?path=/story/atom-groups-dropdownfield--multi-select-dropdown-with-icons)

**Nested MultiSelect Dropdown**

```
{
isMandatory: false,
key: "multiselect",
type: "multiselectdropdown",
label: "With Icons",
disable: false,
variant: "nestedmultiselect",
populators: {
name: "nestedmultiselect-With Icons",
optionsKey: "name",
error: "Error!",
required: false,
isDropdownWithChip: true,
showIcon:true,
options: [
{
name: "Category A",
options: [
{ code: "Category A.Option A", name: "Option A", icon: "Article" },
{ code: "Category A.Option B", name: "Option B", icon: "Article" },
{ code: "Category A.Option C", name: "Option C", icon: "Article" },
],
code: "Category A",
},
{
name: "Category B",
options: [
{ code: "Category B.Option A", name: "Option A", icon: "Article" },
{ code: "Category B.Option 2", name: "Option 2", icon: "Article" },
{ code: "Category B.Option 3", name: "Option 3", icon: "Article" },
],
code: "Category B",
},
],
},
}
```

Multiple options can be selected for each category.

For more information: [Storybook for nested multiselect dropdown](https://unified-dev.digit.org/storybook/?path=/story/atom-groups-dropdownfield--nested-multi-select-dropdown-with-icons)

**Tree MultiSelect Dropdown**

```
{
isMandatory: false,
key: "multiselect",
type: "multiselectdropdown",
label: "Default",
disable: false,
variant: "treemultiselect",
populators: {
name: "treemultiselect-Default",
optionsKey: "name",
error: "Error!",
required: false,
isDropdownWithChip: true,
options: [
{
name: "Category A",
options: [
{
code: "Category A.Option A",
name: "Option A",
options: [
{ code: "Category A.Option A.Option 1", name: "Option 1" },
{ code: "Category A.Option A.Option 2", name: "Option 2" },
],
},
{
code: "Category A.Option B",
name: "Option B",
options: [
{ code: "Category A.Option B.Option 1", name: "Option 1" },
{ code: "Category A.Option B.Option 2", name: "Option 2" },
],
},
],
code: "Category A",
},
{
name: "Category B",
options: [
{ code: "Category B.Option A", name: "Option A" },
{
code: "Category B.Option B",
name: "Option B",
options: [
{ code: "Category B.Option B.Option 1", name: "Option 1" },
{ code: "Category B.Option B.Option 2", name: "Option 2" },
],
},
],
code: "Category B",
},
{
name: "Category C",
options: [{ code: "Category C.Option A", name: "Option A" }],
code: "Category C",
},
],
},
}
```

In a tree multiselect dropdown, you can select both parent and child options. Choosing a child option does not automatically select the parent option. When only some child options are selected, the parent option will show in an intermediate state.

Selecting any parent option will automatically select all its child options.

For more information: [Storybook for treemultiselect dropdown](https://unified-dev.digit.org/storybook/?path=/story/atom-groups-dropdownfield--tree-multiselect-dropdown)

**NestedText MultiSelect Dropdown**

```
{
isMandatory: false,
type: "multiselectdropdown",
key: "multiselect",
label: "With Icons",
disable: false,
variant: "nestedtextmultiselect",
populators: {
name: "nestedtextmultiselect-With Icon",
optionsKey: "name",
error: "Error!",
required: false,
showIcon:true,
isDropdownWithChip:true,
options: [
{
code: "Option1",
name: "Option1",
icon: "Article",
description:"Lorem ipsum dolor sit amet, consectetur adipiscing elit,sed do eiusmod tempor ",
},
{
code: "Option2",
name: "Option2",
icon: "Article",
description:"Lorem ipsum dolor sit amet, consectetur adipiscing elit,sed do eiusmod tempor",
},
{
code: "Option3",
name: "Option3",
icon: "Article",
description:"Lorem ipsum dolor sit amet, consectetur adipiscing elit,sed do eiusmod tempor",
},
],
},
},
```

For more information: [Storybook for Nestedtext Multiselect Dropdown](https://unified-dev.digit.org/storybook/?path=/story/atom-groups-dropdownfield--nested-text-multi-select-with-icons)
