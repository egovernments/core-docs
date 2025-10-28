---
description: Design System - Panel Card component
---

# Panel Card

The Panel Card component is a composite component designed to communicate clear, high-visibility feedback messages, typically success or error outcomes. It brings together an icon, message, optional description, interactive actions, and optional widgets into one cohesive layout.

<figure><img src="../../../../../.gitbook/assets/image (554).png" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="Component React" %}
```
// Sample code

<PanelCard
  animationProps={{
    loop: false,
    noAutoplay: false
  }}
  cardClassName=""
  cardStyles={{}}
  className=""
  customIcon=""
  description="Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat."
  footerChildren={[
    <Button label="Button" onClick={()=>{}} type="button" variation="secondary"/>,
    <Button label="Button" onClick={()=>{}}  type="button"/>
  ]}
  footerStyles={{}}
  iconFill=""
  info="Ref ID "
  maxFooterButtonsAllowed={5}
  message="Success Message!"
  multipleResponses={[]}
  props={{}}
  response="949749795479"
  sortFooterButtons
  style={{}}
  type="success"
>
  <AlertCard
    className="panelcard-alert-card"
    text="This is success"
    variant="success"
  />
</PanelCard>
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

<figure><img src="../../../../../.gitbook/assets/image (555).png" alt=""><figcaption></figcaption></figure>

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (4) (2).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Success Panel</strong></p><p>Displays a confirmation message indicating successful operations and uses a green colour scheme with success iconography and optional ID or confirmation number.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (5) (2).png" alt=""><figcaption></figcaption></figure></div></td><td><strong>Error Panel</strong><br>Indicates failure or issues in the process, and this feature has a red colour scheme with an error icon, and optionally includes details on what failed and how to resolve it.</td></tr></tbody></table>

## Properties

<table data-header-hidden data-full-width="false"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><br><img src="../../../../../.gitbook/assets/image (6) (2).png" alt=""></td><td><p><strong>Description</strong></p><p>Toggle the presence of additional descriptive text below the main message.</p></td></tr><tr><td><strong>Edit Description</strong><br>Enables inline editing of the description field when required, allowing admins or users to update metadata or identifiers dynamically..</td><td><div><figure><img src="../../../../../.gitbook/assets/image (7) (2).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Actions</strong><br>Supports one or more action buttons such as “Go Back,” “Continue,” “Retry,” or custom CTAs.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (8) (2).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Additional Widgets</strong><br>Includes optional elements like info cards, links, or nested content to provide supplementary guidance or system feedback.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (9) (2).png" alt=""><figcaption></figcaption></figure></div></td></tr></tbody></table>

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>className</td><td>text</td><td>-</td></tr><tr><td>style</td><td>text</td><td>-</td></tr><tr><td>children</td><td>yes/no</td><td>-</td></tr><tr><td>footerChildren</td><td>yes/no</td><td>-</td></tr><tr><td>message</td><td>number</td><td>-</td></tr><tr><td>type</td><td>yes/no</td><td>false</td></tr><tr><td>info</td><td>yes/no</td><td>-</td></tr><tr><td>response</td><td>yes/no</td><td>-</td></tr><tr><td>customIcon</td><td>yes/no</td><td>0</td></tr><tr><td>iconFill</td><td>number</td><td>false</td></tr><tr><td>multipleResponses</td><td>yes/no</td><td>-</td></tr><tr><td>footerclassName</td><td>yes/no</td><td>false</td></tr><tr><td>footerStyles</td><td>yes/no</td><td>-</td></tr><tr><td>cardClassName</td><td>yes/no</td><td>-</td></tr><tr><td>cardStyles</td><td>yes/no</td><td>-</td></tr><tr><td>maxFooterButtonsAllowed</td><td>yes/no</td><td>-</td></tr><tr><td>sortFooterButtons</td><td>yes/no</td><td>-</td></tr><tr><td>showChildrenInline</td><td>yes/no</td><td>-</td></tr><tr><td>description</td><td>yes/no</td><td>-</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>Title</td><td>String</td><td>required(if header is not passed)</td></tr><tr><td>Number</td><td>double</td><td>-</td></tr><tr><td>Icon</td><td>Icon widget</td><td>-</td></tr><tr><td>header</td><td>Widget</td><td>-</td></tr><tr><td>content</td><td>Widget</td><td>required</td></tr><tr><td>divider</td><td>bool</td><td>false</td></tr><tr><td>initiallyExpanded</td><td>bool</td><td>false</td></tr><tr><td>showBorder</td><td>bool</td><td>false</td></tr><tr><td>onToggle</td><td>VoidCallBack Function</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

## Usage Guide

***

| <div><figure><img src="../../../../../.gitbook/assets/image (10) (2).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Provide specific feedback</strong></p><p>Display a unique reference ID, transaction number, or message that helps users verify or follow up.  Leave users guessing with vague messages like “Request submitted” without additional traceable context.</p> |
| ------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (11) (2).png" alt=""><figcaption></figcaption></figure></div> |                                                                                                                                                                                                                                                                      |
|                                                                                                                           |                                                                                                                                                                                                                                                                      |

## Change log

***

| Date         | Number  | Notes                                                                                           |
| ------------ | ------- | ----------------------------------------------------------------------------------------------- |
| Dec 15, 2024 | v-0.0.2 | <p>This component is added to the website.<br>This component is now individually versioned.</p> |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Content guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
