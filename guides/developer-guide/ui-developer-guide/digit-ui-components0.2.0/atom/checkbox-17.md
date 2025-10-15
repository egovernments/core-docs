---
description: Design System - Callout component
---

# Callout

The Callout component is a contextual overlay that guides users through tasks, highlights features, or delivers important information. Callouts help users navigate complex flows by offering step-by-step cues or informative prompts in a visually distinct yet non-intrusive manner.

<figure><img src="../../../../../.gitbook/assets/image (25) (1).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../../../../.gitbook/assets/image (26) (1).png" alt=""><figcaption></figcaption></figure>

***

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (27) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Default</strong></p><p>The default Callout features a concise message, supportive action buttons, and is commonly used in walkthroughs, onboarding flows, or form guidance.</p></td></tr></tbody></table>

***

## Properties

|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>Arrows with various positionings</strong></p><p>The arrow is a key visual indicator that links the Callout to the UI element it refers to.<br>Supported placements include:</p><ul><li>Bottom Left / Bottom Centre / Bottom Right</li><li>Left Centre / Right Centre</li><li>Top Left / Top Centre / Top Right</li></ul><p>This flexibility ensures the Callout can adapt to various layouts and screen constraints while maintaining a clear association with the target element.</p> | <div><figure><img src="../../../../../.gitbook/assets/image (28) (1).png" alt=""><figcaption></figcaption></figure></div> |

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>label</td><td>text</td><td></td></tr><tr><td>onChange</td><td>text</td><td></td></tr><tr><td>value</td><td>yes/no</td><td>no</td></tr><tr><td>disabled</td><td>yes/no</td><td>no</td></tr><tr><td>ref</td><td>number</td><td></td></tr><tr><td>checked</td><td>yes/no</td><td></td></tr><tr><td>inputRef</td><td>yes/no</td><td>no</td></tr><tr><td>pageType</td><td>yes/no</td><td>no</td></tr><tr><td>style</td><td>yes/no</td><td>no</td></tr><tr><td>index</td><td>number</td><td>no</td></tr><tr><td>isLabelFirst</td><td>yes/no</td><td>no</td></tr><tr><td>customLabelMarkup</td><td>text</td><td>no</td></tr><tr><td>hideLabel</td><td>yes/no</td><td>no</td></tr><tr><td>isIntermediate</td><td>yes/no</td><td></td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>Title</td><td>String</td><td>required(if header is not passed)</td></tr><tr><td>Number</td><td>double</td><td>-</td></tr><tr><td>Icon</td><td>Icon widget</td><td>-</td></tr><tr><td>header</td><td>Widget</td><td>-</td></tr><tr><td>content</td><td>Widget</td><td>required</td></tr><tr><td>divider</td><td>bool</td><td>false</td></tr><tr><td>initiallyExpanded</td><td>bool</td><td>false</td></tr><tr><td>showBorder</td><td>bool</td><td>false</td></tr><tr><td>onToggle</td><td>VoidCallBack Function</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

***

## Behaviours

|                                                                                                                           |                                                                                                                                                                                                             |
| ------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (29) (2).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Step-based navigation</strong></p><p>Users can navigate through multi-step messages using the Next, Previous, or Skip buttons, which also support the progressive disclosure of information.</p> |

***

## Usage Guide

***

| <div><figure><img src="../../../../../.gitbook/assets/image (30) (2).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Use for exclusive choices</strong></p><p>Use callouts to highlight new features, changes, or temporary announcements that require immediate user attention. This helps users stay informed about important updates while maintaining their current workflow.</p><p>Don't use callouts for permanent content that is part of the regular interface, as this reduces the impact of truly important announcements and creates unnecessary visual noise.</p> |
| ------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (31) (2).png" alt=""><figcaption></figcaption></figure></div> |                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

## Changelog

***

| Date         | Number  | Notes                                                                                           |
| ------------ | ------- | ----------------------------------------------------------------------------------------------- |
| Dec 15, 2024 | v-0.0.2 | <p>This component is added to the website.<br>This component is now individually versioned.</p> |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Writing guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
