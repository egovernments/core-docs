# Digit UI Core Flutter Components

Digit UI - Core Flutter Components

### Introduction: <a href="#jehqun33pi6v" id="jehqun33pi6v"></a>

Digit UI Components is a collection of common Flutter widgets designed to simplify UI development. These components offer easy-to-use and customizable features to enhance UI design and streamline the development process.

### Getting Started: <a href="#id-1o9lgnrk0gne" id="id-1o9lgnrk0gne"></a>

Add this to your pubspec.yaml file:

| <p>dependencies:<br>digit_ui_components: 0.0.1</p> |
| -------------------------------------------------- |

Then run:

| flutter pub get |
| --------------- |

Import the package in your Dart code:

| import 'package:digit\_ui\_components/digit\_components.dart'; |
| -------------------------------------------------------------- |

### List of Components: <a href="#tbotvks0v6wb" id="tbotvks0v6wb"></a>

| **ATOM**    | **VARIANTS**                                                                                                 | **STATES**                                                                                                                                                                       |
| ----------- | ------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Input Field | <p>Text</p><p>Date</p><p>Time</p><p>Geolocation</p><p>Numeric</p><p>Password</p><p>Search</p><p>TextArea</p> | <p>Default</p><p>Filled</p><p>Disabled</p><p>NonEditable</p><p>Focus</p><p>Error</p><p>Label</p><p>Character Count</p><p>Inner Label</p><p>Info</p><p>Help Text/ Description</p> |
| Radio       | Radio Selection                                                                                              | <p>Default</p><p>Disabled</p><p>Selected</p><p>PreSelected</p>                                                                                                                   |
| Toggle      | Toggle                                                                                                       | <p>Default</p><p>Disabled</p><p>Selected</p><p>PreSelected</p>                                                                                                                   |
| Button      | <p>Primary</p><p>Secondary</p><p>Teritiary</p><p>Link</p>                                                    | <p>Active</p><p>Disabled</p><p>Label</p><p>Interactions</p>                                                                                                                      |
| Dropdown    | <p>Single Select</p><p>MultiSelect</p><p>Subtype:</p><p>Default</p><p>Nested</p><p>Tree</p>                  | <p>Default</p><p>Disabled</p><p>Selected</p><p>Interactions</p>                                                                                                                  |
| Checkbox    | <p>Default</p><p>Checked</p>                                                                                 | <p>Active</p><p>Disabled</p><p>Label</p><p>Interactions</p>                                                                                                                      |
| Toast       | <p>Success</p><p>Warning</p><p>Failure</p>                                                                   |                                                                                                                                                                                  |
| Info Card   | <p>Default</p><p>Success</p><p>Warning</p><p>Error</p>                                                       |                                                                                                                                                                                  |

### Button: <a href="#id-5tghcdc543uz" id="id-5tghcdc543uz"></a>

Digit UI Components provides a variety of buttons with optional suffix and prefix icons, contributing to a cohesive and visually appealing UI.

**Button Type:**

* Primary: Represents the primary action. It features a prominent color, and its appearance can change on hover or click.
* Secondary: Offers a secondary action. It has a different color scheme than the primary button.
* Tertiary: Provides a tertiary action with a distinct visual style.
* Link: Resembles a hyperlink, suitable for navigation or linking to other parts of the application. It typically includes an underline.

**Hover and Disabled State**

**The DigitButton widget handles hover effects and a disabled state. When the button is hovered over, it can exhibit visual changes depending on its type. The disabled state prevents interaction and adjusts the button's appearance accordingly.**

**Icon Placement**

**The widget supports the placement of icons both before and after the label text. This allows for flexibility in button design.**

**Properties:**

It contains following **required** Parameters:

| Name Description |
| ---------------- |

| label(string) text displayed on the button |
| ------------------------------------------ |

| onPressed(voidCallBack A callback function, when button is pressed |
| ------------------------------------------------------------------ |

| type specify the type of button(primary or secondary) |
| ----------------------------------------------------- |

These are some optional parameters:

| PrefixIcon Icon to displayed before the label text |
| -------------------------------------------------- |

| SuffixIcon Icon to displayed after the label text |
| ------------------------------------------------- |

| isDisabled indicates where the button is in disabled state |
| ---------------------------------------------------------- |

### Primary Button: <a href="#id-9cct4ogihm4j" id="id-9cct4ogihm4j"></a>

To use primary button add this lines of code:

| <p>Button(<br>label: 'Primary Button',<br>onPressed: () {},<br>type: ButtonType.primary,<br>);</p> |
| -------------------------------------------------------------------------------------------------- |

With suffix Icon:

| <p>Button(<br>suffixIcon: Icons.add,<br>label: 'Primary Button',<br>onPressed: () {},<br>type: ButtonType.primary,<br>);</p> |
| ---------------------------------------------------------------------------------------------------------------------------- |

With prefix Icon:

| <p>Button(<br>prefixIcon: Icons.add,<br>label: 'Primary Button',<br>onPressed: () {},<br>type: ButtonType.primary,<br>);</p> |
| ---------------------------------------------------------------------------------------------------------------------------- |

### Secondary Button: <a href="#t80p74rmzb20" id="t80p74rmzb20"></a>

To use secondary button add this lines of code:

| <p>Button(<br>label: 'secondary Button',<br>onPressed: () {},<br>type: ButtonType.secondary,<br>);</p> |
| ------------------------------------------------------------------------------------------------------ |

Prefix and Suffix icons can be added in the secondary button same as the primary button.

### Tertiary Button: <a href="#j0zgnhqlc248" id="j0zgnhqlc248"></a>

To use tertiary button add this lines of code:

| <p>Button(<br>label: 'tertiary Button',<br>onPressed: () {},<br>type: ButtonType.tertiary,<br>);</p> |
| ---------------------------------------------------------------------------------------------------- |

### Link: <a href="#q13cttcv5ilz" id="q13cttcv5ilz"></a>

To use link, add this lines of code:

| <p>Button(<br>label: 'link',<br>onPressed: () {},<br>type: ButtonType.link,<br>);</p> |
| ------------------------------------------------------------------------------------- |

### Checkbox: <a href="#id-3j3prldnnu6l" id="id-3j3prldnnu6l"></a>

This widget is a versatile and customizable checkbox component. It provides a checkbox with an associated label and allows users to toggle between checked and unchecked states. This widget supports various customization options, including the ability to customize the checkbox icon color, label, padding, and disabled state.

The widget provides a hover state, visually indicating when the user hovers over the checkbox. This can be useful for enhancing the user experience.

**Properties:**

This widget has following **required** parameters:

| Name Description |
| ---------------- |

| label(string) label associated with checkbox |
| -------------------------------------------- |

| onChange(boolCallBack) callback function when the checkbox value changes |
| ------------------------------------------------------------------------ |

These are some option parameters:

| value(default: false) current state of checkbox |
| ----------------------------------------------- |

| disabled indicates whether checkbox is disabled |
| ----------------------------------------------- |

| iconColor checkbox color can be customized using this |
| ----------------------------------------------------- |

| Padding padding around checkbox widget |
| -------------------------------------- |

**Usages:**

Add the following lines of code:

| <p>DigitCheckbox(<br>label: "Label for checkbox",<br>onChanged: (value) {},<br>),</p> |
| ------------------------------------------------------------------------------------- |

### Dropdown: <a href="#jpzxsah6ohgr" id="jpzxsah6ohgr"></a>

Digit UI Components offers various dropdown menus, including single-select, multi-select, and tree-select options.

### Single Select Dropdown: <a href="#dx8hmybsdzva" id="dx8hmybsdzva"></a>

The Single Select Dropdown in Digit UI Components provides a dropdown menu for users to make a single selection. It supports various features such as item filtering, selection handling. This intuitive component supports options with additional features such as images, icons, and descriptions, complemented by hover and mouse-down effects.

**SubTypes:**

* Default Dropdown
* Nested Dropdown
* Tree Dropdown

**Properties:**

These are some required parameters:

| Name Description |
| ---------------- |

| textEditingController controller for managing the text |
| ------------------------------------------------------ |

| onChange a callback when a new option is selected |
| ------------------------------------------------- |

| items A list of DropdownItem representing the options |
| ----------------------------------------------------- |

These are some additional customization parameters:

| suffixIcon modify the suffixIcon to open dropdown |
| ------------------------------------------------- |

| <p>dropdownType dropdown can be nested dropdown( type is mandatory in</p><p>dropdown item list)</p> |
| --------------------------------------------------------------------------------------------------- |

| <p>emptyItemText Text to display when empty options are send or no match</p><p>is found during searching</p> |
| ------------------------------------------------------------------------------------------------------------ |

| isSearchable flag indicating if dropdown should support filtering option |
| ------------------------------------------------------------------------ |

| selectedOption the default selected option |
| ------------------------------------------ |

| isDisabled flag indicating where dropdown is disabled(default: false) |
| --------------------------------------------------------------------- |

**Dropdown Item:**

Inside the dropdown item, we can pass additional parameters to include inside the dropdown like description, image.

There are the customization available inside dropdown item:

| code(required) unique identifier for option |
| ------------------------------------------- |

| name(required) the label or name of dropdown option |
| --------------------------------------------------- |

| description additional description for the dropdown option |
| ---------------------------------------------------------- |

| textIcon Icon to be displayed inside the dropdown option |
| -------------------------------------------------------- |

| profileImageUrl image to be displayed inside the dropdown option |
| ---------------------------------------------------------------- |

| type incase of nested dropdown type will be send |
| ------------------------------------------------ |

**TreeNode:**

Inside the tree node we can pass list of children associated with a node:

| code(required) unique identifier for that node |
| ---------------------------------------------- |

| name(required) displaying name or label for the node |
| ---------------------------------------------------- |

| children a list of tree node |
| ---------------------------- |

**Usages:**

**Default Dropdown**

| <p>DigitDropdown&#x3C;int>(</p><p>dropdownType: type.singleSelect,<br>onChange: (String value, String index) => {},<br>textEditingController: TextEditingController(),<br>items: const [<br>DropdownItem(name: 'first',code: '1',),<br>DropdownItem(name: 'second',code: '2',),<br>DropdownItem(name: 'third',code: '3',),<br>DropdownItem(name: 'fourth',code: '4',<br>),<br>],<br>);</p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

With description and profile image:

| <p>DigitDropdown&#x3C;int>(</p><p>dropdownType: type.singleSelect,<br>onChange: (String value, String index) => {},<br>textEditingController: TextEditingController(),<br>items: const [<br>DropdownItem(<br>name: 'first',<br>code: '1',<br>description: 'description for first one',<br>profileImageUrl: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSzBXNuO6PezhC18aYH_2cYtS0I7KbxoKYdwA&#x26;usqp=CAU',<br>),<br>DropdownItem(<br>name: 'second',<br>code: '2',<br>description: 'description for second one',<br>profileImageUrl: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSzBXNuO6PezhC18aYH_2cYtS0I7KbxoKYdwA&#x26;usqp=CAU',<br>),<br>DropdownItem(<br>name: 'third',<br>code: '3',<br>description: 'description for third one',<br>profileImageUrl: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSzBXNuO6PezhC18aYH_2cYtS0I7KbxoKYdwA&#x26;usqp=CAU',<br>),<br>DropdownItem(<br>name: 'fourth',<br>code: '4',<br>description: 'description for fourth one',<br>profileImageUrl: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSzBXNuO6PezhC18aYH_2cYtS0I7KbxoKYdwA&#x26;usqp=CAU',<br>),<br>],<br>);</p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

**Nested Dropdown**

| <p>DigitDropdown&#x3C;int>(</p><p>dropdownType: type.singleSelect,</p><p>dropdownSubtype: DropdownSubtype.nested,<br>onChange: (String value, String index) => {},<br>textEditingController: TextEditingController(),<br>dropdownType: DropdownType.nestedSelect,<br>items: const [<br>DropdownItem(name: 'first',code: '1',type: 'Type A',),<br>DropdownItem(name: 'second',code: '2',type: 'Type B'),<br>DropdownItem(name: 'third',code: '3',type: 'Type A',),<br>DropdownItem(name: 'fourth',code: '4',type: 'Type B'),<br>],<br>);</p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

**Tree Dropdown**

| <p>TreeSelectDropDown&#x3C;int>(</p><p>dropdownType: type.singleSelect,</p><p>dropdownSubtype: DropdownSubtype.tree,<br>onOptionSelected: (List&#x3C;TreeNode> selectedOptions) {},<br>options: [<br>TreeNode('C', 'C', [<br>TreeNode('C.C1', 'C1', []),<br>TreeNode('C.C2', 'C2', []),<br>]),<br>TreeNode('D', 'D', [<br>TreeNode('D.D1', 'D1', []),<br>TreeNode('D.D2', 'D2', []),<br>]),<br>],<br>controller: TreeSelectController(),<br>);</p> |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### MultiSelect Dropdown: <a href="#qu8jdmpofhjw" id="qu8jdmpofhjw"></a>

The Multi Select Dropdown in Digit UI Components offers a user-friendly interface for selecting multiple options simultaneously. This clean and intuitive component is equipped with built-in chips and provides responsive mouse-down and hover effects.

**SubTypes:**

* Default Dropdown
* Nested Dropdown
* Tree Dropdown

**Properties:**

These are some required parameters:

| Name Description |
| ---------------- |

| options A list of DropdownItem representing options |
| --------------------------------------------------- |

| onOptionSelected callback function when a option is selected |
| ------------------------------------------------------------ |

These are some additional parameters:

| selectionType nested Selected(type is required inside DropdownItem) |
| ------------------------------------------------------------------- |

| selectedOptions List of DropdownItem, which will be selected by default |
| ----------------------------------------------------------------------- |

| chipConfig configuration of appearance of of selected option |
| ------------------------------------------------------------ |

| suffixIcon custom suffix icon |
| ----------------------------- |

| focusNode a focus node can be passed, to control focus |
| ------------------------------------------------------ |

| isDisabled whether dropdown is enabled or disabled |
| -------------------------------------------------- |

| clearAllText Text for Clear all button in chip selection |
| -------------------------------------------------------- |

| valueMapper mapper to show selected option inside the chip |
| ---------------------------------------------------------- |

| controller MultiSelectController can be passed |
| ---------------------------------------------- |

**Usages:**

**Default Dropdown:**

| <p>MultiSelectDropDown&#x3C;int>(</p><p>dropdownType: type.multiSelect,<br>onOptionSelected: (List&#x3C;DropdownItem> selectedOptions) {},<br>options: const [<br>DropdownItem(code: '1', name: 'first'),<br>DropdownItem(code: '2', name: 'second'),<br>DropdownItem(code: '3', name: 'third'),<br>DropdownItem(code: '4', name: 'four'),<br>],<br>);</p> |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

**Nested Dropdown**

| <p>MultiSelectDropDown&#x3C;int>(</p><p>dropdownType: type.multiSelect,</p><p>dropdownSubtype: DropdownSubtype.nested,<br>onOptionSelected: (List&#x3C;DropdownItem> selectedOptions) {},<br>options: const [<br>DropdownItem(<br>code: '1', name: 'first', type: "Type A"),<br>DropdownItem(<br>code: '2', name: 'second', type: "Type A"),<br>DropdownItem(<br>code: '3', name: 'third', type: "Type A"),<br>DropdownItem(<br>code: '4', name: 'four', type: "Type B"),<br>DropdownItem(<br>code: '5', name: 'five', type: "Type B"),<br>],<br>selectionType: SelectionType.nestedMultiSelect,<br>);</p> |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

**Tree Dropdown**

| <p>TreeSelectDropDown&#x3C;int>(</p><p>dropdownType: type.multiSelect,</p><p>dropdownSubtype: DropdownSubtype.tree,<br>onOptionSelected: (List&#x3C;TreeNode> selectedOptions) {},<br>options: [<br>TreeNode('C', 'C', [<br>TreeNode('C.C1', 'C1', []),<br>TreeNode('C.C2', 'C2', []),<br>]),<br>TreeNode('D', 'D', [<br>TreeNode('D.D1', 'D1', []),<br>TreeNode('D.D2', 'D2', []),<br>]),<br>],<br>treeSelectionType: TreeSelectionType.MultiSelect,<br>controller: TreeSelectController(),<br>);</p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

### Info Card: <a href="#id-6fq4vm4i1xsy" id="id-6fq4vm4i1xsy"></a>

This widget is a versatile and customizable information card designed inside a digit ui widget. It provides a visually appealing way to display information, with options for different types of information.

The Info Card supports different types of information, each with its distinct visual style:

* Info: Default information card with a blue background and an information icon.
* Success: Represents a successful operation, featuring a green background and a check-circle icon.
* Error: Indicates an error or unsuccessful operation with a red background and an error icon.
* Warning: Represents a warning or caution, featuring a yellow background and a warning icon.

Developers can include additional widgets beneath the description for extra information or interactive elements. The inline property controls whether these widgets are displayed horizontally or vertically.

**Properties:**

Info card have following **required** parameters:

| Name Description |
| ---------------- |

| title title displayed on the top of the card |
| -------------------------------------------- |

| description detailed content associated with the card |
| ----------------------------------------------------- |

| type specify the type of information |
| ------------------------------------ |

There are some additional customisation parameters:

| icon optional icon to display on card |
| ------------------------------------- |

| additionalWidgets a list of widget to display below description |
| --------------------------------------------------------------- |

| inline determine whether additional widgets displayed inline |
| ------------------------------------------------------------ |

**Usages:**

**Info Card:**

| <p>InfoCard(<br>title: 'Info',<br>type: InfoType.info,<br>Description: 'description'<br>);</p> |
| ---------------------------------------------------------------------------------------------- |

**Success Card:**

| <p>InfoCard(<br>title: 'Success',<br>type: InfoType.success,<br>Description: 'description'<br>);</p> |
| ---------------------------------------------------------------------------------------------------- |

**Error Card:**

| <p>InfoCard(<br>title: 'Error',<br>type: InfoType.error,<br>Description: 'description'<br>);</p> |
| ------------------------------------------------------------------------------------------------ |

**Warning Card:**

| <p>InfoCard(<br>title: 'Warning',<br>type: InfoType.warning,<br>Description: 'description'<br>);</p> |
| ---------------------------------------------------------------------------------------------------- |

### Radio List: <a href="#pqxqd08ervuz" id="pqxqd08ervuz"></a>

The Radio Buttons component in Digit UI Components empowers users to make a single selection from a list of options. This intuitive interface provides a smooth user experience with hover and mouse-down effects. It is designed to handle both horizontal and vertical layouts based on the screen width.

**Properties:**

These are some **required** parameters inside the radio list:

| Name Description |
| ---------------- |

| radioButtons A list of RadioButtonModel representing the radio button |
| --------------------------------------------------------------------- |

| onChanged a callback when a radio button is selected |
| ---------------------------------------------------- |

These are additional parameters:

| <p>groupValue the current selected value in the radio group, using this</p><p>any radio button can be selected initially, default is a</p><p>empty string.</p> |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| isDisabled indicates whether radio buttons are disabled |
| ------------------------------------------------------- |

| containerPadding padding applied around each radio button |
| --------------------------------------------------------- |

**Usages:**

Add this lines of code:

| <p>RadioList(<br>onChanged: (value) {},<br>radioButtons: [<br>RadioButtonModel(code: '1',name: 'One',),<br>RadioButtonModel(code: '2', name: 'Two'),<br>RadioButtonModel(code: '3', name: 'Three'),<br>],<br>);</p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### Input Field: <a href="#onlq20oki39" id="onlq20oki39"></a>

Digit UI Components include various text input fields with optional features such as character count display, inner labels, and help text. These fields also come with built-in validation support for improved data integrity.

#### Input Field Type: <a href="#qnvyf2caw58l" id="qnvyf2caw58l"></a>

* Text Input Field: A text input field for general alphanumeric data.
* TextArea Input Field: For multi-line text input.
* Search Input Field: Designed for search queries or search-related inputs.
* Password Input Field: A secure input field for password entry.
* Numeric Input Field: This field is suitable for numeric input.
* Date Input Field: An input field designed for capturing dates.
* Time Input Field: Use this field for inputting time values.
* Location Input Field: Specifically for geographic location data, such as coordinates.

**Properties:**

These are some common props which can be send inside all the input fields:

| Name Description |
| ---------------- |

| controller(required) textEditing Controller for input field |
| ----------------------------------------------------------- |

| label label for input field |
| --------------------------- |

| readOnly determine if the input field is read only or not |
| --------------------------------------------------------- |

| isRequired determines if input field is required or not |
| ------------------------------------------------------- |

| isDisabled indicates where field is disabled or not |
| --------------------------------------------------- |

| info boolean to show tooltip |
| ---------------------------- |

| infoText customize the tooltip text |
| ----------------------------------- |

| charCount boolean to show char count |
| ------------------------------------ |

| innerLabel inner label for input field |
| -------------------------------------- |

| helpText help message to display below the text field |
| ----------------------------------------------------- |

| validations a list of validation can be passed |
| ---------------------------------------------- |

| initialValue initial value for the field |
| ---------------------------------------- |

| keyBoardType customize keyboard type |
| ------------------------------------ |

| textInputFormatter list of filterTextInputFormatter |
| --------------------------------------------------- |

| onTap a call back function when user tap on field |
| ------------------------------------------------- |

| suffixText a text which will be shown as suffix |
| ----------------------------------------------- |

| prefixText a text which will be shown as prefix |
| ----------------------------------------------- |

| suffixIcon a icon which will be shown as suffix |
| ----------------------------------------------- |

| textAreaScroll defines the scroll behavior for textArea |
| ------------------------------------------------------- |

**TextAreaScroll:**

| smart height will increase based on the input |
| --------------------------------------------- |

| vertical can be increase height by vertical drag |
| ------------------------------------------------ |

| none height and width will not change |
| ------------------------------------- |



#### Text Input Field: <a href="#bgj664e39fat" id="bgj664e39fat"></a>

**Usages:**

| <p>InputField(</p><p>Type: InputType.text,<br>label: "Text Field",<br>initialValue: 'value',<br>controller: TextEditingController(),<br>innerLabel: 'label',<br>helpText: 'help text',<br>charCount: true,<br>);</p> |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

#### Textarea Input Field: <a href="#k2l25yxz70ta" id="k2l25yxz70ta"></a>

**Usages:**

| <p>InputField(</p><p>Type: InputType.textArea,</p><p>label: "Text Area",<br>controller: TextEditingController(),<br>helpText: 'help text',<br>);</p> |
| ---------------------------------------------------------------------------------------------------------------------------------------------------- |

#### Search Input Field: <a href="#hkyh0ue0zjbr" id="hkyh0ue0zjbr"></a>

**Usages:**

| <p>InputField(</p><p>Type: InputType.search,<br>label: "Search Field",<br>controller: TextEditingController(),<br>helpText: 'help text',<br>onSuffixTap: (value){},<br>);</p> |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

#### Password Input Field: <a href="#qgfab16ff5r6" id="qgfab16ff5r6"></a>

**Usages:**

| <p>InputField(</p><p>Type: InputType.password,<br>label: "password Field",<br>controller: TextEditingController(),<br>helpText: 'help text',<br>);</p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------ |

#### Numeric Input Field: <a href="#xvn6oofi0491" id="xvn6oofi0491"></a>

**Usages:**

| <p>InputField(</p><p>Type: InputType.numeric,<br>label: "Numeric Field",<br>controller: TextEditingController(),<br>helpText: 'help text',<br>initialValue: '0',<br>step: 1,<br>);</p> |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

#### Date Input Field: <a href="#id-54pem4zce602" id="id-54pem4zce602"></a>

**Usages:**

| <p>InputField(</p><p>Type: InputType.date,<br>label: "Date Field",<br>controller: TextEditingController(),<br>helpText: 'help text',<br>);</p> |
| ---------------------------------------------------------------------------------------------------------------------------------------------- |

#### Time Input Field: <a href="#lk2257bo4yff" id="lk2257bo4yff"></a>

**Usages:**

| <p>InputField(</p><p>Type: InputType.time,<br>label: "Time Field",<br>controller: TextEditingController(),<br>helpText: 'help text',<br>);</p> |
| ---------------------------------------------------------------------------------------------------------------------------------------------- |

#### Location Input Field: <a href="#id-1d1h9mghookh" id="id-1d1h9mghookh"></a>

**Usages:**

| <p>InputField(</p><p>Type: InputType.location,<br>label: "Location Field",<br>controller: TextEditingController(),<br>helpText: 'help text',<br>);</p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------ |

### Toast: <a href="#f0awr4wc1ck1" id="f0awr4wc1ck1"></a>

The Toast widget provides a customizable toast notification for Flutter applications. It is designed to display short-lived messages, alerts, or notifications to users in a visually appealing and informative manner.

The ToastType enumeration defines different types of toasts, including:

* success: Indicates a successful operation.
* error: Indicates an error or failure.
* warning: Indicates a warning or caution.

**Properties:**

The Toast widget provides a static method show for displaying toasts. This method includes the following parameters:

| Name Description |
| ---------------- |

| context(required) the build context for the widget |
| -------------------------------------------------- |

| <p>options(required) configuration options for the toast, such as the message</p><p>and type</p> |
| ------------------------------------------------------------------------------------------------ |

| duration how long the toast message will be shown(default: 5sec) |
| ---------------------------------------------------------------- |

**Usage:**

**Success Toast:**

| <p>Toast.show(context,<br>options: DigitToastOptions(<br>"Your Success message", ToastType.success));</p> |
| --------------------------------------------------------------------------------------------------------- |

**Error Toast:**

| <p>Toast.show(context,<br>options: DigitToastOptions(<br>"Your Error message", ToastType.error));</p> |
| ----------------------------------------------------------------------------------------------------- |

**Warning Toast:**

| <p>Toast.show(context,<br>options: DigitToastOptions(<br>"Your Warning message", ToastType.warning));</p> |
| --------------------------------------------------------------------------------------------------------- |

### Toggle: <a href="#id-58gtb3rdj4ds" id="id-58gtb3rdj4ds"></a>

The Toggle Buttons component in Digit UI Components presents a list of interactive toggle buttons, providing users with the ability to select an option. Each button is equipped with callbacks for both mouse-down and hover effects, ensuring a responsive and engaging user interface.

**Properties:**

This widget has following **required** parameters:

| Name Description |
| ---------------- |

| toggleButtons A list of ToggleButtonModels that define the toggle button |
| ------------------------------------------------------------------------ |

| onChanged a callback when a toggle is selected |
| ---------------------------------------------- |

These are some additional parameters:

| <p>selectedIndex initially selected toggle(by default first toggle will be</p><p>selected)</p> |
| ---------------------------------------------------------------------------------------------- |

| contentPadding optional Padding around toggle buttons |
| ----------------------------------------------------- |

**Usages:**

Add the following lines of code:

| <p>ToggleList(<br>toggleButtons: [<br>ToggleButtonModel(<br>name: 'Toggle 1', key: 'key1', onSelected: (value) {}),<br>ToggleButtonModel(<br>name: 'Toggle 2', key: 'key2', onSelected: (value) {}),<br>ToggleButtonModel(<br>name: 'Toggle 3', key: 'key3', onSelected: (value) {}),<br>],<br>selectedIndex: 1,<br>onChanged: (selectedValues) {},<br>);</p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

