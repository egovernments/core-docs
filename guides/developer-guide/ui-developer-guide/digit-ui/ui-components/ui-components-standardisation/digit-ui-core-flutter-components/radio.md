# Radio

The Radio Buttons component in Digit UI Components empowers users to make a single selection from a list of options. This intuitive interface provides a smooth user experience with hover and mouse-down effects. It is designed to handle both horizontal and vertical layouts based on the screen width.

**Properties:**

These are some **required** parameters inside the radio list:

```
Name                            Description
```

```
radioButtons                 A list of RadioButtonModel representing the radio button
```

```
onChanged                   a callback when a radio button is selected
```

These are additional parameters:

```
groupValue                  the current selected value in the radio group, using this
                            any radio button can be selected initially, default is a
                            empty string.
```

```
isDisabled                   indicates whether radio buttons are disabled
```

```
containerPadding              padding applied around each radio button
```

**Usages:**

Add this lines of code:

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
