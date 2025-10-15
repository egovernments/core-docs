---
description: Design System - Tabs component
---

# Tabs

Tabs are used to organise content into meaningful sections within the same view. They help reduce cognitive overload by presenting information progressively.

<figure><img src="../../../../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../../../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

***

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Default</strong></p><p>The Basic tab variant presents a straightforward horizontal layout of labelled tabs. It is ideal for dividing related content within the same page or module, allowing users to switch between sections without navigating away.</p></td></tr></tbody></table>

***

## Interaction States

<table><thead><tr><th width="334.98046875"></th><th></th></tr></thead><tbody><tr><td><p><strong>Active</strong></p><p>The active tab is highlighted with a bold label and a strong border to visually indicate selection. It improves user orientation by showing which section is currently visible.</p></td><td><div><figure><img src="../../../../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure></div></td></tr></tbody></table>

## Properties

|                                                                                                                               |                                                                                                                          |
| ----------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| <p><strong>Label</strong></p><p>Each tab is defined by a clearly readable label that communicates its purpose</p>             | <div><figure><img src="../../../../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure></div> |
| <p><strong>With Icon</strong></p><p>Useful for visual reinforcement, especially in data-heavy or mobile-first interfaces.</p> | <div><figure><img src="../../../../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure></div> |
| <p><strong>Without Icon</strong></p><p>A cleaner variant that emphasises text.</p>                                            | <div><figure><img src="../../../../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure></div> |

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>configNavItems</td><td>text</td><td></td></tr><tr><td>configItemKey</td><td>text</td><td></td></tr><tr><td>activeLink</td><td>yes/no</td><td>no</td></tr><tr><td>setActiveLink</td><td>yes/no</td><td>no</td></tr><tr><td>showNav</td><td>number</td><td></td></tr><tr><td>style</td><td>yes/no</td><td></td></tr><tr><td>navStyles</td><td>yes/no</td><td>no</td></tr><tr><td>itemStyle</td><td>yes/no</td><td>no</td></tr><tr><td>className</td><td>yes/no</td><td>no</td></tr><tr><td>navClassName</td><td>number</td><td>no</td></tr><tr><td>onTabClick</td><td>yes/no</td><td>no</td></tr><tr><td>children</td><td>text</td><td>no</td></tr><tr><td>configDisplayKey</td><td>yes/no</td><td>no</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>Title</td><td>String</td><td>required(if header is not passed)</td></tr><tr><td>Number</td><td>double</td><td>-</td></tr><tr><td>Icon</td><td>Icon widget</td><td>-</td></tr><tr><td>header</td><td>Widget</td><td>-</td></tr><tr><td>content</td><td>Widget</td><td>required</td></tr><tr><td>divider</td><td>bool</td><td>false</td></tr><tr><td>initiallyExpanded</td><td>bool</td><td>false</td></tr><tr><td>showBorder</td><td>bool</td><td>false</td></tr><tr><td>onToggle</td><td>VoidCallBack Function</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

***

## Behaviours

|                                                                                                                          |                                                                                                                                                                                                  |
| ------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <div><figure><img src="../../../../../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Responsive Layout</strong></p><p>Tabs automatically adjust their width and layout based on the number of items and screen size to ensure optimal usability across devices.</p>        |
| <div><figure><img src="../../../../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Instant Content Update</strong></p><p>When switching between tabs, the corresponding content updates instantly without needing to reload the page, enhancing the user experience.</p> |

***

## Usage Guide

***

| <p><strong>Highlight the active tab clearly</strong></p><p>Ensure the active tab stands out from inactive ones. This can be done through bold text, colour changes, and a border to help users easily identify which section is currently selected. A well-defined active tab enhances navigation clarity and improves the user experience.  </p><p></p><p>Don’t mix the use of icons in tabs. Consistent icon usage maintains clear spatial relationships and visual balance, ensuring a cohesive navigation experience.</p> | <div><figure><img src="../../../../../.gitbook/assets/image (9) (1).png" alt=""><figcaption></figcaption></figure></div> |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | <div><figure><img src="../../../../../.gitbook/assets/image (490).png" alt=""><figcaption></figcaption></figure></div>   |

## Changelog

***

| Date         | Number  | Notes                                                                                           |
| ------------ | ------- | ----------------------------------------------------------------------------------------------- |
| Dec 15, 2024 | v-0.0.2 | <p>This component is added to the website.<br>This component is now individually versioned.</p> |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Writing guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
