---
description: Design System - OTP input component
---

# OTP Input

The OTP Input component is designed to collect secure, time-sensitive verification codes from users in a clear and accessible way. It emphasises clarity, accuracy, and ease of use across different devices, ensuring a smooth authentication process.

<figure><img src="../../../../../.gitbook/assets/image (15) (1) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="Component React" %}
```
// Sample code

const Component = () => {
const [otp, setOtp] = useState("");

//Example onChange logic
const handleOtpChange = (value) => {
setOtp(value);
if (value.length === args.length) {
const isValid = value.includes(1);
if (isValid) {
console.log("OTP is correct");
return null;
} else {
console.log("Invalid OTP");
return "Invalid OTP";
}
}
return null;
};
return <OTPInput length={6} type="numeric" onChange={handleOtpChange} placeholder={"123456"} label="Enter OTP" inline={false} className="" style={{ }} />;
};
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

<figure><img src="../../../../../.gitbook/assets/image (16) (1) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure>

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (17) (1) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>4-characters</strong></p><p>Used when the OTP is limited to four digits, offering a compact layout ideal for simpler authentication flows.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (18) (1) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>6-characters</strong></p><p>Common in more secure flows, this variant provides six input boxes for enhanced verification.</p></td></tr></tbody></table>

## Properties

<table data-header-hidden data-full-width="false"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Label</strong><br>Positioned above the input fields (e.g., "Enter OTP"), it provides clear instructions to the user.<br></td><td><div><figure><img src="../../../../../.gitbook/assets/image (23) (1) (1) (2).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Error</strong><br>Displays an error message (e.g., “Invalid OTP”) with a red border and icon to indicate incorrect input.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (22) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><p><strong>Masking</strong></p><p>Optionally replaces typed characters with dots (●) for added security, particularly useful in shared or public environments.</p></td><td><div><figure><img src="../../../../../.gitbook/assets/image (21) (1) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td></td><td></td></tr></tbody></table>

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>length</td><td>text</td><td>-</td></tr><tr><td>type</td><td>text</td><td>no</td></tr><tr><td>onChange</td><td>yes/no</td><td>no</td></tr><tr><td>placeholder</td><td>yes/no</td><td>-</td></tr><tr><td>className</td><td>number</td><td>-</td></tr><tr><td>style</td><td>yes/no</td><td>-</td></tr><tr><td>label</td><td>yes/no</td><td>no</td></tr><tr><td>inline</td><td>yes/no</td><td>no</td></tr><tr><td>masking</td><td>yes/no</td><td>no</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>Title</td><td>String</td><td>required(if header is not passed)</td></tr><tr><td>Number</td><td>double</td><td>-</td></tr><tr><td>Icon</td><td>Icon widget</td><td>-</td></tr><tr><td>header</td><td>Widget</td><td>-</td></tr><tr><td>content</td><td>Widget</td><td>required</td></tr><tr><td>divider</td><td>bool</td><td>false</td></tr><tr><td>initiallyExpanded</td><td>bool</td><td>false</td></tr><tr><td>showBorder</td><td>bool</td><td>false</td></tr><tr><td>onToggle</td><td>VoidCallBack Function</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

## Interaction State

***

<table data-header-hidden data-full-width="false"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Single Focus</strong><br>In Single Focus mode, only one input box is actively focused at a time. As the user types, the focus automatically moves to the next box, improving usability and reducing the need for manual navigation between fields.<br></td><td><div><figure><img src="../../../../../.gitbook/assets/image (20) (1) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure></div></td></tr></tbody></table>

## Behaviours

|                                                                                                                                   |                                                                                                                                                        |
| --------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <div><figure><img src="../../../../../.gitbook/assets/image (26) (1) (2).png" alt=""><figcaption></figcaption></figure></div>     | <p><strong>Auto Tabbing</strong></p><p>The cursor automatically jumps to the next field as each digit is entered.</p>                                  |
| <div><figure><img src="../../../../../.gitbook/assets/image (25) (1) (2).png" alt=""><figcaption></figcaption></figure></div>     | <p><strong>Backspace Navigation</strong></p><p>Pressing backspace in an empty field moves the focus to the previous box, allowing easy correction.</p> |
| <div><figure><img src="../../../../../.gitbook/assets/image (24) (1) (1) (2).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Paste Handling</strong></p><p>Supports pasting a full OTP string, automatically distributing characters across input fields.</p>            |



***

## Usage Guide

***

| <div><figure><img src="../../../../../.gitbook/assets/image (27) (1) (2).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Use Clear Focus State for Better User Guidance</strong></p><p>Ensure that the currently active OTP input field is visually distinct so users can immediately recognise where they need to type next. A proper focus state improves accessibility and enhances the user experience by providing clear feedback on input interactions.  Users should not struggle to identify which input box is currently active. Lack of clear focus indication can result in hesitation or mistakes, causing frustration.</p> |
| ----------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (28) (1) (2).png" alt=""><figcaption></figcaption></figure></div> |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |

## Changelog

***

| Date         | Number  | Notes                                                                                           |
| ------------ | ------- | ----------------------------------------------------------------------------------------------- |
| Dec 15, 2024 | v-0.0.2 | <p>This component is added to the website.<br>This component is now individually versioned.</p> |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Content guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
