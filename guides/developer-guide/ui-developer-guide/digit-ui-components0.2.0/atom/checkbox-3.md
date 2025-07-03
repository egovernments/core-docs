---
description: Design System - Dropdown single select component
---

# Dropdown - Single Select

The Dropdown - Single Select lets users pick one option from a predefined list. It is ideal for forms and filters where only one choice is valid, offering a compact and user-friendly way to streamline selections.

<figure><img src="../../../../../.gitbook/assets/image (387).png" alt=""><figcaption></figcaption></figure>

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

***

<figure><img src="../../../../../.gitbook/assets/image (388).png" alt=""><figcaption></figcaption></figure>

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (394).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Basic Dropdown</strong></p><p>The Basic Dropdown serves as a standard selection tool, displaying a list of options when triggered. It is ideal for simple use cases such as selecting a city, category, or value from a list. This variant focuses on clarity and ease of interaction, offering a clean and accessible way to choose a single option.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (393).png" alt=""><figcaption></figcaption></figure></div></td><td><strong>Categorical Dropdown</strong><br>The Categorical Dropdown introduces grouped options within the dropdown menu. This structure is suitable for cases where options belong to distinct categories, such as departments, regions, or job types. Each category acts as a label, visually separating options to enhance scannability and reduce cognitive load.</td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (392).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Nested Text Dropdown</strong></p><p>This enables sub-options to be embedded within a main option, providing an expandable hierarchy of selections. This is useful when each primary option leads to further granularity, such as a parent category leading to subcategories. It keeps the UI clean while supporting detailed selection paths.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (391).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Profile Dropdown</strong></p><p>The Profile Dropdown is designed to display user-related actions and information, typically accessed via an avatar or username. It includes quick links such as account settings, profile view, and logout. This variant is focused on user personalization and session management in an application.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (390).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Profile with Nested Text Dropdown</strong></p><p>This variant extends the Profile Dropdown by incorporating nested items for more structured user options. Sub-options can be organized under primary sections, enabling users to access layered account controls efficiently.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (389).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Tree Dropdown</strong></p><p>The Tree Dropdown supports multi-level branching, allowing users to drill down into deeply nested structures. It is ideal for navigating hierarchical datasets such as file systems, organisational structures, or nested location data. Each node can expand independently, helping users locate items without overwhelming the interface.</p></td></tr><tr><td></td><td></td></tr></tbody></table>

## Properties

<table data-header-hidden data-full-width="false"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Disabled</strong><br>A greyed-out, inactive selector showing unavailable options while maintaining visibility of potential choices.<br></td><td><div><figure><img src="../../../../../.gitbook/assets/image (402).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Error</strong><br>Visually highlights invalid selections with warning colours and messages to prompt user correction.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (401).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><p><strong>Icon</strong></p><p>An optional visual cue inside the dropdown that represents the selection type, improving recognition and UI scannability at a glance.</p></td><td><div><figure><img src="../../../../../.gitbook/assets/image (400).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><p><strong>Label</strong></p><p>A clear, short identifier placed consistently near the selector to indicate its purpose.</p></td><td><div><figure><img src="../../../../../.gitbook/assets/image (399).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><p><strong>Help Text</strong></p><p>Optional guidance below the dropdown that explains requirements or provides examples without crowding the UI.</p></td><td><div><figure><img src="../../../../../.gitbook/assets/image (398).png" alt=""><figcaption></figcaption></figure></div></td></tr></tbody></table>

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>option</td><td>text</td><td>-</td></tr><tr><td>variant</td><td>text</td><td>no</td></tr><tr><td>id</td><td>yes/no</td><td>no</td></tr><tr><td>placeholder</td><td>yes/no</td><td>-</td></tr><tr><td>onBlur</td><td>number</td><td>-</td></tr><tr><td>optionKey</td><td>yes/no</td><td>-</td></tr><tr><td>showIcon</td><td>yes/no</td><td>no</td></tr><tr><td>className</td><td>yes/no</td><td>no</td></tr><tr><td>style</td><td>yes/no</td><td>no</td></tr><tr><td>profilePic</td><td>number</td><td>no</td></tr><tr><td>theme</td><td>yes/no</td><td>no</td></tr><tr><td>customSelector</td><td></td><td>no</td></tr><tr><td>showArrow</td><td>yes/no</td><td>no</td></tr><tr><td>isSearchable</td><td>yes/no</td><td></td></tr><tr><td>disabled</td><td>yes/no</td><td></td></tr><tr><td>keepNull</td><td>yes/no</td><td></td></tr><tr><td>freeze</td><td>yes/no</td><td></td></tr><tr><td>ref</td><td>yes/no</td><td></td></tr><tr><td>showTooltip</td><td>yes/no</td><td></td></tr><tr><td>showBottom</td><td>yes/no</td><td></td></tr><tr><td>menuStyles</td><td>yes/no</td><td></td></tr><tr><td>optionCardStyles</td><td>yes/no</td><td></td></tr><tr><td>selected</td><td>yes/no</td><td></td></tr><tr><td>autoFocus</td><td>yes/no</td><td></td></tr><tr><td>select</td><td>yes/no</td><td></td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>Title</td><td>String</td><td>required(if header is not passed)</td></tr><tr><td>Number</td><td>double</td><td>-</td></tr><tr><td>Icon</td><td>Icon widget</td><td>-</td></tr><tr><td>header</td><td>Widget</td><td>-</td></tr><tr><td>content</td><td>Widget</td><td>required</td></tr><tr><td>divider</td><td>bool</td><td>false</td></tr><tr><td>initiallyExpanded</td><td>bool</td><td>false</td></tr><tr><td>showBorder</td><td>bool</td><td>false</td></tr><tr><td>onToggle</td><td>VoidCallBack Function</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

## Interaction State

***

<table data-header-hidden data-full-width="false"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Hover State</strong><br>When a user hovers over the dropdown trigger, a visual cue such as a border highlight is introduced to indicate interactivity. This subtle shift in appearance signals that the component is actionable. The hover state improves discoverability and helps users distinguish interactive elements from static content.<br></td><td><div><figure><img src="../../../../../.gitbook/assets/image (397).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><p><strong>Selected State</strong></p><p>When an option within the dropdown is selected, it is visually highlighted through a background colour fill and bold text style. This state communicates the user’s current choice clearly and supports actions such as re-selection or change. The selected state ensures clarity and reinforces decision-making within the interface.</p></td><td><div><figure><img src="../../../../../.gitbook/assets/image (396).png" alt=""><figcaption></figcaption></figure></div></td></tr></tbody></table>

## Behaviours

|                                                                                                                        |                                                                                                                                                                                                                                                                                                    |
| ---------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (404).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Expanded State</strong></p><p>When a user clicks or taps on the dropdown, it expands to reveal a list of options. The dropdown remains open until an option is selected or the user clicks outside the dropdown. The selected option is highlighted to indicate the current choice.</p> |
| <div><figure><img src="../../../../../.gitbook/assets/image (403).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Animation</strong></p><p>The dropdown opens and closes with a smooth "ease-in" animation, enhancing the user experience.</p>                                                                                                                                                            |

***

## Usage Guide

***

| <div><figure><img src="../../../../../.gitbook/assets/image (406).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Use Clear and Concise Labels</strong></p><p>Use descriptive and straightforward labels for the dropdown and its options. This helps users quickly understand the purpose and make informed choices.</p> |
| ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <div><figure><img src="../../../../../.gitbook/assets/image (407).png" alt=""><figcaption></figcaption></figure></div> |                                                                                                                                                                                                                    |

## Changelog

***

| Date         | Number  | Notes                                                                                           |
| ------------ | ------- | ----------------------------------------------------------------------------------------------- |
| Dec 15, 2024 | v-0.0.2 | <p>This component is added to the website.<br>This component is now individually versioned.</p> |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Content guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
