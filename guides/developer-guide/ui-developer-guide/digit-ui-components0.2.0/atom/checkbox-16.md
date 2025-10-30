---
description: Design System - Toast component
---

# Toast

The Toast component delivers brief, unobtrusive feedback messages to inform users about the result of an action. It is accessible, timely, and clearly distinguishes message types through consistent visual cues and positioning.

<figure><img src="../../../../../.gitbook/assets/image (22) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="Component React" %}
```
// Sample code

 <Toast
    label="Success Toast Message"
    populators={{
      name: 'toast'
    }}
    style={{}}
    transitionTime={600000}
    type="success"
  />
```
{% endtab %}

{% tab title="Component Flutter" %}
```
// Sample code

Toast.showToast(context,
              message: 'This is a toast!',
              type: ToastType.info,
              position: ToastPosition.aboveOneButtonFooter
          );
```
{% endtab %}

{% tab title="Component Design" %}

{% endtab %}
{% endtabs %}

## Anatomy

***

<figure><img src="../../../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure>

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Success</strong></p><p>Indicates a successful or completed action, with a green background and check icon.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Warning</strong></p><p>Alerts users to potential issues that need attention but aren’t critical. Often styled with an amber background.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (8) (1) (1) (1) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Info</strong> </p><p>Provides general information or guidance in blue, without urgency.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (6) (1) (1) (1) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Error</strong> </p><p>Communicates a failure or problem, using red tones to draw immediate attention.</p></td></tr></tbody></table>

## Properties

<table data-header-hidden data-full-width="false"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Input Text</strong><br>Custom message text that conveys the result or information clearly and concisely.<br></td><td><div><figure><img src="../../../../../.gitbook/assets/image (9) (1) (1) (1) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Duration</strong><br>Specifies how long the toast remains visible on the screen, usually in milliseconds.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (10) (1) (1) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure></div></td></tr></tbody></table>

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>label</td><td>text</td><td>-</td></tr><tr><td>onClose</td><td>text</td><td>no</td></tr><tr><td>isDleteBtn</td><td>yes/no</td><td>no</td></tr><tr><td>transitionTime</td><td>yes/no</td><td>-</td></tr><tr><td>type</td><td>number</td><td>-</td></tr><tr><td>style</td><td>yes/no</td><td>-</td></tr><tr><td>labelstyle</td><td>yes/no</td><td>no</td></tr><tr><td>isWarningButtons</td><td>yes/no</td><td>no</td></tr><tr><td>onYes</td><td>yes/no</td><td>no</td></tr><tr><td>onNo</td><td>number</td><td>no</td></tr><tr><td>variant</td><td>yes/no</td><td>no</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>message</td><td>String</td><td>required</td></tr><tr><td>type</td><td>ToastType</td><td>required</td></tr><tr><td>duration</td><td>Duration</td><td>-</td></tr><tr><td>animationDuration</td><td>Duration</td><td>-</td></tr><tr><td>position</td><td>ToastPosition</td><td>-</td></tr><tr><td>customPosition</td><td>StyledToastPosition</td><td>-</td></tr><tr><td>digitToastThemeData</td><td>DigitToastThemeData</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

***

## Behaviours

|                                                                                                                                           |                                                                                                       |
| ----------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (11) (1) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Auto Dismiss</strong></p><p>Toast automatically disappears after the defined duration.</p> |
| <div><figure><img src="../../../../../.gitbook/assets/image (12) (1) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Manual Dismiss</strong></p><p>Users can manually close a toast using the close icon.</p>   |

***

## Usage Guide

***

| <div><figure><img src="../../../../../.gitbook/assets/image (13) (1) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Keep messages brief and time-sensitive</strong></p><p>Use short and actionable text that disappears automatically after 3-5 seconds. Ensure it provides immediate value without interrupting workflow and is horizontally centre-aligned for better visibility..  Never stack multiple toasts; excessive toasts overwhelm users and dilute the importance of urgent notifications.</p> |
| ----------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (14) (1) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure></div> |                                                                                                                                                                                                                                                                                                                                                                                                   |

## Changelog

***

| Date         | Number  | Notes                                                                                           |
| ------------ | ------- | ----------------------------------------------------------------------------------------------- |
| Dec 15, 2024 | v-0.0.2 | <p>This component is added to the website.<br>This component is now individually versioned.</p> |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Content guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
