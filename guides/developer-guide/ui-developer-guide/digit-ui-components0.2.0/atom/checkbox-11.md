---
description: Design System - Chips component
---

# Chips

The Chips component is a compact, interactive UI element used to display discrete pieces of information, user selections, filters, tags, or statuses. This chip's component enhances the interface by providing quick insights or actions in a visually organised way without overwhelming the user.

<figure><img src="../../../../../.gitbook/assets/image (21) (1) (1).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (4) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Default</strong></p><p>This represents the standard chip style, which has a neutral background, commonly used for user choices, tags, or options, and this is also non-dismissable by default.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (3) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Error</strong></p><p>This highlights the invalid or incorrect selections and is also styled with a red border and background to indicate a problem or error state.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>With Close</strong></p><p>This includes a dismiss (close) icon that allows users to remove a selection or input dynamically and is useful for multi-select filters, form tags, or user-generated inputs.</p></td></tr></tbody></table>

***

## Properties

|                                                                                                                                                                                                                               |                                                                                                                                      |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| <p><strong>With Icon</strong></p><p>An optional icon can be added to the left or right (dismiss/close icon). This enhances usability and improves scanability, especially for chips used in status indicators or filters.</p> | <div><figure><img src="../../../../../.gitbook/assets/image (5) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div> |

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>className</td><td>text</td><td>-</td></tr><tr><td>text</td><td>text</td><td>no</td></tr><tr><td>onTagClick</td><td>yes/no</td><td>no</td></tr><tr><td>onClick</td><td>yes/no</td><td>-</td></tr><tr><td>extraStyles</td><td>number</td><td>-</td></tr><tr><td>disabled</td><td>yes/no</td><td>-</td></tr><tr><td>isErrorTag</td><td>yes/no</td><td>no</td></tr><tr><td>error</td><td>yes/no</td><td>no</td></tr><tr><td>hideClose</td><td>yes/no</td><td>no</td></tr><tr><td>onErrorClick</td><td>number</td><td>no</td></tr><tr><td>iconReq</td><td>yes/no</td><td>no</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>Title</td><td>String</td><td>required(if header is not passed)</td></tr><tr><td>Number</td><td>double</td><td>-</td></tr><tr><td>Icon</td><td>Icon widget</td><td>-</td></tr><tr><td>header</td><td>Widget</td><td>-</td></tr><tr><td>content</td><td>Widget</td><td>required</td></tr><tr><td>divider</td><td>bool</td><td>false</td></tr><tr><td>initiallyExpanded</td><td>bool</td><td>false</td></tr><tr><td>showBorder</td><td>bool</td><td>false</td></tr><tr><td>onToggle</td><td>VoidCallBack Function</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

***

## Behaviours

|                                                                                                                                      |                                                                                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (6) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Compact &#x26; Responsive</strong></p><p>This Chips component is designed to occupy minimal space, and it also auto-resizes based on content and adapts to containers across screen sizes.</p> |

***

## Usage Guide

***

| <div><figure><img src="../../../../../.gitbook/assets/image (7) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Use Chips to show selected options</strong></p><p>Use chips to display selected options in a multi-select dropdown, making it easy for users to review and remove selections if needed.  </p><p></p><p>Avoid using chips that don’t clearly show how to remove or edit them, and don’t display error states without simple instructions on how to fix the issue.  </p> |
| ------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (8) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div> |                                                                                                                                                                                                                                                                                                                                                                                   |

## Changelog

***

| Date         | Number  | Notes                                                                                           |
| ------------ | ------- | ----------------------------------------------------------------------------------------------- |
| Dec 15, 2024 | v-0.0.2 | <p>This component is added to the website.<br>This component is now individually versioned.</p> |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Content guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
