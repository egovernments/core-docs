# Toast

## **Description** <a href="#z9xnle6d7qbw" id="z9xnle6d7qbw"></a>

The Toast component is used to provide users with temporary notifications. It does not require any user action.&#x20;

## **Configuration** <a href="#z9xnle6d7qbw" id="z9xnle6d7qbw"></a>

#### **Usage of Toast Component (using FormComposerV2)** <a href="#z9xnle6d7qbw" id="z9xnle6d7qbw"></a>

**Success Toast**

```
<Toast
label={"Success Toast Message"}
onClose={}
transitionTime={}
/>
```

**Warning Toast**

```
<Toast
label={"Warning Toast Message"}
warning={“warning”}
onClose={}
transitionTime={}
/>
```

**Error Toast**

```
<Toast
label={"Error Toast Message"}
error={true}
onClose={}
transitionTime={}
/>
```

The default transitionTime for any variant of toast is 5 seconds. However, this is configurable using the transitionTime prop (in milliseconds).

For more information: [Storybook for Toast](https://unified-dev.digit.org/storybook/?path=/story/atom-groups-toast--success-toast)
