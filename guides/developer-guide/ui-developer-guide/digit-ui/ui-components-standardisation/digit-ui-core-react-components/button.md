# Button

## **Description** <a href="#id-6hwdxa6yactk" id="id-6hwdxa6yactk"></a>

Buttons are used for specific user actions. These clickable UI components allow the users to interact with the system.&#x20;

## Configuration

#### **Usage of Button Component** <a href="#id-6hwdxa6yactk" id="id-6hwdxa6yactk"></a>

**Primary Variant**

```
<Button
variation="primary"
label={"Primary"}
type="button"
icon="MyLocation"
isSuffix={false}
isDisabled={false}
/>
```

**Secondary Variant**

```
<Button
variation="secondary"
label={"Secondary"}
type="button"
icon="MyLocation"
isSuffix={false}
isDisabled={false}
/>
```

**Tertiary Variant**

```
<Button
variation="teritiary"
label={"Teritiary"}
type="button"
icon="MyLocation"
isSuffix={false}
isDisabled={false}
/>
```

**Link Variant**

```
<Button
variation="link"
label={"Link"}
type="button"
icon="MyLocation"
isSuffix={false}
isDisabled={false}
/>
```

Icons are sent as a string added before the label. To add it as a suffix, set the isSuffix parameter to true.

For more information: [StoryBook for button components](https://unified-dev.digit.org/storybook/?path=/story/atom-groups-buttonfield--primary)
