---
description: Design System - Button component
---

# Button

The Button is a basic interactive element used to perform actions or navigate within an app. It helps users complete tasks like submitting forms, starting processes, or opening pages, making it an essential part of any interface.

<figure><img src="../../../../../../../.gitbook/assets/Image (1).png" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="Component React" %}
```
// Sample code

<Button 
  icon="CheckCircle" 
  label={t("Label")} 
  title={t("LabelMore")} 
  onClick={() => console.log("clicked")} 
  type="button" 
  variation="primary" 
/>
```
{% endtab %}

{% tab title="Component Flutter" %}
```
// Sample code

DigitButton(
          label: Primary Button,
          onPressed: () {},
          type: DigitButtonType.primary,
          isDisabled: false,
          size: DigitButtonSize.small
          suffixIcon: Icons.home,
        );
```
{% endtab %}

{% tab title="Component Design" %}
{% embed url="https://www.figma.com/design/sH2pLZBXZZ6c7LlfQwFFjR/Design-System?node-id=10013-14407&t=bXeR2K2cY0SyAPnC-0" %}
{% endtab %}
{% endtabs %}

## Anatomy

***

<figure><img src="../../../../../../../.gitbook/assets/Image (2).png" alt=""><figcaption></figcaption></figure>

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><img src="../../../../../../../.gitbook/assets/Image1 (2).png" alt=""></td><td><p>P<strong>rimary</strong> </p><p>The primary button is the default action button and is used for the most prominent action on a page or view. It uses a solid fill color to stand out. Only one primary button should appear per view to maintain a clear focus and hierarchy. Use it thoughtfully to avoid overwhelming users or diluting its importance.</p></td></tr><tr><td><img src="../../../../../../../.gitbook/assets/Image2.png" alt="" data-size="original"></td><td><strong>Secondary</strong><br>The secondary button communicates a moderate level of emphasis and is intended for actions that complement the primary or accent actions in a view. With a simple stroke and no fill, it maintains a clean and subtle appearance. These buttons are typically used for secondary tasks or options that provide additional functionality but are not critical to the core experience. </td></tr><tr><td><img src="../../../../../../../.gitbook/assets/Image3.png" alt=""></td><td><p><strong>Tertiary</strong></p><p>The tertiary button is a minimal, text-only variant designed for actions with less prominence in the overall hierarchy. It is used for secondary or supportive actions that complement primary tasks.</p></td></tr><tr><td><img src="../../../../../../../.gitbook/assets/Image4.png" alt="" data-size="original"></td><td><strong>Link</strong><br>The link button communicates navigation or secondary actions and is represented as text with an underline. Use link buttons to direct users to related content, additional resources, or less critical actions without disrupting the visual hierarchy of the page.</td></tr></tbody></table>

## Properties

<table data-header-hidden data-full-width="false"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Label</strong><br>This property represents the text displayed inside the button. It is a required field and helps users understand the action that the button will trigger. The label should be concise and clear to communicate the button’s purpose effectively.<br></td><td><img src="../../../../../../../.gitbook/assets/Imagep1.png" alt=""></td></tr><tr><td><strong>Disabled</strong><br>The “isDisabled” property disables the button, preventing any user interaction. It also applies a disabled visual style (like graying out the button) to indicate that the button is not active.</td><td><img src="../../../../../../../.gitbook/assets/Imagep2.png" alt=""></td></tr><tr><td><strong>Icon</strong><br>The icon property specifies the name of the icon to be rendered inside the button. This helps provide a visual cue along with the button text. The icon placement can be either before or after the label based on the how the “Prefix” and “Suffix” properties are defined.</td><td><img src="../../../../../../../.gitbook/assets/Imagep3.png" alt=""></td></tr><tr><td><strong>Size</strong><br>The size property specifies the size of the button. You can choose between "large", "medium", and "small" to adjust the button's height and font size.</td><td><img src="../../../../../../../.gitbook/assets/Imagep4.png" alt=""></td></tr><tr><td><strong>Type</strong><br>The type property determines the HTML type attribute for the button, such as "submit", "button", or "actionButton". This is useful for form submission or defining button behavior in HTML forms.</td><td><img src="../../../../../../../.gitbook/assets/Imagep5.png" alt=""></td></tr></tbody></table>

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
| Property              | Value                      | Default |
| --------------------- | -------------------------- | ------- |
| label                 | string                     | -       |
| variation             | string                     | primary |
| iconFill              | string                     | -       |
| isDisabled            | boolean                    | -       |
| type                  | string                     | -       |
| icon                  | string                     | -       |
| size                  | string                     | large   |
| ref                   | reference to a DOM element | -       |
| className             | string                     | -       |
| submit                | string                     | -       |
| formId                | string                     | -       |
| onClick               | function                   | -       |
| title                 | string                     | -       |
| style                 | object                     | -       |
| isSuffix              | boolean                    | -       |
| textStyles            | object                     | -       |
| hideDefaultActionIcon | boolean                    | -       |
| options               | array                      | -       |
| isSearchable          | boolean                    | -       |
| optionsKey            | string                     | -       |
| menuStyles            | object                     | -       |
| showBottom            | boolean                    | -       |
| onOptionSelect        | function                   | -       |
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>label</td><td>String</td><td>required</td></tr><tr><td>onPressed</td><td>VoidCallBack Function</td><td>-</td></tr><tr><td>type</td><td>ButtonType(primary, secondary, tertiary, link)</td><td>-primary by default</td></tr><tr><td>size</td><td>ButtonSize(large, medium, small)</td><td>large by default</td></tr><tr><td>prefixIcon</td><td>IconData</td><td>-</td></tr><tr><td>suffixIcon</td><td>IconData</td><td>-</td></tr><tr><td>buttonTheme</td><td>DefaultButtonTheme</td><td>-</td></tr><tr><td>isDisabled</td><td>bool</td><td>false</td></tr><tr><td>capitalizedLetters</td><td>bool </td><td>true</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

## Behaviours

***

| ![](../../../../../../../.gitbook/assets/Imageb1.png)       | <p><strong>Hover State</strong></p><p>When a user hovers over the button, a visual cue is added to emphasize interactivity. This is achieved by introducing a subtle line below the button. The line appears as a clean, horizontal underline that complements the button's style, without overwhelming the design. The hover state enhances the button's affordance, guiding users and improving interactivity without altering the button’s primary layout or design.</p> |
| ----------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![](../../../../../../../.gitbook/assets/Imageb2.png)       | <p><strong>Mousedown State</strong></p><p>The Mouse Down state of the button represents the moment when the user clicks and holds the button. This state provides immediate feedback to the user, confirming that their interaction has been registered. The text label becomes bolder, emphasizing the active interaction</p>                                                                                                                                              |
| ![](<../../../../../../../.gitbook/assets/Imageb1 (1).png>) | <p><strong>Flexible Width</strong></p><p>The width of the button adjusts to the length of the text. This behaviour is dynamic with respect to the character limit defined. There is no text overflow in buttons.</p>                                                                                                                                                                                                                                                        |
| ![](<../../../../../../../.gitbook/assets/Imageb2 (1).png>) | <p><strong>Character Limit</strong></p><p>The default character limit for buttons is set to 64 characters to promote clear and concise actionable labels.</p>                                                                                                                                                                                                                                                                                                               |
| ![](../../../../../../../.gitbook/assets/Imageb3.png)       | <p><strong>Truncated Label</strong></p><p>If the label is too long to fit within the button, it will be truncated. The full text will be displayed on hover for web and on long press for mobile interfaces.</p>                                                                                                                                                                                                                                                            |

## Usage Guide

***

<table data-header-hidden><thead><tr><th></th><th valign="top"></th></tr></thead><tbody><tr><td><p><img src="../../../../../../../.gitbook/assets/Imageb4.png" alt=""></p><p><img src="../../../../../../../.gitbook/assets/Imageb5.png" alt=""></p></td><td valign="top"><p><strong>Use icons only when necessary</strong></p><p>Add icons to buttons only when they provide meaningful context or reinforce the action. Icons should be highly relevant and improve user understanding.  </p><p>Never include icons purely for visual appeal or without a clear purpose. Decorative icons can confuse users and detract from the button's functionality.</p></td></tr><tr><td><img src="../../../../../../../.gitbook/assets/Imageb6.png" alt=""></td><td valign="top"><p><strong>Do not override button colour</strong></p><p>Do not use custom colors for buttons. The colors of different button variations have been designed to be consistent and accessible.</p></td></tr></tbody></table>

## Content Guidelines

| <p><strong>Concise and actionable labels</strong></p><p>Button labels should be clear, concise, and action-oriented to help users understand their purpose instantly. Instead of words which are not verbs like "My Bills" or "Inbox," use specific phrases like "Download Bills " or "View Application" that tell users what will happen when clicked.   </p><p>Avoid unnecessary words that clutter the label—brevity improves readability and reduces cognitive load. Labels should also align with user expectations; for example, a delete action should say "Delete" instead of "Remove" if deletion is permanent.    </p> | ![](../../../../../../../.gitbook/assets/Imageb7.png) |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| <p><strong>Casing</strong></p><p>Use ‘Titlecase’ for buttons. This means capitalising the first letter of all words, except for articles and conjunctions. Eg. “Submit Feedback”, “Create Account”, “Learn More.”  </p><p>Title case enhances the emphasis of actions at the same time ensuring accessibility and readability. There can be exception to this casing definition if the action is a sentence.</p>                                                                                                                                                                                                                 | ![](../../../../../../../.gitbook/assets/Imageb8.png) |

## Change log

***

| Date | Number | Notes |
| ---- | ------ | ----- |
|      |        |       |
|      |        |       |
|      |        |       |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong><br>Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong><br>Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong><br>Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong><br>Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong><br>Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong><br>All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong><br>Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong><br>Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>true</td><td><strong>Content guidelines</strong><br>Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong><br>Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states...etc)</td></tr><tr><td>true</td><td><strong>Defined behaviors</strong><br>Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong><br>Access to the design file for the component in Figma multiple options, states, color themes, and platform scales.</td></tr></tbody></table>
