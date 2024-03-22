# Dropdown

## Overview <a href="#dx8hmybsdzva" id="dx8hmybsdzva"></a>

Digit UI Components offers various drop-down menus, including single-select, multi-select, and tree-select options.

## Single Select Drop-down <a href="#dx8hmybsdzva" id="dx8hmybsdzva"></a>

The Single Select drop-down in Digit UI Components provides a drop-down menu for users to make a single selection. It supports various features such as item filtering and selection handling. This intuitive component supports options with additional features such as images, icons, and descriptions, complemented by hover and mouse-down effects.

**Sub-Types**

* Default drop-down
* Nested drop-down
* Tree drop-down

**Properties**

Below are some **required** parameters:

```
Name                             Description
```

```
textEditingController         controller for managing the text
```

```
onChange                      a callback when a new option is selected
```

```
items                         A list of DropdownItem representing the options
```

These are some additional customisation parameters:

```
suffixIcon                    modify the suffixIcon to open dropdown
```

<pre><code>dropdownType                   dropdown can be nested dropdown( type is mandatory in
<strong>                               nested dropdown item list)
</strong></code></pre>

```
emptyItemText                 Text to display when empty options are sent or no match
                              is found during searching
```

```
isSearchable                 flag indicating if the dropdown should support filtering
                             option
```

```
selectedOption              the default selected option
```

```
isDisabled                 flag indicating where dropdown is disabled(default: false)
```

**DropdownItem**

Inside the dropdown item, we can pass additional parameters to include the drop-down like description, image and icons.

There are the customisations available inside the drop-down item:

```
code(required)                 unique identifier for option
```

```
name(required)                 the label or name of dropdown option
```

```
description                    additional description for the dropdown option
```

```
textIcon                      Icon to be displayed inside the dropdown option
```

```
textIcon                      Icon to be displayed inside the dropdown option
```

```
type                          in case of nested dropdown type will be sent
```

**TreeNode**

Inside the tree node we can pass a list of children associated with a node:

```
code(required)                 unique identifier for that node
```

```
name(required)                 displaying the name or label for the node
```

```
children                      a list of the tree node
```

**Usages**

**Default drop-down**

```
DigitDropdown<int>(
  dropdownType: type.singleSelect,
  onChange: (String value, String index) => {},
  textEditingController: TextEditingController(),
  items: const [
    DropdownItem(name: 'first',code: '1',),
    DropdownItem(name: 'second',code: '2',),
    DropdownItem(name: 'third',code: '3',),
    DropdownItem(name: 'fourth',code: '4',),
  ],
);
```

With description and profile image:

<pre><code>DigitDropdown&#x3C;int>(
  dropdownType: type.singleSelect,
  onChange: (String value, String index) => {},
  textEditingController: TextEditingController(),
  items: const [
    DropdownItem(
      name: 'first',
      code: '1',
      description: 'description for first one',
      profileImageUrl: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSzBXNuO6PezhC18aYH_2cYtS0I7KbxoKYdwA&#x26;usqp=CAU',
    ),
    DropdownItem(
      name: 'second',
      code: '2',
      description: 'description for second one',
      profileImageUrl: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSzBXNuO6PezhC18aYH_2cYtS0I7KbxoKYdwA&#x26;usqp=CAU',
    ),
    DropdownItem(
      name: 'third',
      code: '3',
      description: 'description for third one',
      profileImageUrl: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSzBXNuO6PezhC18aYH_2cYtS0I7KbxoKYdwA&#x26;usqp=CAU',
<strong>    ),
</strong>    DropdownItem(
      name: 'fourth',
      code: '4',
      description: 'description for fourth one',
      profileImageUrl: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSzBXNuO6PezhC18aYH_2cYtS0I7KbxoKYdwA&#x26;usqp=CAU',
    ),
  ],
);
</code></pre>

**Nested drop-down**

```
DigitDropdown<int>(
  dropdownType: type.singleSelect,
  dropdownSubtype: DropdownSubtype.nested,
  onChange: (String value, String index) => {},
  textEditingController: TextEditingController(),
  dropdownType: DropdownType.nestedSelect,
  items: const [
    DropdownItem(name: 'first',code: '1',type: 'Type A',),
    DropdownItem(name: 'second',code: '2',type: 'Type B'),
    DropdownItem(name: 'third',code: '3',type: 'Type A',),
    DropdownItem(name: 'fourth',code: '4',type: 'Type B'),
  ],
);
```

**Tree drop-down**

```
TreeSelectDropDown<int>(
  dropdownType: type.singleSelect,
  dropdownSubtype: DropdownSubtype.tree,
  onOptionSelected: (List<TreeNode> selectedOptions) {},
  options: [
      TreeNode('C', 'C', [
      TreeNode('C.C1', 'C1', []),
      TreeNode('C.C2', 'C2', []),
    ]),
    TreeNode('D', 'D', [
      TreeNode('D.D1', 'D1', []),
      TreeNode('D.D2', 'D2', []),
    ]),
  ],
  controller: TreeSelectController(),
);
```

### Multi Select Drop-down <a href="#qu8jdmpofhjw" id="qu8jdmpofhjw"></a>

The Multi-Select drop down in DIGIT UI components offers a user-friendly interface for selecting multiple options simultaneously. This clean and intuitive component is equipped with built-in chips and provides responsive mouse-down and hover effects.

**Sub-Types**

* Default drop-down
* Nested drop-down
* Tree drop-down

**Properties**

Below are some **required** parameters:

```
Name                             Description
```

```
options                         A list of DropdownItem representing options
```

```
onOptionSelected                callback function when an option is selected
```

These are some additional parameters:

```
selectionType                   nested Selected(type is required inside DropdownItem)
```

| selectedOptions List of DropdownItem, which will be selected by default |
| ----------------------------------------------------------------------- |

```
selectedOptions                  List of DropdownItem, which will be selected by 
                                 default
```

```
chipConfig                       configuration of appearance of selected option
```

```
suffixIcon                      custom suffix icon
```

```
focusNode                       a focus node can be passed, to control focus
```

```
isDisabled                      whether dropdown is enabled or disabled
```

```
clearAllText                    Text for Clear all button in chip selection
```

```
valueMapper                      mapper to show selected option inside the chip
```

```
controller                      MultiSelectController can be passed
```

**Usages**

**Default Drop-down**

```
MultiSelectDropDown<int>(
  dropdownType: type.multiSelect,
  onOptionSelected: (List<DropdownItem> selectedOptions) {},
  options: const [
    DropdownItem(code: '1', name: 'first'),
    DropdownItem(code: '2', name: 'second'),
    DropdownItem(code: '3', name: 'third'),
    DropdownItem(code: '4', name: 'four'),
  ],
);
```

**Nested Drop-down**

```
MultiSelectDropDown<int>(
  dropdownType: type.multiSelect,
  dropdownSubtype: DropdownSubtype.nested,
  onOptionSelected: (List<DropdownItem> selectedOptions) {},
  options: const [
    DropdownItem(
      code: '1', name: 'first', type: "Type A"),
    DropdownItem(
      code: '2', name: 'second', type: "Type A"),
    DropdownItem(
      code: '3', name: 'third', type: "Type A"),
    DropdownItem(
      code: '4', name: 'four', type: "Type B"),
    DropdownItem(
      code: '5', name: 'five', type: "Type B"),
  ],
  selectionType: SelectionType.nestedMultiSelect,
);
```

**Tree Drop-down**

```
TreeSelectDropDown<int>(
  dropdownType: type.multiSelect,
  dropdownSubtype: DropdownSubtype.tree,
  onOptionSelected: (List<TreeNode> selectedOptions) {},
  options: [
    TreeNode('C', 'C', [
      TreeNode('C.C1', 'C1', []),
      TreeNode('C.C2', 'C2', []),
    ]),
    TreeNode('D', 'D', [
      TreeNode('D.D1', 'D1', []),
      TreeNode('D.D2', 'D2', []),
    ]),
  ],
  controller: TreeSelectController(),
);
```
