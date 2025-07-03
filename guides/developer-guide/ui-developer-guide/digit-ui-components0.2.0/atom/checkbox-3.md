---
description: Design System - Stepper component
---

# Dropdown - Single Select

The Dropdown - Single Select lets users pick one option from a predefined list. It is ideal for forms and filters where only one choice is valid, offering a compact and user-friendly way to streamline selections.

<figure><img src="../../../../../.gitbook/assets/image (370).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../../../../.gitbook/assets/image (371).png" alt=""><figcaption></figcaption></figure>

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><img src="../../../../../.gitbook/assets/image (373).png" alt=""></td><td><p><strong>Horizontal Stepper</strong></p><p>Displays steps in a single row, guiding users through a linear process from left to right. Ideal for checkouts, onboarding, and multi-step forms with clear progress indicators.</p></td></tr><tr><td><img src="../../../../../.gitbook/assets/image (372).png" alt=""></td><td><strong>Vertical Stepper</strong><br>The Vertical Stepper displays steps in a column, ideal for mobile screens or detailed content. It improves readability and offers clear top-to-bottom navigation, making it great for forms or lengthy descriptions.</td></tr></tbody></table>

## Properties

<table data-header-hidden data-full-width="false"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Divider</strong><br>Determines whether a visual separator (divider) is displayed between steps. Helps in distinguishing each step clearly.<br></td><td><div><figure><img src="../../../../../.gitbook/assets/image (379).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Number of Steps</strong><br>Defines the total steps in the stepper. Helps in setting the length of the process.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (380).png" alt=""><figcaption></figcaption></figure></div></td></tr></tbody></table>

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>currentStep</td><td>text</td><td>-</td></tr><tr><td>onStepClick</td><td>text</td><td>no</td></tr><tr><td>totalSteps</td><td>yes/no</td><td>no</td></tr><tr><td>customSteps</td><td>yes/no</td><td>-</td></tr><tr><td>direction</td><td>number</td><td>-</td></tr><tr><td>style</td><td>yes/no</td><td>-</td></tr><tr><td>className</td><td>yes/no</td><td>no</td></tr><tr><td>activeSteps</td><td>yes/no</td><td>no</td></tr><tr><td>hideDivider</td><td>yes/no</td><td>no</td></tr><tr><td>props</td><td>number</td><td>no</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>Title</td><td>String</td><td>required(if header is not passed)</td></tr><tr><td>Number</td><td>double</td><td>-</td></tr><tr><td>Icon</td><td>Icon widget</td><td>-</td></tr><tr><td>header</td><td>Widget</td><td>-</td></tr><tr><td>content</td><td>Widget</td><td>required</td></tr><tr><td>divider</td><td>bool</td><td>false</td></tr><tr><td>initiallyExpanded</td><td>bool</td><td>false</td></tr><tr><td>showBorder</td><td>bool</td><td>false</td></tr><tr><td>onToggle</td><td>VoidCallBack Function</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

## Interaction State

***

<table data-header-hidden data-full-width="false"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Active State</strong><br>The current step is visually highlighted to indicate progress.<br></td><td><div><figure><img src="../../../../../.gitbook/assets/image (375).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Completed State</strong><br>Steps that users have finished are marked as completed, often with a checkmark or different styling.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (376).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Hover State</strong><br>On hover, inactive steps highlight to indicate they are clickable and part of the navigation flow.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (377).png" alt=""><figcaption></figcaption></figure></div></td></tr></tbody></table>

## Behaviours

|                                                                                                                        |                                                                                                                                                                                                                                                           |
| ---------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (381).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Horizontal Scrolling</strong></p><p>When using a horizontal stepper in a narrow container, steps can scroll sideways to accommodate all steps within view.</p>                                                                                 |
| <div><figure><img src="../../../../../.gitbook/assets/image (382).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Vertical Scrolling</strong></p><p>In vertical layouts with limited height, steps scroll vertically to ensure users can access each step sequentially without content being cut off.</p>                                                        |
| <div><figure><img src="../../../../../.gitbook/assets/image (383).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Label Overflow</strong></p><p>If step labels exceed the available space, they are truncated with ellipsis (...) or wrapped to the next line based on layout and design requirements. Tooltips can be used to show the full label on hover.</p> |
| <div><figure><img src="../../../../../.gitbook/assets/image (384).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Flexible Dimensions</strong></p><p>Steppers adapt to custom width and height defined by their parent containers using flex layouts. They maintain usability and alignment across different screen sizes and orientations.</p>                  |

***

## Usage Guide

***

| <div><figure><img src="../../../../../.gitbook/assets/image (386).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Use for a process that involves multiple steps</strong></p><p>Use a stepper only when a process involves multiple steps, ensuring clear progression and user guidance.</p> |
| ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (385).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Avoid using it for just one or two steps</strong></p><p>Avoid using a stepper for processes with just one or two steps, as it adds unnecessary complexity.</p>             |

## Changelog

***

| Date         | Number  | Notes                                                                                           |
| ------------ | ------- | ----------------------------------------------------------------------------------------------- |
| Dec 15, 2024 | v-0.0.2 | <p>This component is added to the website.<br>This component is now individually versioned.</p> |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Content guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
