---
description: Design System - Switch component
---

# Switch

The Switch component is used to toggle between two binary states, such as On/Off, Enable/Disable, or Active/Inactive. It offers a direct, easy-to-understand interaction and provides instant feedback. The design ensures accessibility, responsiveness, and consistency across applications.

<figure><img src="../../../../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

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

***

<figure><img src="../../../../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Default</strong></p><p>This is a clean toggle without any accompanying label or icon. It's compact and ideal for minimal layouts where the switch’s meaning is already clear from context.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>With Symbol</strong></p><p>This variant includes a symbol (like "|" for On and "◯" for Off) inside the switch thumb. It enhances visual clarity and is useful when colour alone isn't enough to indicate the switch's state.</p></td></tr></tbody></table>

***

## Properties

|                                                                                                                                                                                                                               |                                                                                                                          |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| <p><strong>With Icon</strong></p><p>An optional icon can be added to the left or right (dismiss/close icon). This enhances usability and improves scanability, especially for chips used in status indicators or filters.</p> | <div><figure><img src="../../../../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure></div> |

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>isLabelFirst</td><td>text</td><td></td></tr><tr><td>label</td><td>text</td><td></td></tr><tr><td>shapeOnOff</td><td>yes/no</td><td>no</td></tr><tr><td>isCheckedInitially</td><td>yes/no</td><td>no</td></tr><tr><td>onToggle</td><td>number</td><td></td></tr><tr><td>className</td><td>yes/no</td><td></td></tr><tr><td>style</td><td>yes/no</td><td>no</td></tr><tr><td>disable</td><td>yes/no</td><td>no</td></tr><tr><td>switchStyle</td><td>yes/no</td><td>no</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>Title</td><td>String</td><td>required(if header is not passed)</td></tr><tr><td>Number</td><td>double</td><td>-</td></tr><tr><td>Icon</td><td>Icon widget</td><td>-</td></tr><tr><td>header</td><td>Widget</td><td>-</td></tr><tr><td>content</td><td>Widget</td><td>required</td></tr><tr><td>divider</td><td>bool</td><td>false</td></tr><tr><td>initiallyExpanded</td><td>bool</td><td>false</td></tr><tr><td>showBorder</td><td>bool</td><td>false</td></tr><tr><td>onToggle</td><td>VoidCallBack Function</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

***

## Behaviours

|                                                                                                                       |                                                                                                                                                                                                                                                                                    |
| --------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Label</strong></p><p>Use switches to represent binary on/off states. They are ideal for toggling settings or features that require immediate activation or deactivation.</p><p>Avoid using switches to indicate errors. Switches are not designed for error states.</p> |
| <div><figure><img src="../../../../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Label Alignment</strong></p><p>The placement of the label can be customised to appear left or right of the switch. This helps maintain visual balance depending on layout needs and reading flow.</p>                                                                   |

***

## Usage Guide

***

| <div><figure><img src="../../../../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Use dividers for activation states</strong></p><p>Use switches to represent binary on/off states. They are ideal for toggling settings or features that require immediate activation or deactivation.</p><p>Avoid using switches to indicate errors. Switches are not designed for error states.</p> |
| --------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure></div> |                                                                                                                                                                                                                                                                                                                 |

## Changelog

***

| Date         | Number  | Notes                                                                                           |
| ------------ | ------- | ----------------------------------------------------------------------------------------------- |
| Dec 15, 2024 | v-0.0.2 | <p>This component is added to the website.<br>This component is now individually versioned.</p> |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Content guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
