# Input Field

## Overview

DIGIT UI components include various text input fields with optional features such as character count display, inner labels, and help text. These fields also come with built-in validation support for improved data integrity.

## Input Field Type <a href="#qnvyf2caw58l" id="qnvyf2caw58l"></a>

* Text Input Field: A text input field for general alphanumeric data.
* Text Area Input Field: For multi-line text input.
* Search Input Field: Designed for search queries or search-related inputs.
* Password Input Field: A secure input field for password entry.
* Numeric Input Field: This field is suitable for numeric input.
* Date Input Field: An input field designed for capturing dates.
* Time Input Field: Use this field for inputting time values.
* Location Input Field: Specifically for geographic location data, such as coordinates.

### **Properties**

These are some common props which can be sent inside all the input fields:

```
Name                              Description
```

```
controller(required)             textEditing Controller for input field
```

```
label                            label for input field
```

```
readOnly                        determines if the input field is read-only or not
```

```
isRequired                      determines if the input field is required or not
```

```
isDisabled                      indicates where the field is disabled or not
```

```
info                            boolean to show the tooltip
```

```
infoText                         customize the tooltip text
```

```
charCount                       boolean to show the char count
```

```
innerLabel                      inner label for input field
```

```
helpText                         help message to display below the text field
```

```
validations                     a list of validations can be passed
```

```
initialValue                     initial value for the field
```

```
keyBoardType                      customize keyboard type
```

```
textInputFormatter               list of filterTextInputFormatter
```

```
onTap                           a call-back function when the user taps on the field
```

```
suffixText                       a text which will be shown as a suffix
```

```
prefixText                      a text which will be shown as a prefix
```

```
suffixIcon                       an icon which will be shown as a suffix
```

```
textAreaScroll                 defines the scroll behaviour for textArea
```

**TextAreaScroll**

```
smart                           height will increase based on the input
```

```
vertical                        can be increased height by vertical drag
```

```
none                            height and width will not change
```

#### Text Input Field <a href="#bgj664e39fat" id="bgj664e39fat"></a>

**Usages**

```
InputField(
  Type: InputType.text,
  label: "Text Field",
  initialValue: 'value',
  controller: TextEditingController(),
  innerLabel: 'label',
  helpText: 'help text',
  charCount: true,
);
```

#### TextArea Input Field <a href="#k2l25yxz70ta" id="k2l25yxz70ta"></a>

**Usages**

```
InputField(
  Type: InputType.textArea,
  label: "Text Area",
  controller: TextEditingController(),
  helpText: 'help text',
);
```

#### Search Input Field <a href="#hkyh0ue0zjbr" id="hkyh0ue0zjbr"></a>

**Usages**

```
InputField(
  Type: InputType.search,
  label: "Search Field",
  controller: TextEditingController(),
  helpText: 'help text',
  onSuffixTap: (value){},
);
```

#### Password Input Field <a href="#qgfab16ff5r6" id="qgfab16ff5r6"></a>

**Usages**

```
InputField(
  Type: InputType.password,
  label: "password Field",
  controller: TextEditingController(),
  helpText: 'help text',
);
```

#### Numeric Input Field <a href="#xvn6oofi0491" id="xvn6oofi0491"></a>

**Usages**

```
InputField(
  Type: InputType.numeric,
  label: "Numeric Field",
  controller: TextEditingController(),
  helpText: 'help text',
  initialValue: '0',
  step: 1,
);
```

#### Date Input Field <a href="#id-54pem4zce602" id="id-54pem4zce602"></a>

**Usages**

```
InputField(
  Type: InputType.date,
  label: "Date Field",
  controller: TextEditingController(),
  helpText: 'help text',
);
```

#### Time Input Field <a href="#lk2257bo4yff" id="lk2257bo4yff"></a>

**Usages**

```
InputField(
  Type: InputType.time,
  label: "Time Field",
  controller: TextEditingController(),
  helpText: 'help text',
);
```

#### Location Input Field <a href="#id-1d1h9mghookh" id="id-1d1h9mghookh"></a>

**Usages**

```
InputField(
  Type: InputType.location,
  label: "Location Field",
  controller: TextEditingController(),
  helpText: 'help text',
);
```
