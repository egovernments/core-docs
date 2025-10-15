---
description: Design System - Menu Card component
---

# Menu Card

The Menu Card component serves as a navigational tile, guiding users through various modules, processes, or tasks. Built with accessibility, responsiveness, and clarity in mind, this molecule uses strong visual hierarchy with clear icons, descriptions, and optional labels. It supports interaction cues such as hover states and is optimised for multiple device sizes.

<figure><img src="../../../../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

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

MenuCard(
            heading: 'Heading',
            description: 'Lorem Ipsum',
            onTap: () {
              // Handle tap
            },
          ),
```
{% endtab %}

{% tab title="Component Design" %}

{% endtab %}
{% endtabs %}

## Anatomy

<figure><img src="../../../../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Menu 1</strong></p><p>A basic card with an icon and a short descriptive text for task or module access.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure></div></td><td><strong>Menu 2</strong><br>Extends Menu 1 by including a Label next to the icon to add context or categorisation.</td></tr></tbody></table>

## Properties

<table data-header-hidden data-full-width="false"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Icon - Menu 1 &#x26; 2</strong><br>Clearly conveys the function or context of the menu item.<br></td><td><div><figure><img src="../../../../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Description - Menu 1 &#x26; 2</strong><br>A short line of text to inform the user about the menu’s purpose, to indicate that the button is not active.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Label - Menu 2</strong><br>Appears above the description and helps name or categorise grouped items.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure></div></td></tr></tbody></table>

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>icon</td><td>text</td><td>-</td></tr><tr><td>menuName</td><td>text</td><td>-</td></tr><tr><td>description</td><td>yes/no</td><td>no</td></tr><tr><td>className</td><td>yes/no</td><td>no</td></tr><tr><td>styles</td><td>number</td><td>-</td></tr><tr><td>onClick</td><td>yes/no</td><td>-</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>heading</td><td>String</td><td>required</td></tr><tr><td>description</td><td>String</td><td>-</td></tr><tr><td>Icon</td><td>Icon Data</td><td>-</td></tr><tr><td>onTap</td><td>VoidCallBack</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

## Usage Guide

***

| <div><figure><img src="../../../../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Maintain clarity</strong></p><p>Use concise, descriptive labels and explanations for each card.  Overload the card with long sentences or technical jargon..</p> |
| --------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure></div> |                                                                                                                                                                             |

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
