# Toast

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

The default transitionTime for any variant of toast will be 5 seconds, but that can be configurable using the transitionTime prop (in milliseconds).

For more information: [Storybook for Toast](https://unified-dev.digit.org/storybook/?path=/story/atom-groups-toast--success-toast)
