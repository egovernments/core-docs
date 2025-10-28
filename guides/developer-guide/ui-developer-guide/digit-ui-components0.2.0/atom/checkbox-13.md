---
description: Design System - Radio component
---

# Radio

The Radio component allows users to select a single option from a set of mutually exclusive choices. It promotes clarity, ease of decision-making, and accessibility through consistent styling and intuitive interaction patterns.

<figure><img src="../../../../../.gitbook/assets/image (349).png" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="Component React" %}
```
// Sample code

        <RadioButtons
          onSelect={(selected) => {
            setSelectedOption(selected.code);
          }}
          disabled = {true}
          options={options}
          optionsKey="name"
          selectedOption={options.find((opt) => opt.code === selectedOption)}
          value={selectedOption}
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

<figure><img src="../../../../../.gitbook/assets/image (351).png" alt=""><figcaption></figcaption></figure>

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (353).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Active</strong></p><p>The active or "on" state of a radio button indicates that the option has been selected by the user. Unlike checkboxes, only one radio button within a group can be in the active state at any given time.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (352).png" alt=""><figcaption></figcaption></figure></div></td><td><strong>Inactive</strong><br>The inactive or "off" state of a radio button indicates that the option is available but not currently selected. This state is distinct from both the selected state and the disabled state. When a radio button is in the inactive state, it remains fully interactive. Users can click or tap on the radio button to select it, which will automatically deselect any previously selected option in the same group.</td></tr></tbody></table>

## Properties

<table data-header-hidden data-full-width="false"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Filled State</strong><br>A radio button that shows it is selected by filling the inner circle. This state indicates the user’s current choice.<br></td><td><div><figure><img src="../../../../../.gitbook/assets/image (363).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Default State</strong><br>The standard appearance of a radio button before any selection is made. It appears with an empty circle and is ready for interaction.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (362).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Disabled State</strong><br>A radio button that appears greyed out and cannot be selected. This state is used when an option is not available for user interaction.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (361).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Disabled Filled</strong><br>A selected radio button that is also disabled. It indicates a pre-selected option that users cannot change.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (357).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Read Only</strong><br>A radio button that is selected but not interactive. This state is used when users can view the selected option but are not allowed to modify it.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (356).png" alt=""><figcaption></figcaption></figure></div></td></tr></tbody></table>

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>selectedOption</td><td>text</td><td>-</td></tr><tr><td>onSelect</td><td>text</td><td>no</td></tr><tr><td>options</td><td>yes/no</td><td>no</td></tr><tr><td>optionsKey</td><td>yes/no</td><td>-</td></tr><tr><td>innerStyles</td><td>number</td><td>-</td></tr><tr><td>style</td><td>yes/no</td><td>-</td></tr><tr><td>alignVertical</td><td>yes/no</td><td>no</td></tr><tr><td>additionalWrapperClass</td><td>yes/no</td><td>no</td></tr><tr><td>disabled</td><td>yes/no</td><td>no</td></tr><tr><td>name</td><td>number</td><td>no</td></tr><tr><td>inputRef</td><td>yes/no</td><td>no</td></tr><tr><td>inputStyle</td><td>text</td><td>no</td></tr><tr><td>isDependent</td><td>yes/no</td><td>no</td></tr><tr><td>labelKey</td><td>yes/no</td><td>-</td></tr><tr><td>value</td><td>yes/no</td><td>-</td></tr><tr><td>isLabelFirst</td><td>yes/no</td><td>-</td></tr><tr><td>inputStyle</td><td>yes/no</td><td>-</td></tr><tr><td>labelKey</td><td>yes/no</td><td>-</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>Title</td><td>String</td><td>required(if header is not passed)</td></tr><tr><td>Number</td><td>double</td><td>-</td></tr><tr><td>Icon</td><td>Icon widget</td><td>-</td></tr><tr><td>header</td><td>Widget</td><td>-</td></tr><tr><td>content</td><td>Widget</td><td>required</td></tr><tr><td>divider</td><td>bool</td><td>false</td></tr><tr><td>initiallyExpanded</td><td>bool</td><td>false</td></tr><tr><td>showBorder</td><td>bool</td><td>false</td></tr><tr><td>onToggle</td><td>VoidCallBack Function</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

## Interaction State

***

| <div><figure><img src="../../../../../.gitbook/assets/image (354).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Hover State</strong></p><p>When users hover over an inactive radio button, it transitions to display our Primary orange colour. This distinct colour change serves as a clear visual cue that differentiates the hover state from both the default inactive state and the non-interactive disabled state. The orange highlight indicates to users that the radio button is interactive and can be selected, encouraging engagement while reinforcing the component's actionable nature.</p> |
| ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <div><figure><img src="../../../../../.gitbook/assets/image (355).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Mousedown State</strong></p><p>When a user hovers over the button, a visual cue is added to emphasise interactivity. This is achieved by introducing a subtle outline around the button. The subtle halo outline complements the button's style, without overwhelming the design.</p>                                                                                                                                                                                                       |

## Behaviours

|                                                                                                                        |                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <div><figure><img src="../../../../../.gitbook/assets/image (364).png" alt=""><figcaption></figcaption></figure></div> | When the radio label exceeds the width of the parent container, the text wraps to the next line to maintain readability. Character count can be limited if required based on layout constraints. |
|                                                                                                                        |                                                                                                                                                                                                  |

***

## Usage Guide

***

| <div><figure><img src="../../../../../.gitbook/assets/image (368).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Single Selection Only</strong></p><p>Use radio buttons when the user needs to select only one option from a list. They are not intended for multi-selection; use checkboxes if multiple selections are required.</p> |
| ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|                                                                                                                        |                                                                                                                                                                                                                                 |

## Changelog

***

| Date         | Number  | Notes                                                                                           |
| ------------ | ------- | ----------------------------------------------------------------------------------------------- |
| Dec 15, 2024 | v-0.0.2 | <p>This component is added to the website.<br>This component is now individually versioned.</p> |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Content guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
