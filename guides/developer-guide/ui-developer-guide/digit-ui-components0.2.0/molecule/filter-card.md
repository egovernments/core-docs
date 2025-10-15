---
description: Design System - Filter Card component
---

# Filter Card

The Filter Card component is a layout container designed to offer users an intuitive and accessible way to narrow down data or results based on specified parameters.

<figure><img src="../../../../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../../../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Horizontal</strong></p><p>Ideal for wider layouts or desktop/tablet views where filters are applied inline at the top of a table or section. Promotes quick scanning and efficient space usage.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure></div></td><td><strong>Vertical</strong><br>This layout presents filters in a stacked format, enabling a more comfortable interaction on narrow viewports or where field variety is high.</td></tr></tbody></table>

## Properties

<table data-header-hidden data-full-width="false"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Header Icon</strong><br>A visual cue precedes the heading for easy recognition and visual alignment with DIGIT’s iconography standards..<br></td><td><div><figure><img src="../../../../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Close Button</strong><br>Offers the ability to optionally include a close/dismiss icon for the card, especially useful when it’s implemented as an overlay or drawer.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure></div></td></tr></tbody></table>

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>wrapperClassName</td><td>text</td><td>-</td></tr><tr><td>headerContentClassName</td><td>text</td><td>-</td></tr><tr><td>caption</td><td>yes/no</td><td>no</td></tr><tr><td>captionClassName</td><td>yes/no</td><td>no</td></tr><tr><td>header</td><td>number</td><td>-</td></tr><tr><td>headerClasName</td><td>yes/no</td><td>no</td></tr><tr><td>subHeader</td><td>yes/no</td><td>no</td></tr><tr><td>subHeaderClasName</td><td>yes/no</td><td>no</td></tr><tr><td>body</td><td>yes/no</td><td>no</td></tr><tr><td>bodyClasName</td><td>number</td><td>no</td></tr><tr><td>style</td><td>yes/no</td><td>-no</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>Title</td><td>String</td><td>required(if header is not passed)</td></tr><tr><td>Number</td><td>double</td><td>-</td></tr><tr><td>Icon</td><td>Icon widget</td><td>-</td></tr><tr><td>header</td><td>Widget</td><td>-</td></tr><tr><td>content</td><td>Widget</td><td>required</td></tr><tr><td>divider</td><td>bool</td><td>false</td></tr><tr><td>initiallyExpanded</td><td>bool</td><td>false</td></tr><tr><td>showBorder</td><td>bool</td><td>false</td></tr><tr><td>onToggle</td><td>VoidCallBack Function</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

## Usage Guide

***

| <div><figure><img src="../../../../../.gitbook/assets/image (540).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Match layout to context</strong></p><p>Use the horizontal variant for desktop/table views and vertical for mobile or sidebar layouts.  Avoid forcing a vertical layout into a constrained width or a horizontal one in mobile viewports.</p> |
| ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (541).png" alt=""><figcaption></figcaption></figure></div> |                                                                                                                                                                                                                                                         |
|                                                                                                                        |                                                                                                                                                                                                                                                         |

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
