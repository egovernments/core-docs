---
description: Design System - Timeline component
---

# Timeline

The Timeline component visually represents a sequence of events or stages in a linear, chronological order. Designed with clarity and accessibility in mind, it helps users understand the progress, status, and associated actions within a workflow.

<figure><img src="../../../../../.gitbook/assets/image (476).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../../../../.gitbook/assets/image (477).png" alt=""><figcaption></figcaption></figure>

***

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (478).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Upcoming</strong></p><p>Displays future events or steps in the process. The visual indicator is muted to reflect inactivity, and it can include relevant date/time info.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (479).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>In Progress</strong></p><p>Represents tasks or stages currently underway. It uses an active visual indicator to denote ongoing status and may include interactive elements like “View Details”.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (480).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Completed</strong></p><p>Marks finished tasks using a filled, completed icon. This variant reinforces a sense of progression and task completion.</p></td></tr></tbody></table>

***

## Properties

|                                                                                                                                                                                              |                                                                                                                        |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| <p><strong>Default</strong></p><p>Shows only the stage name without additional data, keeping the interface clean.</p>                                                                        | <div><figure><img src="../../../../../.gitbook/assets/image (481).png" alt=""><figcaption></figcaption></figure></div> |
| <p><strong>Date</strong></p><p>Includes the date beneath the stage to inform users of timing for events or steps.</p>                                                                        | <div><figure><img src="../../../../../.gitbook/assets/image (482).png" alt=""><figcaption></figcaption></figure></div> |
| <p><strong>Additional Elements</strong></p><p>Enhances the component with date/time details and a collapsible “View Details” element, which opens further content.</p>                       | <div><figure><img src="../../../../../.gitbook/assets/image (483).png" alt=""><figcaption></figcaption></figure></div> |
| <p><strong>Expanded</strong></p><p>Displays rich content such as text blocks, image/document previews, and action buttons to support user interaction.</p>                                   | <div><figure><img src="../../../../../.gitbook/assets/image (485).png" alt=""><figcaption></figcaption></figure></div> |
| <p><strong>Error Timeline</strong></p><p>Highlights failed or incomplete steps with red indicators and messaging like “Failed”, drawing attention to issues that require user attention.</p> | <div><figure><img src="../../../../../.gitbook/assets/image (486).png" alt=""><figcaption></figcaption></figure></div> |

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>label</td><td>text</td><td></td></tr><tr><td>subElements</td><td>text</td><td></td></tr><tr><td>variant</td><td>yes/no</td><td>no</td></tr><tr><td>viewDetailsLabel</td><td>yes/no</td><td>no</td></tr><tr><td>hideDetailsLabel</td><td>number</td><td></td></tr><tr><td>additionalElements</td><td>yes/no</td><td></td></tr><tr><td>inline</td><td>yes/no</td><td>no</td></tr><tr><td>individualElementStyles</td><td>yes/no</td><td>no</td></tr><tr><td>showConnector</td><td>yes/no</td><td>no</td></tr><tr><td>className</td><td>number</td><td>no</td></tr><tr><td>isLabelFirst</td><td>yes/no</td><td>no</td></tr><tr><td>isNextActiveStep</td><td>text</td><td>no</td></tr><tr><td>showDefaultValueForDate</td><td>yes/no</td><td>no</td></tr><tr><td>isError</td><td>yes/no</td><td></td></tr><tr><td>initialVisibleAdditionalElementsCount</td><td>yes/no</td><td></td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>Title</td><td>String</td><td>required(if header is not passed)</td></tr><tr><td>Number</td><td>double</td><td>-</td></tr><tr><td>Icon</td><td>Icon widget</td><td>-</td></tr><tr><td>header</td><td>Widget</td><td>-</td></tr><tr><td>content</td><td>Widget</td><td>required</td></tr><tr><td>divider</td><td>bool</td><td>false</td></tr><tr><td>initiallyExpanded</td><td>bool</td><td>false</td></tr><tr><td>showBorder</td><td>bool</td><td>false</td></tr><tr><td>onToggle</td><td>VoidCallBack Function</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

***

## Behaviours

|                                                                                                                        |                                                                                                                                                                                            |
| ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <div><figure><img src="../../../../../.gitbook/assets/image (487).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Progressive Expansion</strong></p><p>Sections expand to reveal additional information, files, and actions only when the user chooses to explore, preventing visual clutter.</p> |

***

## Usage Guide

***

| <p><strong>Ensure Clear Status Representation</strong></p><p>Each timeline status should be visually distinct using clear colours, icons, and typography so that users can easily understand the progression and current state.</p><p></p><p>Icons should clearly match their status. Avoid using similar icons for different statuses, which can lead to misinterpretation.</p> | <div><figure><img src="../../../../../.gitbook/assets/image (488).png" alt=""><figcaption></figcaption></figure></div> |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
|                                                                                                                                                                                                                                                                                                                                                                                  | <div><figure><img src="../../../../../.gitbook/assets/image (489).png" alt=""><figcaption></figcaption></figure></div> |

## Changelog

***

| Date         | Number  | Notes                                                                                           |
| ------------ | ------- | ----------------------------------------------------------------------------------------------- |
| Dec 15, 2024 | v-0.0.2 | <p>This component is added to the website.<br>This component is now individually versioned.</p> |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Writing guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
