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

| Date | Number | Notes |
| ---- | ------ | ----- |
|      |        |       |
|      |        |       |
|      |        |       |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td>All interactive states</td></tr><tr><td>true</td><td>Accessible use of colours</td></tr><tr><td>true</td><td>Accessible contrast for text</td></tr><tr><td>true</td><td>Accessible contrast for UI components</td></tr><tr><td>true</td><td>Keyboard interactions</td></tr></tbody></table>
