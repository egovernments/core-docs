# Toggle

## Overview

The Toggle Buttons component in DIGIT UI presents a list of interactive toggle buttons, providing users with the ability to select an option. Each button is equipped with callbacks for both mouse-down and hover effects, ensuring a responsive and engaging user interface.

### **Properties**

The widget contains the following **required** parameters:

```
Name                           Description
```

```
toggleButtons                   A list of ToggleButtonModels that define the toggle 
                                button
```

```
onChanged                       a callback when a toggle is selected
```

Below are some additional parameters:

```
selectedIndex                 initially selected toggle(by default first toggle will 
                              be selected)
```

```
contentPadding                optional Padding around toggle buttons
```

## **Configuration**

**Usages**

Add the following lines of code:

```
ToggleList(
  toggleButtons: [
    ToggleButtonModel(
      name: 'Toggle 1', key: 'key1', onSelected: (value) {}),
    ToggleButtonModel(
      name: 'Toggle 2', key: 'key2', onSelected: (value) {}),
    ToggleButtonModel(
      name: 'Toggle 3', key: 'key3', onSelected: (value) {}),
  ],
  selectedIndex: 1,
onChanged: (selectedValues) {},
);
```
