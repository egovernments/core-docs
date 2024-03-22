# Checkbox

This widget is a versatile and customizable checkbox component. It provides a checkbox with an associated label and allows users to toggle between checked and unchecked states. This widget supports various customisation options, including the ability to customise the checkbox icon colour, label, padding, and disabled state.

The widget provides a hover state, visually indicating when the user hovers over the checkbox. This can be useful for enhancing the user experience.

**Properties:**

This widget has following **required** parameters:

```
Name                         Description
```

```
label(string)               label associated with checkbox
```

```
onChange(boolCallBack)      callback function when the checkbox value changes
```

These are some option parameters:

```
value(default: false)        current state of checkbox
```

```
isDisabled                     indicates whether checkbox is disabled
```

```
iconColor                    checkbox color can be customized using this
```

```
Padding                      padding around checkbox widget
```

**Usages:**

Add the following lines of code:

```
DigitCheckbox(
  label: "Label for checkbox",
  onChanged: (value) {},
),
```
