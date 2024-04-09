# Dropdown

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

We can show icons beside each option, for that we need to send the showIcon prop as true and also send the icons as a string along with the options.

Usually, the dropdown will be searchable but can be configured using the isSearchable prop.

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

For the type dropdown, and variant “nesteddropdown” , options can be sent like the above config.

Icons are not mandatory, but if required can be sent like this.

While searching for any option, the results will be based on the main Category names.

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

For the type dropdown, and variant “treedropdown”, options can be sent like the above config.

For now, treedropdown does not support icons.

When the user clicks on any of the parent options, then the child options will be shown. If the user clicks on the final child option that will be selected.

Only the final child options are selectable options in the tree dropdown.

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

For the type dropdown, and variant “nestedtextdropdown” , options can be sent like the above config.

This variant can be used when you want to send a description for each option.

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

For the type dropdown, and variant “profiledropdown”, options can be sent like the above config.

Any image can be sent as a profileIcon as shown in the config.

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

For the type multiselect dropdown, the options can be sent like this.

If icons are not needed one can ignore them. Else showIcon should be sent as true.

isDropdownWithChip should be sent as true to show chips after options are selected.

The label for clearing all chips can be configured using clearLabel.

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

In Tree multiselect dropdown, both parent and child options can be selected.

Selecting the child option does not select the parent option.

If only some of the child options are selected then the parent option will be in an intermediate state.

If any parent option is selected, that makes all the child options to get selected.

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

