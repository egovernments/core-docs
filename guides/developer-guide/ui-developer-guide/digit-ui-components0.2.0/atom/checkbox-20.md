---
description: Design System - Tags component
---

# Tags

Tags are compact elements used to represent status, categorise content, or highlight metadata. Tags deliver quick visual cues without disrupting the user experience. They are lightweight, informative, and scalable for various use cases across web and mobile interfaces.

<figure><img src="../../../../../.gitbook/assets/image (32) (2).png" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="Component React" %}
```
// Sample code

<Tag
  icon=""
  label="Tag With icon & stroke"
  labelStyle={{}}
  stroke
  style={{}}
  type="success"
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

<figure><img src="../../../../../.gitbook/assets/image (33) (2).png" alt=""><figcaption></figcaption></figure>

***

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (24) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Default</strong></p><p>Neutral in appearance, the Default tag is used for generic labelling without implying any state or action.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Success</strong></p><p>Represents positive states such as completion, confirmation, or availability. Shown in green.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (4) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Error</strong></p><p>Indicates issues, failures, or blocked statuses. Visually emphasised with red to alert users.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (3) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Warning</strong></p><p>Used to caution users about potentially risky or incomplete actions. Typically styled in amber or yellow.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Custom</strong></p><p>Allows the use of personalized icons and color schemes for specialized use cases that fall outside standard categories.</p></td></tr></tbody></table>

***

## Interaction States

<table><thead><tr><th width="334.98046875"></th><th></th></tr></thead><tbody><tr><td><p><strong>Hover State</strong> </p><p>On hover, tags visually respond with Slight elevation or shadow. This state helps communicate affordance and improves overall interactivity, especially in filter chips or action tags.</p></td><td><div><figure><img src="../../../../../.gitbook/assets/image (5) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td></tr></tbody></table>

## Properties

|                                                                                                                                                                                                                |                                                                                                                                  |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>Icon</strong></p><p>Tags can include a leading icon to visually reinforce the tag’s context, improving scannability and recognition. Icons change based on tag type.</p>                            | <div><figure><img src="../../../../../.gitbook/assets/image (6) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div> |
| <p><strong>Stroke</strong></p><p>Tags may have a stroked border for emphasis or differentiation. Stroke enhances visual hierarchy without adding bulk, especially useful in outlined or minimal UI themes.</p> | <div><figure><img src="../../../../../.gitbook/assets/image (7) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div> |

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>className</td><td>text</td><td></td></tr><tr><td>iconClassName</td><td>text</td><td></td></tr><tr><td>iconColor</td><td>yes/no</td><td>no</td></tr><tr><td>label</td><td>yes/no</td><td>no</td></tr><tr><td>style</td><td>number</td><td></td></tr><tr><td>stroke</td><td>yes/no</td><td></td></tr><tr><td>type</td><td>yes/no</td><td>no</td></tr><tr><td>showIcon</td><td>yes/no</td><td>no</td></tr><tr><td>labelStyle</td><td>yes/no</td><td>no</td></tr><tr><td>onClick</td><td>number</td><td>no</td></tr><tr><td>alignment</td><td>yes/no</td><td>no</td></tr><tr><td>icon</td><td>text</td><td>no</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>Title</td><td>String</td><td>required(if header is not passed)</td></tr><tr><td>Number</td><td>double</td><td>-</td></tr><tr><td>Icon</td><td>Icon widget</td><td>-</td></tr><tr><td>header</td><td>Widget</td><td>-</td></tr><tr><td>content</td><td>Widget</td><td>required</td></tr><tr><td>divider</td><td>bool</td><td>false</td></tr><tr><td>initiallyExpanded</td><td>bool</td><td>false</td></tr><tr><td>showBorder</td><td>bool</td><td>false</td></tr><tr><td>onToggle</td><td>VoidCallBack Function</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

***

## Behaviours

|                                                                                                                                  |                                                                                                                                                         |
| -------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (8) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Responsiveness</strong></p><p>Tags adapt to different screen sizes, containers, and content lengths without breaking layout consistency.</p> |

***

## Usage Guide

***

| <div><figure><img src="../../../../../.gitbook/assets/image (9) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div>  | <p><strong>Use tags to highlight important</strong></p><p>Use tags to highlight important labels that help users quickly identify key information at a glance. Tags should be concise yet meaningful, making it easier for users to navigate and understand context.</p><p></p><p>Avoid using long or complex tags. Tags should be short, clear, and to the point so users can quickly understand their meaning at a glance.</p> |
| --------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (10) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div> |                                                                                                                                                                                                                                                                                                                                                                                                                                  |

## Changelog

***

| Date         | Number  | Notes                                                                                           |
| ------------ | ------- | ----------------------------------------------------------------------------------------------- |
| Dec 15, 2024 | v-0.0.2 | <p>This component is added to the website.<br>This component is now individually versioned.</p> |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Writing guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
