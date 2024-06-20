# Radio

## Overview

The Radio Buttons component in DIGIT UI empowers users to make a single selection from a list of options. This intuitive interface provides a smooth user experience with hover and mouse-down effects. It is designed to handle both horizontal and vertical layouts based on the screen width.

## **Properties**

Below are some **required** parameters inside the radio list:

```
Name                            Description
```

```
radioButtons                 A list of RadioButtonModel representing the radio button
```

```
onChanged                   a callback when a radio button is selected
```

The following are additional parameters:

```
groupValue                  the current selected value in the radio group, using this
                            any radio button can be selected initially, the default is a
                            empty string.
```

```
isDisabled                   indicates whether radio buttons are disabled
```

```
containerPadding              padding applied around each radio button
```

## **Configuration**

**Usages**

Add the below lines of code to configure the radio button:

```
RadioList(
  onChanged: (value) {},
  radioButtons: [
    RadioButtonModel(code: '1',name: 'One',),
    RadioButtonModel(code: '2', name: 'Two'),
    RadioButtonModel(code: '3', name: 'Three'),
  ],
);
```