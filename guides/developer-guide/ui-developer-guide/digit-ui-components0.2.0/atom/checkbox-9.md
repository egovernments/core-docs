---
description: Design System - Breadcrumbs component
---

# Breadcrumbs

The Breadcrumbs component is a navigation aid that helps users understand their current position within a product’s hierarchy. It improves user orientation and facilitates smooth backwards navigation, particularly in multi-level interfaces.

<figure><img src="../../../../../.gitbook/assets/image (9) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../../../../.gitbook/assets/image (16) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Basic</strong></p><p>Displays the full navigation path linearly, and it's best used when the number of breadcrumb items is limited and space is sufficient.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Collapsed</strong></p><p>Compresses middle items into an ellipsis (...) for better scalability, and it's ideal for complex or deeply nested paths to maintain a clean layout.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>With Custom Separators</strong></p><p>Uses stylised or alternate separators like arrows (→) instead of slashes, and it enhances visual hierarchy and readability based on context or brand style.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>With Icons</strong></p><p>Includes relevant icons alongside each breadcrumb label.<br>Helps with quicker recognition and improves usability, especially for users with lower literacy or cognitive load.</p></td></tr></tbody></table>

***

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>crumbs</td><td>text</td><td>-</td></tr><tr><td>className</td><td>text</td><td>no</td></tr><tr><td>style</td><td>yes/no</td><td>no</td></tr><tr><td>spanStyle</td><td>yes/no</td><td>-</td></tr><tr><td>customSeperator</td><td>number</td><td>-</td></tr><tr><td>maxItems</td><td>yes/no</td><td>-</td></tr><tr><td>itemsBeforeCollapse</td><td>yes/no</td><td>no</td></tr><tr><td>itemsAfterCollapse</td><td>yes/no</td><td>no</td></tr><tr><td>expandText</td><td>yes/no</td><td>no</td></tr><tr><td>itemStyle</td><td>number</td><td>no</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>Title</td><td>String</td><td>required(if header is not passed)</td></tr><tr><td>Number</td><td>double</td><td>-</td></tr><tr><td>Icon</td><td>Icon widget</td><td>-</td></tr><tr><td>header</td><td>Widget</td><td>-</td></tr><tr><td>content</td><td>Widget</td><td>required</td></tr><tr><td>divider</td><td>bool</td><td>false</td></tr><tr><td>initiallyExpanded</td><td>bool</td><td>false</td></tr><tr><td>showBorder</td><td>bool</td><td>false</td></tr><tr><td>onToggle</td><td>VoidCallBack Function</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

***

## Behaviours

|                                                                                                                                          |                                                                                                                                                                                                                                        |
| ---------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (5) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Clickable Navigation</strong></p><p>All breadcrumb items (except the current page) are clickable, enabling users to quickly jump to previous steps or levels in their journey.</p>                                          |
| <div><figure><img src="../../../../../.gitbook/assets/image (6) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Responsive Collapsing</strong></p><p>Breadcrumbs automatically adjust and collapse middle items when the screen width is limited, ensuring the component remains compact and accessible on mobile or smaller viewports.</p> |



***

## Usage Guide

***

| <div><figure><img src="../../../../../.gitbook/assets/image (7) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Use breadcrumbs to show hierarchy</strong></p><p>Maintain a consistent hierarchical structure for breadcrumbs, as they provide users with a clear path for navigation and context about their current location.  </p><p>Use breadcrumbs for anything other than navigating a linear hierarchy. They should not serve as interactive elements for actions like filtering or other functionalities.</p> |
| ---------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (9) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div> |                                                                                                                                                                                                                                                                                                                                                                                                                  |

## Changelog

***

| Date         | Number  | Notes                                                                                           |
| ------------ | ------- | ----------------------------------------------------------------------------------------------- |
| Dec 15, 2024 | v-0.0.2 | <p>This component is added to the website.<br>This component is now individually versioned.</p> |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Content guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
