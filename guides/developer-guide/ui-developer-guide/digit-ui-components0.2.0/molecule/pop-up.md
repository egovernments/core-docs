---
description: Design System - Pop Up component
---

# Pop Ups

The Popups Card component is a focused, interruptive component used to convey critical information or require immediate user interaction. It follows DIGIT’s principles of accessibility, responsiveness, and contextual clarity to ensure that users are guided without ambiguity and can take informed action without navigating away from their current flow.

<figure><img src="../../../../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="Component React" %}
```
// Sample code

<PopUp
  alertHeading=""
  alertMessage=""
  className=""
  customIcon=""
  description="Please contact the administrator if you have forgotten your password."
  equalWidthButtons
  footerChildren={[
    <Button label="Cancel" onClick={() => {}} type="button"/>,
    <Button icon="FileDownload" label="Download Template" onClick={function noRefCheck() {}} type="submit"/>
  ]}
  footerStyles={{}}
  footerclassName=""
  headerMaxLength=""
  headerclassName=""
  heading="Heading"
  iconFill=""
  maxFooterButtonsAllowed={5}
  onClose={function noRefCheck() {}}
  onOverlayClick={function noRefCheck() {}}
  overlayClassName=""
  props={{}}
  showIcon
  sortFooterButtons
  style={{}}
  subHeaderMaxLength=""
  subheading="Subheading"
  type="default"
>
  <div>
    This is the content of the Popup
  </div>
  <AlertCard
    className="popup-alert-card"
    text="This is an alert card"
  />
</PopUp>
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

<figure><img src="../../../../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Default</strong></p><p>Displays informative messages or prompts for user actions with optional titles, descriptions, and buttons.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure></div></td><td><strong>Alert</strong><br>Used to communicate critical errors or system-level alerts, typically styled in red with an alert icon to grab attention.</td></tr></tbody></table>

## Properties

<table data-header-hidden data-full-width="false"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><p><strong>Icon for heading</strong></p><p>Both variants support contextual icons next to headings, such as info or warning icons, to enhance clarity and visual hierarchy.<br></p></td><td><div><figure><img src="../../../../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Descriptions</strong><br>A paragraph below the heading provides additional details or instructions for the user.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Action buttons</strong><br>Configurable with either a single primary button or both primary and secondary actions, allowing flexible interaction.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Custom height &#x26; width</strong><br>The component adapts to mobile, tablet, and desktop screen sizes, with scalable height and width to maintain visual balance and usability, adjusting the button's height and font size.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure></div></td></tr></tbody></table>

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>className</td><td>text</td><td>-</td></tr><tr><td>style</td><td>text</td><td>-</td></tr><tr><td>children</td><td>yes/no</td><td>no</td></tr><tr><td>headerclassName</td><td>yes/no</td><td>no</td></tr><tr><td>footerclassName</td><td>number</td><td>-</td></tr><tr><td>footerStyles</td><td>yes/no</td><td>-</td></tr><tr><td>footerChildren</td><td>yes/no</td><td>no</td></tr><tr><td>maxFooterButtonsAllowed</td><td>yes/no</td><td>no</td></tr><tr><td>sortFooterButtons</td><td>yes/no</td><td>no</td></tr><tr><td>equalWidthButtons</td><td>number</td><td>no</td></tr><tr><td>onClose</td><td>yes/no</td><td>no</td></tr><tr><td>onOverlayClick</td><td>yes/no</td><td>no</td></tr><tr><td>type</td><td>yes/no</td><td>no</td></tr><tr><td>showIcon</td><td>yes/no</td><td>no</td></tr><tr><td>customIcon</td><td>yes/no</td><td>no</td></tr><tr><td>iconFill</td><td>yes/no</td><td>no</td></tr><tr><td>heading</td><td>yes/no</td><td>no</td></tr><tr><td>subheading</td><td>yes/no</td><td>no</td></tr><tr><td>headerMaxLength</td><td>yes/no</td><td>no</td></tr><tr><td>subHeaderMaxLength</td><td>yes/no</td><td>no</td></tr><tr><td>description</td><td>yes/no</td><td>no</td></tr><tr><td>showChildrenInline</td><td>yes/no</td><td>no</td></tr><tr><td>overlayClassName</td><td>yes/no</td><td>no</td></tr><tr><td>alertHeading</td><td>yes/no</td><td>no</td></tr><tr><td>alertMessage</td><td>yes/no</td><td>no</td></tr><tr><td>showAlertAsSvg</td><td>yes/no</td><td>no</td></tr><tr><td>showIcon</td><td>yes/no</td><td>no</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>Title</td><td>String</td><td>required(if header is not passed)</td></tr><tr><td>Number</td><td>double</td><td>-</td></tr><tr><td>Icon</td><td>Icon widget</td><td>-</td></tr><tr><td>header</td><td>Widget</td><td>-</td></tr><tr><td>content</td><td>Widget</td><td>required</td></tr><tr><td>divider</td><td>bool</td><td>false</td></tr><tr><td>initiallyExpanded</td><td>bool</td><td>false</td></tr><tr><td>showBorder</td><td>bool</td><td>false</td></tr><tr><td>onToggle</td><td>VoidCallBack Function</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

## Usage Guide

***

| <div><figure><img src="../../../../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Prioritise user actions</strong></p><p>Use a clear call-to-action like “Continue” or “Submit” as the primary button, and pair it with a secondary option like “Cancel” when applicable.  Don’t overload the pop-up with too many buttons or unclear labels that can confuse the user.</p> |
| --------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure></div> |                                                                                                                                                                                                                                                                                                      |

## Change log

***

| Date         | Number  | Notes                                                                                           |
| ------------ | ------- | ----------------------------------------------------------------------------------------------- |
| Dec 15, 2024 | v-0.0.2 | <p>This component is added to the website.<br>This component is now individually versioned.</p> |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Content guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
