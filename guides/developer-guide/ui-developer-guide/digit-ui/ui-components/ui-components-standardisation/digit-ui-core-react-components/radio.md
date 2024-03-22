# Radio

#### **Config for Radio Component (using FormComposerV2)** <a href="#f5cx7rg1qwba" id="f5cx7rg1qwba"></a>

```
{
isMandatory: false,
type: "radio",
key: "genders",
label: "Deafult",
disable: false,
populators: {
name: "radio-Deafult",
optionsKey: "name",
error: "Error!",
required: true,
mdmsConfig: {
masterName: "GenderType",
moduleName: "common-masters",
localePrefix: "COMMON_GENDER",
},
},
}
```

While using the radio component independently and to disable it set the prop as disabled={true}.

For more information: [Storybook for radio field](https://unified-dev.digit.org/storybook/?path=/story/atom-groups-radiofield--default)
