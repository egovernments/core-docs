# Input Field

## Description

The Input field enables users to interact with the application through content input and data. The component allows users to input responses or data based on specific requirements.

## Configuration

#### **Config for TextInput Component (using FormComposerV2)** <a href="#id-1mwkh8rij8gt" id="id-1mwkh8rij8gt"></a>

**Type: text**

```
{
inline:true,
label:"Example",
placeholder:"Enter Text"
isMandatory: true,
type:"text",
disable:false,
nonEditable:false,
infoMessage:"Sample info message"
description:"Help Text"
charCount:true,
withoutLabel:false,
populators:{
name:"defaultText",
error:"Error Message",
validation:{minLength:2, maxLength:10},
customIcon:"DownloadIcon",
onIconSelection:{(e)=>{console.log("clicked");}}
prefix:"$",
suffix:"$",
wrapLabel:true
}
}
```

Below are the details for the type: text:

<table><thead><tr><th width="195">Label</th><th>Label for text field</th></tr></thead><tbody><tr><td>placeholder</td><td>Placeholder for the text field</td></tr><tr><td>isMandatory</td><td>Whether field is mandatory or not</td></tr><tr><td>disable</td><td>To disable the text field (no interaction will be possible if disabled)</td></tr><tr><td>nonEditable</td><td>To make text field readOnly</td></tr><tr><td>infoMessage</td><td>Information to be shown when hovered on the info icon beside the label</td></tr><tr><td>description</td><td>Help text for the text field</td></tr><tr><td>charCount</td><td>Number of characters in the input value</td></tr><tr><td>withoutLabel</td><td>Default will be false, if sent as true then label won't be shown</td></tr><tr><td>populators</td><td><p>Name : Mandatory field</p><p>Error : Error message to be shown</p><p>Validations: if required like maxlength, minlength etc</p><p>customIcon: to show any icon inside the text field (can be sent as a string)</p><p>onIconSelection: IconSelection function</p><p>Prefix: To show prefix</p><p>Suffix: to show suffix</p></td></tr><tr><td>wrapLabel</td><td>Can wrap label to the next line in desktop and tablet screens</td></tr></tbody></table>

**Example Usage of TextInput Component**

```
<TextInput
type="text"
disabled={false}
populators={{customIcon: "MyLocation"}
onIconSelection={()=>{console.log("selected")}
></TextInput>
```

For more information: [StoryBook for Text Input field](https://unified-dev.digit.org/storybook/?path=/story/atom-groups-inputfield--default)

**Type: date**

```
{
label:"ExampleDate",
placeholder:"dd/mm/yyyy"
isMandatory: true,
type:"date",
disable:false,
nonEditable:false,
infoMessage:"Sample info message"
description:"Help Text"
charCount:true,
withoutLabel:false,
populators:{
name:"defaultDate",
error:"Error Message",
editableDate:true
}
}
```

The date can be selected from the date chart. If editableDate is set to true, the date can be edited without using the date chart; otherwise, it cannot be edited.

For more information: [StoryBook for date field](https://unified-dev.digit.org/storybook/?path=/story/atom-groups-inputfield--default\&args=type:date)

**Type: time**

```
{
label:"ExampleTime",
placeholder:"placeholder"
isMandatory: true,
type:"time",
disable:false,
nonEditable:false,
infoMessage:"Sample info message"
description:"Help Text"
charCount:true,
withoutLabel:false,
populators:{
name:"defaultTime",
error:"Error Message",
editableTime:true
}
}
```

The time can be selected from the time chart. If `editableTime` is set to `true`, the time can be edited without using the time chart; otherwise, it cannot be edited.

For more information: [StoryBook for time field](https://unified-dev.digit.org/storybook/?path=/story/atom-groups-inputfield--default\&args=type:time)

**Type: geolocation**

```
{
label:"ExampleGeolocation",
placeholder:"placeholder"
isMandatory: true,
type:"geolocation",
disable:false,
nonEditable:false,
infoMessage:"Sample info message"
description:"Help Text"
charCount:true,
withoutLabel:false,
populators:{
name:"defaultGeolocation",
error:"Error Message",
onIconSelection:{(e)=>{console.log(“clicked”);}}
}
}
```

Click on the geolocation icon to call and activate the onIconSelection function. Otherwise, the location details are captured by default.

For more information: [StoryBook for Geolocation field](https://unified-dev.digit.org/storybook/?path=/story/atom-groups-inputfield--default\&args=type:geolocation)

**Type: numeric**

```
{
label:"ExampleNumeric",
placeholder:"placeholder"
isMandatory: true,
type:"numeric",
disable:false,
nonEditable:false,
infoMessage:"Sample info message"
description:"Help Text"
charCount:true,
withoutLabel:false,
populators:{
name:"defaultGeolocation",
error:"Error Message",
},
config:{step:””}
}
```

The numeric value by default increases and decreases by step value 1. But it can be configured using the step value sent as a prop in the config.

For more information: [StoryBook for Numeric field](https://unified-dev.digit.org/storybook/?path=/story/atom-groups-inputfield--default\&args=type:numeric)

**With Prefix and Suffix**

```
{
label:"ExamplePrefix",
placeholder:"placeholder"
isMandatory: true,
type:"text",
disable:false,
nonEditable:false,
infoMessage:"Sample info message"
description:"Help Text"
charCount:true,
withoutLabel:false,
populators:{
name:"defaultText",
error:"Error Message",
prefix:”+91”
},
}
```

```
{
label:"ExampleSuffix",
placeholder:"placeholder"
isMandatory: true,
type:"text",
disable:false,
nonEditable:false,
infoMessage:"Sample info message"
description:"Help Text"
charCount:true,
withoutLabel:false,
populators:{
name:"defaultText",
error:"Error Message",
suffix:”Kg”
},
}
```

**Type: password**

```
{
label:"ExamplePassword",
placeholder:"placeholder"
isMandatory: true,
type:"password",
disable:false,
nonEditable:false,
infoMessage:"Sample info message"
description:"Help Text"
charCount:true,
withoutLabel:false,
populators:{
name:"defaultText",
error:"Error Message",
},
}
```

For more information: [Storybook for password field](https://unified-dev.digit.org/storybook/?path=/story/atom-groups-inputfield--default\&args=type:numeric)

**Type: search**

```
{
label:"ExampleSearch",
placeholder:"placeholder"
isMandatory: true,
type:"search",
disable:false,
nonEditable:false,
infoMessage:"Sample info message"
description:"Help Text"
charCount:true,
withoutLabel:false,
populators:{
name:"defaultSearch",
error:"Error Message",
onIconSelection:{(e)=>{console.log(“clicked”);}}
}
}
```

#### **Config for TextArea Component (using FormComposerV2)** <a href="#gxsd3529bja3" id="gxsd3529bja3"></a>

```
{
label:"ExampleTextArea",
placeholder:"placeholder"
isMandatory: true,
type:"textarea",
disable:false,
nonEditable:false,
infoMessage:"Sample info message"
description:"Help Text"
charCount:true,
withoutLabel:false,
populators:{
name:"defaultSearch",
error:"Error Message",
resizeSmart: false,
}

```

There are two variants for the textarea - one has a resize option and the other is resizeSmart which auto-adjusts the height based on the input content.

For more information: [Storybook for TextArea](https://unified-dev.digit.org/storybook/?path=/story/atom-groups-inputfield--default\&args=type:textarea)
