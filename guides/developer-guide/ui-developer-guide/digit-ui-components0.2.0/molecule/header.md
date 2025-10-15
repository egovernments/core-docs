---
description: Design System - Header component
---

# Header

The Header component establishes a clear and consistent identity. Designed with accessibility and responsiveness in mind, the Header serves as a navigation anchor, contextual identifier, and personalisation hub. It ensures that users always know where they are, can quickly change settings like language or city, and recognise the governing body or service brand in view.

<figure><img src="../../../../../.gitbook/assets/image (511).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../../../../.gitbook/assets/image (512).png" alt=""><figcaption></figcaption></figure>

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (513).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Light Mode</strong></p><p>A minimal white background header suited for daylight or bright-themed interfaces. It keeps the focus on the primary page content while maintaining clear brand visibility.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (514).png" alt=""><figcaption></figcaption></figure></div></td><td><strong>Dark Mode</strong><br>A bolder visual variant is typically used in high-contrast interfaces. Ideal for mobile or dashboard environments where visual hierarchy is important.</td></tr></tbody></table>

## Properties

<table data-header-hidden data-full-width="false"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Customise Name</strong><br>The name of the platform, department, or app can be tailored, making the header reusable across multiple services or city implementations. <br></td><td><div><figure><img src="../../../../../.gitbook/assets/image (515).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><p><strong>Language Selector</strong></p><p>Supports multilingual use by allowing users to change the interface language dynamically from the header.</p></td><td><div><figure><img src="../../../../../.gitbook/assets/image (516).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><p><strong>City Selection Dropdown</strong></p><p>Allows users to switch between different cities or localities, ensuring content and services stay relevant to the chosen jurisdiction.</p></td><td><div><figure><img src="../../../../../.gitbook/assets/image (517).png" alt=""><figcaption></figcaption></figure></div></td></tr></tbody></table>

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>wrapperClassName</td><td>text</td><td>-</td></tr><tr><td>headerContentClassName</td><td>text</td><td>-</td></tr><tr><td>caption</td><td>yes/no</td><td>no</td></tr><tr><td>captionClassName</td><td>yes/no</td><td>no</td></tr><tr><td>header</td><td>number</td><td>-</td></tr><tr><td>headerClasName</td><td>yes/no</td><td>-</td></tr><tr><td>subHeader</td><td>yes/no</td><td>no</td></tr><tr><td>subHeaderClasName</td><td>yes/no</td><td>no</td></tr><tr><td>body</td><td>yes/no</td><td>no</td></tr><tr><td>bodyClasName</td><td>number</td><td>no</td></tr><tr><td>style</td><td>yes/no</td><td>no</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>Title</td><td>String</td><td>required(if header is not passed)</td></tr><tr><td>Number</td><td>double</td><td>-</td></tr><tr><td>Icon</td><td>Icon widget</td><td>-</td></tr><tr><td>header</td><td>Widget</td><td>-</td></tr><tr><td>content</td><td>Widget</td><td>required</td></tr><tr><td>divider</td><td>bool</td><td>false</td></tr><tr><td>initiallyExpanded</td><td>bool</td><td>false</td></tr><tr><td>showBorder</td><td>bool</td><td>false</td></tr><tr><td>onToggle</td><td>VoidCallBack Function</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

## Usage Guide

| <div><figure><img src="../../../../../.gitbook/assets/image (518).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Contrast Adaptation</strong></p><p>Use appropriate variants (Light/Dark) depending on the surrounding UI theme to ensure optimal readability and visual harmony with the interface environment.  Don't use the same header variant across different background contexts, as this creates poor contrast and reduces visibility when the header colour doesn't properly complement the surrounding theme.</p> |
| ---------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (519).png" alt=""><figcaption></figcaption></figure></div> |                                                                                                                                                                                                                                                                                                                                                                                                                        |

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
