---
description: Design System - Dropdown component
hidden: true
---

# Dropdown

The Checkbox is a simple selection control that allows users to make binary choices, such as selecting or deselecting options. It is commonly used in forms, preference settings, and multi-select scenarios, providing clear visual feedback for user actions.

<figure><img src="../../../../../../../.gitbook/assets/Image.png" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="Component React" %}
```
// Sample code
<Dropdown
  additionalWrapperClass=""
  defaultValue="FEMALE"
  description=""
  error=""
  errorStyle={null}
  inputRef={null}
  label="Select Option"
  name="genders"
  onChange={()=>{}}
  option={[
    {
      code: 'Option1',
      name: 'Option1'
    },
    {
      code: 'Option2',
      name: 'Option2'
    },
    {
      code: 'Option3',
      name: 'Option3'
    }
  ]}
  optionKey="name"
  optionsCustomStyle={{}}
  props={{
    data: [
      {
        code: 'Option1',
        name: 'Option1'
      },
      {
        code: 'Option2',
        name: 'Option2'
      },
      {
        code: 'Option3',
        name: 'Option3'
      }
    ],
    isLoading: false
  }}
  select={(e)=>{console.log(e)}}
  t={()=>{}}
  type="dropdown"
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

<figure><img src="../../../../../../../.gitbook/assets/Imagea.png" alt=""><figcaption></figcaption></figure>

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><img src="../../../../../../../.gitbook/assets/Imagev1.png" alt=""></td><td><p>Checked</p><p>The checked state indicates that the user has actively selected the option. It provides clear visual feedback with a filled checkbox, often accompanied by a checkmark. This state should be used when an option is explicitly chosen or enabled by default.</p></td></tr><tr><td><img src="../../../../../../../.gitbook/assets/Imagev2.png" alt="" data-size="original"></td><td><strong>Intermediate</strong><br>The indeterminate state represents a mixed selection, typically used for parent checkboxes in multi-select scenarios. It visually signals that only some child options are selected, rather than all. This state does not appear by direct user interaction but is controlled programmatically to reflect partial selections.</td></tr><tr><td><img src="../../../../../../../.gitbook/assets/Imagev3.png" alt=""></td><td><p><strong>Unchecked</strong></p><p>The unchecked state indicates that the option is not selected. It appears as an empty checkbox, providing a clear visual cue that no action has been taken. This is the default state unless specified otherwise.</p></td></tr></tbody></table>

## Properties

<table data-header-hidden data-full-width="false"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Label</strong><br>This property represents the text displayed inside the button. It is a required field and helps users understand the action that the button will trigger. The label should be concise and clear to communicate the button’s purpose effectively.<br></td><td><img src="../../../../../../../.gitbook/assets/Imagep1.png" alt=""></td></tr><tr><td><strong>Disabled</strong><br>The “isDisabled” property disables the button, preventing any user interaction. It also applies a disabled visual style (like graying out the button) to indicate that the button is not active.</td><td><img src="../../../../../../../.gitbook/assets/Imagep2.png" alt=""></td></tr><tr><td><strong>Icon</strong><br>The icon property specifies the name of the icon to be rendered inside the button. This helps provide a visual cue along with the button text. The icon placement can be either before or after the label based on the how the “Prefix” and “Suffix” properties are defined.</td><td><img src="../../../../../../../.gitbook/assets/Imagep3.png" alt=""></td></tr><tr><td><strong>Size</strong><br>The size property specifies the size of the button. You can choose between "large", "medium", and "small" to adjust the button's height and font size.</td><td><img src="../../../../../../../.gitbook/assets/Imagep4.png" alt=""></td></tr><tr><td><strong>Type</strong><br>The type property determines the HTML type attribute for the button, such as "submit", "button", or "actionButton". This is useful for form submission or defining button behavior in HTML forms.</td><td><img src="../../../../../../../.gitbook/assets/Imagep5.png" alt=""></td></tr></tbody></table>

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>varinat</td><td>string</td><td>-</td></tr><tr><td>id</td><td>number</td><td>-</td></tr><tr><td>onBlur</td><td>function</td><td>-</td></tr><tr><td>optionKey</td><td>string</td><td>-</td></tr><tr><td>showIcon</td><td>boolean</td><td>false</td></tr><tr><td>className</td><td>string</td><td>-</td></tr><tr><td>style</td><td>object</td><td>{}</td></tr><tr><td>profilePic</td><td>element</td><td>-</td></tr><tr><td>theme</td><td>string</td><td>-</td></tr><tr><td>customSelector</td><td>element</td><td>null</td></tr><tr><td>showArrow</td><td>boolean</td><td>true</td></tr><tr><td>isSearchable</td><td>boolean</td><td>true</td></tr><tr><td>disabled</td><td>boolean</td><td>false</td></tr><tr><td>autoComplete</td><td>boolean</td><td>-</td></tr><tr><td>keepNull</td><td>boolean</td><td>-</td></tr><tr><td>t</td><td>function</td><td>-</td></tr><tr><td>freeze</td><td>boolean</td><td>-</td></tr><tr><td>ref</td><td>reference to a DOM element</td><td>-</td></tr><tr><td>showToolTip</td><td>boolean</td><td>-</td></tr><tr><td>option</td><td>array</td><td>-</td></tr><tr><td>showBottom</td><td>boolean</td><td>-</td></tr><tr><td>menuStyles</td><td>object</td><td>{}</td></tr><tr><td>optionCardStyles</td><td>object</td><td>{}</td></tr><tr><td>selected</td><td>object</td><td>-</td></tr><tr><td>onClick</td><td>function</td><td>-</td></tr><tr><td>autoFocus</td><td>boolean</td><td>-</td></tr><tr><td>placeholder</td><td>string</td><td>-</td></tr><tr><td>select</td><td>function</td><td>-</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>Title</td><td>String</td><td>required(if header is not passed)</td></tr><tr><td>Number</td><td>double</td><td>-</td></tr><tr><td>Icon</td><td>Icon widget</td><td>-</td></tr><tr><td>header</td><td>Widget</td><td>-</td></tr><tr><td>content</td><td>Widget</td><td>required</td></tr><tr><td>divider</td><td>bool</td><td>false</td></tr><tr><td>initiallyExpanded</td><td>bool</td><td>false</td></tr><tr><td>showBorder</td><td>bool</td><td>false</td></tr><tr><td>onToggle</td><td>VoidCallBack Function</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

## Interaction State

***

| ![](../../../../../../../.gitbook/assets/Imageb1.png) | <p><strong>Hover State</strong></p><p>When a user hovers over the button, a visual cue is added to emphasize interactivity. This is achieved by introducing a subtle line below the button. The line appears as a clean, horizontal underline that complements the button's style, without overwhelming the design. The hover state enhances the button's affordance, guiding users and improving interactivity without altering the button’s primary layout or design.</p> |
| ----------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![](../../../../../../../.gitbook/assets/Imageb2.png) | <p><strong>Mousedown State</strong></p><p>The Mouse Down state of the button represents the moment when the user clicks and holds the button. This state provides immediate feedback to the user, confirming that their interaction has been registered. The text label becomes bolder, emphasizing the active interaction</p>                                                                                                                                              |

## Usage Guide

***

| ![](<../../../../../../../.gitbook/assets/4AA18190-F8A7-4D78-A1B7-9D226F44C477_4_5005_c (1).jpeg>) | <p><strong>Use for compact information display</strong></p><p>Organise dense or hierarchical content like FAQs, step-by-step instructions</p> |
| -------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
|                                                                                                    |                                                                                                                                               |
|                                                                                                    |                                                                                                                                               |

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
