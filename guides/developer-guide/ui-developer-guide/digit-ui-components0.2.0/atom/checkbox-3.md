---
description: Design System - Checkbox component
---

# Checkbox

The Checkbox is a simple selection control that allows users to make binary choices, such as selecting or deselecting options. It is commonly used in forms, preference settings, and multi-select scenarios, providing clear visual feedback for user actions.

<figure><img src="../../../../../.gitbook/assets/image (346).png" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="Component React" %}
```
// Sample code
<CheckBox
      label={"Label"}
      checked={isChecked}
      onChange={(e)=>{console.log(e.target.checked}}
></CheckBox>
```
{% endtab %}

{% tab title="Component Flutter" %}
```
// Sample code

 DigitCheckbox(
    label: 'I agree to terms and conditions',
    value: true,
    onChanged: (value) {
      ////  update your state 
   },
    isDisabled: false,
    isRequired: true,
  )
```
{% endtab %}

{% tab title="Component Design" %}

{% endtab %}
{% endtabs %}

## Anatomy

***

<figure><img src="../../../../../.gitbook/assets/Imagea.png" alt=""><figcaption></figcaption></figure>

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><img src="../../../../../.gitbook/assets/Imagev1.png" alt=""></td><td><p><strong>Checked</strong></p><p>The checked state indicates that the user has actively selected the option. It provides clear visual feedback with a filled checkbox, often accompanied by a checkmark. This state should be used when an option is explicitly chosen or enabled by default.</p></td></tr><tr><td><img src="../../../../../.gitbook/assets/Imagev2.png" alt="" data-size="original"></td><td><strong>Intermediate</strong><br>The indeterminate state represents a mixed selection, typically used for parent checkboxes in multi-select scenarios. It visually signals that only some child options are selected, rather than all. This state does not appear by direct user interaction but is controlled programmatically to reflect partial selections.</td></tr><tr><td><img src="../../../../../.gitbook/assets/Imagev3.png" alt=""></td><td><p><strong>Unchecked</strong></p><p>The unchecked state indicates that the option is not selected. It appears as an empty checkbox, providing a clear visual cue that no action has been taken. This is the default state unless specified otherwise.</p></td></tr></tbody></table>

## Properties

<table data-header-hidden data-full-width="false"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Label</strong><br>This property represents the text displayed inside the button. It is a required field and helps users understand the action that the button will trigger. The label should be concise and clear to communicate the button’s purpose effectively.<br></td><td><img src="../../../../../.gitbook/assets/Imagep1.png" alt=""></td></tr><tr><td><strong>Disabled</strong><br>The “isDisabled” property disables the button, preventing any user interaction. It also applies a disabled visual style (like graying out the button) to indicate that the button is not active.</td><td><img src="../../../../../.gitbook/assets/Imagep2.png" alt=""></td></tr><tr><td><strong>Icon</strong><br>The icon property specifies the name of the icon to be rendered inside the button. This helps provide a visual cue along with the button text. The icon placement can be either before or after the label based on the how the “Prefix” and “Suffix” properties are defined.</td><td><img src="../../../../../.gitbook/assets/Imagep3.png" alt=""></td></tr><tr><td><strong>Size</strong><br>The size property specifies the size of the button. You can choose between "large", "medium", and "small" to adjust the button's height and font size.</td><td><img src="../../../../../.gitbook/assets/Imagep4.png" alt=""></td></tr><tr><td><strong>Type</strong><br>The type property determines the HTML type attribute for the button, such as "submit", "button", or "actionButton". This is useful for form submission or defining button behavior in HTML forms.</td><td><img src="../../../../../.gitbook/assets/Imagep5.png" alt=""></td></tr></tbody></table>

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>label</td><td>string</td><td>-</td></tr><tr><td>onChange</td><td>function</td><td>-</td></tr><tr><td>value</td><td>string</td><td>-</td></tr><tr><td>disabled</td><td>boolean</td><td>-</td></tr><tr><td>inputRef</td><td>reference to a DOM element</td><td>-</td></tr><tr><td>checked</td><td>boolean</td><td>false</td></tr><tr><td>pageType</td><td>string</td><td>-</td></tr><tr><td>style</td><td>object</td><td>-</td></tr><tr><td>index</td><td>number</td><td>0</td></tr><tr><td>isLabelFirst</td><td>boolean</td><td>false</td></tr><tr><td>hideLabel</td><td>boolean</td><td>-</td></tr><tr><td>isIntermediate</td><td>boolean</td><td>false</td></tr><tr><td>mainClassName</td><td>string</td><td>-</td></tr><tr><td>id</td><td></td><td>-</td></tr><tr><td>labelClassName</td><td>string</td><td>-</td></tr><tr><td>onLabelClick</td><td>function</td><td>-</td></tr><tr><td>inputWrapperClassName</td><td>string</td><td>-</td></tr><tr><td>inputClassName</td><td>string</td><td>-</td></tr><tr><td>inputIconClassname</td><td>string</td><td>-</td></tr><tr><td>iconFill</td><td>string</td><td>-</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>value</td><td>bool</td><td>required</td></tr><tr><td>label</td><td>String</td><td>-</td></tr><tr><td>onChanged</td><td>ValueChanged&#x3C;bool></td><td>-</td></tr><tr><td>isDisabled</td><td>bool</td><td>-</td></tr><tr><td>alignRight</td><td>bool</td><td>-</td></tr><tr><td>readOnly</td><td>bool</td><td>false</td></tr><tr><td>checkboxThemeData</td><td>DigitCheckboxThemeData</td><td>false</td></tr><tr><td>isRequired</td><td>bool</td><td>false</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

## Interaction State

***

| ![](../../../../../.gitbook/assets/Imageb1.png) | <p><strong>Hover State</strong></p><p>When a user hovers over the button, a visual cue is added to emphasize interactivity. This is achieved by introducing a subtle line below the button. The line appears as a clean, horizontal underline that complements the button's style, without overwhelming the design. The hover state enhances the button's affordance, guiding users and improving interactivity without altering the button’s primary layout or design.</p> |
| ----------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![](../../../../../.gitbook/assets/Imageb2.png) | <p><strong>Mousedown State</strong></p><p>The Mouse Down state of the button represents the moment when the user clicks and holds the button. This state provides immediate feedback to the user, confirming that their interaction has been registered. The text label becomes bolder, emphasizing the active interaction</p>                                                                                                                                              |

## Usage Guide

***

| <div><figure><img src="../../../../../.gitbook/assets/image (348).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Usage for multiselection</strong></p><p>Checkboxes should be used when users need to select any number of choices from a list of options. They are appropriate when presenting independent options where multiple selections are allowed simultaneously.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ---------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (347).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Avoid interchanging checkboxes with Radio buttons</strong> </p><p>Checkboxes should be used when users need to select any number of options from a list (including zero, one, or multiple selections). They represent independent choices that don't affect each other. Checkboxes work well for "opt-in" scenarios, toggling features on/off, or when users need to select multiple items from a visible set of options. <br>Radio buttons, by contrast, should only be used when users must select exactly one option from a set of mutually exclusive choices. Using checkboxes when a single selection is required creates confusion and violates established interaction patterns, potentially leading to user frustration and errors.</p> |
|                                                                                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |

## Changelog

***

| Date         | Number  | Notes                                                                                           |
| ------------ | ------- | ----------------------------------------------------------------------------------------------- |
| Dec 15, 2024 | v-0.0.2 | <p>This component is added to the website.<br>This component is now individually versioned.</p> |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Content guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
