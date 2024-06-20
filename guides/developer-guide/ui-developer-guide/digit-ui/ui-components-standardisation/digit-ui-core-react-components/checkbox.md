# Checkbox

## **Description** <a href="#hoqgfvm6xrz1" id="hoqgfvm6xrz1"></a>

The checkbox component allows users to select one or multiple options from a given set of choices.&#x20;

## **Configuration**

#### **Config for Checkbox Component (using FormComposerV2)** <a href="#hoqgfvm6xrz1" id="hoqgfvm6xrz1"></a>

```
{
inline:true,
isMandatory: true,
type:"checkbox",
disable:false,
withoutLabel:true,
populators:{
name:"checkbox",
error:"Error Message",
title:”Checkbox Label”,
isLabelFirst: false,
}
}
```

By default, the checkbox appears before the label, but this order can be changed using the `isLabelFirst` option.

For more information: [Storybook for checkbox field](https://unified-dev.digit.org/storybook/?path=/story/atom-groups-checkboxfield--default)
