---
description: Design System - Footer component
---

# Footer

The Footer component provides navigational actions or supplementary content at the bottom of pages. It serves as a closing control panel for tasks or flows, ensuring alignment with accessibility, responsiveness, and contextual clarity across applications.

<figure><img src="../../../../../.gitbook/assets/image (536).png" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="Component React" %}
```
// Sample code

  <CheckBox
    label="Label"
    onChange={(e)=>{console.log(e.target.checked}}
  />
```
{% endtab %}

{% tab title="Component Flutter" %}
```
// Sample code

DigitAccordion(
              header: Text('Accordion'),
              content: Text('This is the content of Accordion'),
              initiallyExpanded: false,
              divider: true,
              showBorder: true,
            ),
```
{% endtab %}

{% tab title="Component Design" %}

{% endtab %}
{% endtabs %}

## Anatomy

<figure><img src="../../../../../.gitbook/assets/image (537).png" alt=""><figcaption></figcaption></figure>

***

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (538).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Default</strong></p><p>A straightforward footer with clearly defined action buttons like "Back" and "Next," used in linear flows or form-based screens.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (539).png" alt=""><figcaption></figcaption></figure></div></td><td><strong>Flex</strong><br>A more dynamic variant that allows flexible content like dropdown menus, dynamic button alignment, and custom text</td></tr></tbody></table>

## Properties

<table data-header-hidden data-full-width="false"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Button</strong><br>Supports multiple button styles, including:<br>Primary (e.g., “Next”)<br>Secondary (e.g., “Back”)<br>Tertiary (optional actions)<br>Dropdown / Dropup menus (used to group multiple actions)<br></td><td><div><figure><img src="../../../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Extra Content</strong><br>Allows inclusion of helper or legal text beneath or between buttons, offering context or attribution.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure></div></td></tr></tbody></table>

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>className</td><td>text</td><td>-</td></tr><tr><td>style</td><td>text</td><td>-</td></tr><tr><td>actionFields</td><td>yes/no</td><td>no</td></tr><tr><td>maxActionFieldsAllowed</td><td>yes/no</td><td>no</td></tr><tr><td>sortActionFields</td><td>number</td><td>-</td></tr><tr><td>setactionFieldsToRight</td><td>yes/no</td><td>-</td></tr><tr><td>setactionFieldsToLeft</td><td>yes/no</td><td>no</td></tr><tr><td>children</td><td>yes/no</td><td>no</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>Title</td><td>String</td><td>required(if header is not passed)</td></tr><tr><td>Number</td><td>double</td><td>-</td></tr><tr><td>Icon</td><td>Icon widget</td><td>-</td></tr><tr><td>header</td><td>Widget</td><td>-</td></tr><tr><td>content</td><td>Widget</td><td>required</td></tr><tr><td>divider</td><td>bool</td><td>false</td></tr><tr><td>initiallyExpanded</td><td>bool</td><td>false</td></tr><tr><td>showBorder</td><td>bool</td><td>false</td></tr><tr><td>onToggle</td><td>VoidCallBack Function</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

## Usage Guide

***

| <div><figure><img src="../../../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Button Labeling</strong></p><p>Clearly label all buttons with actionable language like “Next,” “Submit,” or “Save”.  Avoid using vague or unclear labels like “Click” or “Okay” that provide no guidance on the action.</p> |
| -------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure></div> |                                                                                                                                                                                                                                        |

## Change log

***

| Date | Number | Notes |
| ---- | ------ | ----- |
|      |        |       |
|      |        |       |
|      |        |       |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td>All interactive states</td></tr><tr><td>true</td><td>Accessible use of colours</td></tr><tr><td>true</td><td>Accessible contrast for text</td></tr><tr><td>true</td><td>Accessible contrast for UI components</td></tr><tr><td>true</td><td>Keyboard interactions</td></tr></tbody></table>
