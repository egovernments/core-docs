---
description: Design System - Divider component
---

# Divider

The Divider component is a minimal visual element used to create a clear separation between content blocks, sections, or UI elements. Designed with simplicity and clarity in mind, dividers help maintain a clean layout structure, enhance visual hierarchy, and improve content readability without drawing unnecessary attention.

<figure><img src="../../../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../../../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Small</strong></p><p>The Small variant is the most minimal, offering a subtle line ideal for closely related content or where minimal visual interruption is needed.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Medium</strong></p><p>The Medium variant provides a slightly more prominent separation and is commonly used between groups of information or components within a section.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Large</strong></p><p>The Large variant offers the strongest emphasis, ideal for separating major sections or modules, especially in dense interfaces or dashboards.</p></td></tr></tbody></table>

***

## Properties

|                                                                                                                                                                                                                               |                                                                                                                          |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| <p><strong>With Icon</strong></p><p>An optional icon can be added to the left or right (dismiss/close icon). This enhances usability and improves scanability, especially for chips used in status indicators or filters.</p> | <div><figure><img src="../../../../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure></div> |

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>className</td><td>text</td><td>no</td></tr><tr><td>style</td><td>yes/no</td><td>no</td></tr><tr><td>variant</td><td>yes/no</td><td>-</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>Title</td><td>String</td><td>required(if header is not passed)</td></tr><tr><td>Number</td><td>double</td><td>-</td></tr><tr><td>Icon</td><td>Icon widget</td><td>-</td></tr><tr><td>header</td><td>Widget</td><td>-</td></tr><tr><td>content</td><td>Widget</td><td>required</td></tr><tr><td>divider</td><td>bool</td><td>false</td></tr><tr><td>initiallyExpanded</td><td>bool</td><td>false</td></tr><tr><td>showBorder</td><td>bool</td><td>false</td></tr><tr><td>onToggle</td><td>VoidCallBack Function</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

***

## Behaviours

|                                                                                                                      |                                                                                                                                                                                   |
| -------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Responsiveness</strong></p><p>Dividers adapt fluidly to their container width and scale across screen sizes while preserving consistency in thickness and spacing.</p> |

***

## Usage Guide

***

| <div><figure><img src="../../../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Use Dividers with Headers for Clear Sectioning</strong></p><p>Place dividers below the header text to create distinct sections or page titles. This helps organise content and improves visual hierarchy.  </p><p>Avoid using dividers excessively, as they can create unnecessary visual noise and clutter. Use them sparingly to maintain a clean and focused layout</p> |
| -------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure></div> |                                                                                                                                                                                                                                                                                                                                                                                       |

## Changelog

***

| Date         | Number  | Notes                                                                                           |
| ------------ | ------- | ----------------------------------------------------------------------------------------------- |
| Dec 15, 2024 | v-0.0.2 | <p>This component is added to the website.<br>This component is now individually versioned.</p> |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Content guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
