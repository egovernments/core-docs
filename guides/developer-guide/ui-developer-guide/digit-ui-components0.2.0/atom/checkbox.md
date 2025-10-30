---
description: Design System - Alert card component
---

# Alert Card

The Alert Card component is a visual communication element used to inform users about critical messages like errors, warnings, success confirmations, or informative updates. It ensures users are guided with appropriate visual cues and messaging hierarchy at every touchpoint of their interaction.

<figure><img src="../../../../../.gitbook/assets/image (10) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="Component React" %}
```
// Sample code

<AlertCard
  additionalElements={[
    <p key="1">Additional Element 1</p>,
    <img key="2" alt="Additional Element 2" src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQIGMLufj86aep95KwMzr3U0QShg7oxdAG8gBPJ9ALIFQ&s"/>,
    <img key="3" alt="Additional Element 3" src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQIGMLufj86aep95KwMzr3U0QShg7oxdAG8gBPJ9ALIFQ&s"/>,
    <img key="4" alt="Additional Element 4" src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQIGMLufj86aep95KwMzr3U0QShg7oxdAG8gBPJ9ALIFQ&s"/>,
    <img key="5" alt="Additional Element 5" src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQIGMLufj86aep95KwMzr3U0QShg7oxdAG8gBPJ9ALIFQ&s"/>,
    <img key="6" alt="Additional Element 6" src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQIGMLufj86aep95KwMzr3U0QShg7oxdAG8gBPJ9ALIFQ&s"/>,
    <img key="7" alt="Additional Element 7" src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQIGMLufj86aep95KwMzr3U0QShg7oxdAG8gBPJ9ALIFQ&s"/>,
    <img key="8" alt="Additional Element 8" src="https://digit.org/wp-content/uploads/2023/06/Digit-Logo-1.png"/>,
    <TextArea populators={{resizeSmart: true}} type="textarea"/>,
    <InfoButton label="Button" size="large"/>
  ]}
  label="Info"
  text="Application process will take a minute to complete. It might cost around Rs.500/- to Rs.1000/- to clean your septic tank and you can expect theservice to get completed in 24 hrs from the time of payment."
  variant="default"
/>
```
{% endtab %}

{% tab title="Component Flutter" %}
```
// Sample code

AlertCard(
    title: 'Information',
    description: 'This is an informational card',
    type: InfoType.info,
  )
```
{% endtab %}

{% tab title="Component Design" %}

{% endtab %}
{% endtabs %}

## Anatomy

***

<figure><img src="../../../../../.gitbook/assets/image (11) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (15) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Info</strong></p><p>Used to convey general information or tips that help users proceed smoothly, and uses a neutral blue tone to maintain a calm and non-intrusive presence.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (14) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Error</strong></p><p>Indicates a problem or a failure in the process and is highlighted with red accents to draw immediate attention.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (13) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Success</strong></p><p>Represents successful outcomes or completion of user actions, and green colour signifies affirmation and closure.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (12) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Warning</strong></p><p>Alerts users about potential issues or required attention, and the orange tone ensures visibility without creating an alarm.</p></td></tr></tbody></table>

***

## Properties

|                                                                                                                                                                                                                                                     |                                                                                                                                       |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>Action Button</strong></p><p>Optional call-to-action placed within the alert for quick resolution or follow-up and it is also styled consistently with the alert type.</p>                                                               | <div><figure><img src="../../../../../.gitbook/assets/image (16) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div> |
| <p><strong>Widget Alignment</strong></p><p>Elements like text, icon, buttons, and additional content are aligned using layout grids or auto-layout features as it ensures a structured, clean appearance across device sizes and screen states.</p> | <div><figure><img src="../../../../../.gitbook/assets/image (17) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div> |

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>label</td><td>text</td><td>-</td></tr><tr><td>text</td><td>text</td><td>no</td></tr><tr><td>variant</td><td>yes/no</td><td>no</td></tr><tr><td>style</td><td>yes/no</td><td>-</td></tr><tr><td>textStyle</td><td>number</td><td>-</td></tr><tr><td>additionalElements</td><td>yes/no</td><td>-</td></tr><tr><td>inline</td><td>yes/no</td><td>no</td></tr><tr><td>className</td><td>yes/no</td><td>no</td></tr><tr><td>headerWrapperClassName</td><td>yes/no</td><td>no</td></tr><tr><td>headerClassName</td><td>number</td><td>no</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>title</td><td>String</td><td>required</td></tr><tr><td>description</td><td>String</td><td>required</td></tr><tr><td>type</td><td>Alert Card type</td><td>info</td></tr><tr><td>additionalWidget</td><td>List&#x3C;Widget></td><td>-</td></tr><tr><td>inline</td><td>bool</td><td>false</td></tr><tr><td>infoCardThemeData</td><td>DigitInfoCardThemeData</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

***

## Behaviours

|                                                                                                                                       |                                                                                                                                                                                                              |
| ------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <div><figure><img src="../../../../../.gitbook/assets/image (21) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Flexible Layout</strong></p><p>Designed to adapt within cards, modals, or full-width views, and it is also responsive to container size and works well in both desktop and mobile interfaces.</p> |

***

## Usage Guide

***

| <p></p><div><figure><img src="../../../../../.gitbook/assets/image (19) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Use Alert Cards to provide clear feedback</strong></p><p>Use alert cards to provide clear and concise feedback about important system statuses, warnings, or errors. Ensure the message is direct and informative so users can take appropriate action quickly.  Avoid using alert cards for non-critical information or minor updates. Overusing them for trivial messages can cause users to ignore them, reducing their effectiveness in important situations.</p> |
| -------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p></p><div><figure><img src="../../../../../.gitbook/assets/image (20) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div> |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |

## Changelog

***

| Date         | Number  | Notes                                                                                           |
| ------------ | ------- | ----------------------------------------------------------------------------------------------- |
| Dec 15, 2024 | v-0.0.2 | <p>This component is added to the website.<br>This component is now individually versioned.</p> |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Content guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
