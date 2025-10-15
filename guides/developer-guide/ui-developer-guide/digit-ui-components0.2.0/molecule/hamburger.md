---
description: Design System - Hamburger component
---

# Hamburger

The Hamburger component serves as a collapsible vertical navigation panel, enabling users to switch between modules, configure language and city preferences, and access universal actions. This component provides a consistent and intuitive experience across services.

<figure><img src="../../../../../.gitbook/assets/image (520).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../../../../.gitbook/assets/image (521).png" alt=""><figcaption></figcaption></figure>

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (522).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Light Mode</strong></p><p>The default Text Block displays a structured combination of a caption, heading, subheading, and description. Each section can be individually toggled on or off based on the context or content requirement.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (523).png" alt=""><figcaption></figcaption></figure></div></td><td><strong>Dark Mode</strong><br>Intended for darker UIs, this version enhances visual contrast and reduces strain during prolonged usage or low-light environments.</td></tr></tbody></table>

## Properties

<table data-header-hidden data-full-width="false"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Profile</strong><br>Displays user-specific details such as name and mobile number, along with an optional avatar or icon, reinforcing personalisation.<br></td><td><div><figure><img src="../../../../../.gitbook/assets/image (524).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Enable Search</strong><br>Allows users to search through nested navigation items, improving usability for platforms with many modules or submodules.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (525).png" alt=""><figcaption></figcaption></figure></div></td></tr></tbody></table>

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>items</td><td>text</td><td>-</td></tr><tr><td>profileName</td><td>text</td><td>-</td></tr><tr><td>profileNumber</td><td>yes/no</td><td>no</td></tr><tr><td>theme</td><td>yes/no</td><td>no</td></tr><tr><td>className</td><td>yes/no</td><td>-</td></tr><tr><td>styles</td><td>yes/no</td><td>-</td></tr><tr><td>hideUserManuals</td><td>yes/no</td><td>no</td></tr><tr><td>useManualLabel</td><td>yes/no</td><td>no</td></tr><tr><td>profile</td><td>yes/no</td><td>no</td></tr><tr><td>usermanuals</td><td>number</td><td>no</td></tr><tr><td>onSelect</td><td>yes/no</td><td>no</td></tr><tr><td>onLogout</td><td>yes/no</td><td>no</td></tr><tr><td>reopenOnLogout</td><td>yes/no</td><td>no</td></tr><tr><td>closeOnClickOutside</td><td>yes/no</td><td>no</td></tr><tr><td>onOutsideClick</td><td>yes/no</td><td>no</td></tr><tr><td>onLabelClick</td><td>yes/no</td><td>no</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>Title</td><td>String</td><td>required(if header is not passed)</td></tr><tr><td>Number</td><td>double</td><td>-</td></tr><tr><td>Icon</td><td>Icon widget</td><td>-</td></tr><tr><td>header</td><td>Widget</td><td>-</td></tr><tr><td>content</td><td>Widget</td><td>required</td></tr><tr><td>divider</td><td>bool</td><td>false</td></tr><tr><td>initiallyExpanded</td><td>bool</td><td>false</td></tr><tr><td>showBorder</td><td>bool</td><td>false</td></tr><tr><td>onToggle</td><td>VoidCallBack Function</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

## Usage Guide

***

| <div><figure><img src="../../../../../.gitbook/assets/image (526).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Action Accessibility</strong></p><p>Keep important global actions like "Logout" and "User Manual" fixed and accessible at the bottom.  Don’t hide logout or profile info under collapsible menus; users expect to see these instantly upon opening the drawer.</p> |
| ---------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (527).png" alt=""><figcaption></figcaption></figure></div> |                                                                                                                                                                                                                                                                               |
|                                                                                                                        |                                                                                                                                                                                                                                                                               |

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
