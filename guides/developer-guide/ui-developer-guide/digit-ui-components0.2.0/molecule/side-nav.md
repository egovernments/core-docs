---
description: Design System - Side nav component
---

# Side Nav

The Side Nav component acts as the primary navigation pattern, helping users access modules, submodules, and utilities in a compact, vertically stacked structure. Designed for both accessibility and scalability, it accommodates icons, labels, tree structures, and persistent actions, ensuring a consistent experience across municipal and citizen-facing interfaces.

<figure><img src="../../../../../.gitbook/assets/image (528).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../../../../.gitbook/assets/image (529).png" alt=""><figcaption></figcaption></figure>

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (530).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Light</strong></p><p>Ideal for interfaces with brighter UIs, ensuring visual consistency and high contrast with dark icons and text.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (531).png" alt=""><figcaption></figcaption></figure></div></td><td><strong>Dark</strong><br>Best suited for dashboards or applications requiring reduced eye strain or a focused visual hierarchy.</td></tr></tbody></table>

## Properties

<table data-header-hidden data-full-width="false"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Enable Search</strong><br>Provides a quick-filtering input field at the top of the side nav, enabling users to locate modules and nested items efficiently. Particularly helpful in apps with deep or large information architectures.<br></td><td><img src="../../../../../.gitbook/assets/Imagep1.png" alt=""></td></tr><tr><td><strong>Universal Action</strong><br>Includes persistent utilities like Help, Settings, and Logout; these remain accessible regardless of scroll or nav state, improving usability.</td><td><img src="../../../../../.gitbook/assets/Imagep2.png" alt=""></td></tr><tr><td><strong>Tree Selection for Children</strong><br>Supports hierarchical navigation by displaying submodules or inner navigation when parent items are expanded. Allows users to interact with nested items.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (532).png" alt=""><figcaption></figcaption></figure></div></td></tr></tbody></table>

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>items</td><td>text</td><td>-</td></tr><tr><td>theme</td><td>text</td><td>-</td></tr><tr><td>variant</td><td>yes/no</td><td>no</td></tr><tr><td>collapsedWidth</td><td>yes/no</td><td>no</td></tr><tr><td>expandedWidth</td><td>number</td><td>-</td></tr><tr><td>transitionDuration</td><td>yes/no</td><td>-</td></tr><tr><td>styles</td><td>yes/no</td><td>no</td></tr><tr><td>hideAccessbilityTools</td><td>yes/no</td><td>no</td></tr><tr><td>enableSearch</td><td>yes/no</td><td>no</td></tr><tr><td>onSelect</td><td>yes/no</td><td>no</td></tr><tr><td>onBottomItemClick</td><td>number</td><td>no</td></tr><tr><td>className</td><td>yes/no</td><td>no</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>Title</td><td>String</td><td>required(if header is not passed)</td></tr><tr><td>Number</td><td>double</td><td>-</td></tr><tr><td>Icon</td><td>Icon widget</td><td>-</td></tr><tr><td>header</td><td>Widget</td><td>-</td></tr><tr><td>content</td><td>Widget</td><td>required</td></tr><tr><td>divider</td><td>bool</td><td>false</td></tr><tr><td>initiallyExpanded</td><td>bool</td><td>false</td></tr><tr><td>showBorder</td><td>bool</td><td>false</td></tr><tr><td>onToggle</td><td>VoidCallBack Function</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

## Usage Guide

***

| <div><figure><img src="../../../../../.gitbook/assets/image (533).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Hierarchical Structure</strong></p><p>Enable tree selection for complex apps where submodules need to be grouped contextually.  Don’t flatten deep hierarchies if users need to frequently access child modules—it hinders navigation efficiency.</p> |
| ---------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (534).png" alt=""><figcaption></figcaption></figure></div> |                                                                                                                                                                                                                                                                  |

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
