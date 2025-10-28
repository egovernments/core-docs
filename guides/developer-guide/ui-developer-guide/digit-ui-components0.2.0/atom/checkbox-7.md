---
description: Design System - Multi Select component
---

# Dropdown - Multi Select

The Multi Select dropdown component enables users to select multiple options from a structured list. It is designed to enhance efficiency in scenarios where bulk selection is necessary, such as filtering results, assigning categories, or selecting roles. This component supports flexible content types, hierarchical grouping, and contextual help to guide user interaction.

<figure><img src="../../../../../.gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="Component React" %}
```
// Sample code

<MultiSelectDropdown
              onClose={(values) => {
                setSlectedOptions(values);
              }}
              defaultLabel="" // Default label for selected
              defaultUnit="" // Default unit for selected
              props={{
                className:'', // custom class name for digit-multiselectdropdown-wrap
                style:{} // custom styles for digit-multiselectdropdown-wrap
              }}
              isPropsNeeded={false}
              ServerStyle={{}} // custom styles for digit-multiselectdropdown-server
              config={{
                clearLabel: "", // label for clear all chip , default label is "Clear All"
                isDropdownWithChip: true, // flag to show chips
                showIcon: true, // flag to add icons for each options
                numberOfChips: 4, // count of the chips to be shown , if more selected adds + chip
              }}
              disabled={false} // disable multiselect dropdown
              selectAllLabel="" // label for select all
              categorySelectAllLabel="" // label for category level select all
              restrictSelection={false} // restricts to select any option
              isSearchable={true} // flag to make multiselect dropdown selectable
              chipsKey="" // what to be shown as label for chips
              frozenData={[
                {
                  code: "Category A.Option A",
                  name: "Option A",
                  icon: "Article",
                },
              ]}
              // can add frozen data
              handleViewMore={(e) => {
                setShowPopup(true);
              }} // when clicked on + chip this is called
              showTooltip={true} // flag to show the tooltip for labels and options on hover
              variant={"nestedmultiselect"} // varinat ("treemultiselect","nestedmultiselect","nestedtextmultiselect")
              onSelect={() => {}} // mandatory prop
              selected={[]} // selected array
              addSelectAllCheck={true} // flag to add select all check
              addCategorySelectAllCheck={true} // flag to add category select all check
              options={[
                {
                  name: "Category A",
                  options: [
                    {
                      code: "Category A.Option A",
                      name: "Option A",
                      icon: "Article",
                    },
                    {
                      code: "Category A.Option B",
                      name: "Option B",
                      icon: "Article",
                    },
                    {
                      code: "Category A.Option C",
                      name: "Option C",
                      icon: "Article",
                    },
                  ],
                  code: "Category A",
                },
                {
                  name: "Category B",
                  options: [
                    {
                      code: "Category B.Option 1",
                      name: "Option 1",
                      icon: "Article",
                    },
                    {
                      code: "Category B.Option 2",
                      name: "Option 2",
                      icon: "Article",
                    },
                    {
                      code: "Category B.Option 3",
                      name: "Option 3",
                      icon: "Article",
                    },
                  ],
                  code: "Category B",
                },
              ]} // options to be shown
              optionsKey={"code"} // key for the options
            ></MultiSelectDropdown>


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

<figure><img src="../../../../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Basic Dropdown</strong></p><p>A standard list of multiple checkboxes allowing users to select one or more options. Each selected option appears in the input field as a chip.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Categorical Dropdown</strong></p><p>Organises options under headings or categories, improving readability and helping users quickly locate desired items.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Nested Text Dropdown</strong></p><p>Presents each option with supporting secondary text or descriptions, ideal for selections that require additional context.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (6) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Profile Dropdown</strong></p><p>Options are displayed as user profiles (with avatar, name, etc.), allowing users to select multiple people or roles.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Profile with Nested Text Dropdown</strong></p><p>Combines profile visuals with supporting subtext.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (8) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Tree Dropdown</strong></p><p>Allows parent-child groupings with collapsible nodes, helpful in scenarios like selecting locations, organizational units, or tags with hierarchy.</p></td></tr></tbody></table>

***

## Interaction States

<table><thead><tr><th width="334.98046875"></th><th></th></tr></thead><tbody><tr><td><p><strong>Hover State</strong> </p><p>When the user hovers over the field or an item, it highlights to indicate interactivity and help the user discover selectable areas.</p></td><td><div><figure><img src="../../../../../.gitbook/assets/image (9) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><p><strong>Selected State</strong></p><p>Selected items are visually highlighted as rows inside the dropdown and as removable chips in the input field.</p></td><td><div><figure><img src="../../../../../.gitbook/assets/image (10) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td></tr></tbody></table>

## Properties

|                                                                                                                                                                                            |                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>Disabled</strong></p><p>Renders the dropdown non-interactive and visually muted. Used when the selection is temporarily or conditionally unavailable.</p>                       | <div><figure><img src="../../../../../.gitbook/assets/image (19) (1).png" alt=""><figcaption></figcaption></figure></div> |
| <p><strong>Error</strong> </p><p>Displays a red outline with an error message for validation feedback when the selection fails to meet the criteria.</p>                                   | <div><figure><img src="../../../../../.gitbook/assets/image (18) (1).png" alt=""><figcaption></figcaption></figure></div> |
| <p><strong>Non Editable</strong></p><p>Locks the field from further changes but still shows existing selections for reference.</p>                                                         | <div><figure><img src="../../../../../.gitbook/assets/image (17) (1).png" alt=""><figcaption></figcaption></figure></div> |
| <p><strong>Icon</strong></p><p>Shows a dropdown arrow or custom icons to indicate collapsibility and affordance.</p>                                                                       | <div><figure><img src="../../../../../.gitbook/assets/image (16) (1).png" alt=""><figcaption></figcaption></figure></div> |
| <p><strong>Label</strong></p><p>Text placed above the field to indicate the purpose or category of the dropdown.</p>                                                                       | <div><figure><img src="../../../../../.gitbook/assets/image (15) (1).png" alt=""><figcaption></figcaption></figure></div> |
| <p><strong>Help Text</strong></p><p>Optional guidance placed below the dropdown to clarify intent, usage, or rules.</p>                                                                    | <div><figure><img src="../../../../../.gitbook/assets/image (14) (1).png" alt=""><figcaption></figcaption></figure></div> |
| <p><strong>Select Users</strong></p><p>Allows users to quickly select or deselect all visible options within the dropdown. Especially useful in long or grouped lists.</p>                 | <div><figure><img src="../../../../../.gitbook/assets/image (13) (1).png" alt=""><figcaption></figcaption></figure></div> |
| <p><strong>Chips for Multi Select</strong></p><p>Each selected item is displayed as a dismissible chip within the collapsed field, providing a clear summary of the user's selections.</p> | <div><figure><img src="../../../../../.gitbook/assets/image (11) (1).png" alt=""><figcaption></figcaption></figure></div> |

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>options</td><td>text</td><td></td></tr><tr><td>optionsKey</td><td>text</td><td></td></tr><tr><td>selected</td><td>yes/no</td><td>no</td></tr><tr><td>onSelect</td><td>yes/no</td><td>no</td></tr><tr><td>onClose</td><td>number</td><td></td></tr><tr><td>defaultLabel</td><td>yes/no</td><td></td></tr><tr><td>defaultUnit</td><td>yes/no</td><td>no</td></tr><tr><td>props</td><td>yes/no</td><td>no</td></tr><tr><td>isPropsNeeded</td><td>yes/no</td><td>no</td></tr><tr><td>serverStyle</td><td>number</td><td>no</td></tr><tr><td>config</td><td>yes/no</td><td>no</td></tr><tr><td>disabled</td><td>text</td><td>no</td></tr><tr><td>variant</td><td>yes/no</td><td>no</td></tr><tr><td>addSelectAllCheck</td><td>yes/no</td><td></td></tr><tr><td>addCategorySelectAllCheck</td><td>yes/no</td><td></td></tr><tr><td>selectAllLabel</td><td>yes/no</td><td></td></tr><tr><td>categorySelectAllLabel</td><td>yes/no</td><td></td></tr><tr><td>restrictSelection</td><td>yes/no</td><td></td></tr><tr><td>isSearchable</td><td>yes/no</td><td></td></tr><tr><td>chipsKey</td><td>yes/no</td><td></td></tr><tr><td>frozenData</td><td>yes/no</td><td></td></tr><tr><td>handleViewMore</td><td>yes/no</td><td></td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>Title</td><td>String</td><td>required(if header is not passed)</td></tr><tr><td>Number</td><td>double</td><td>-</td></tr><tr><td>Icon</td><td>Icon widget</td><td>-</td></tr><tr><td>header</td><td>Widget</td><td>-</td></tr><tr><td>content</td><td>Widget</td><td>required</td></tr><tr><td>divider</td><td>bool</td><td>false</td></tr><tr><td>initiallyExpanded</td><td>bool</td><td>false</td></tr><tr><td>showBorder</td><td>bool</td><td>false</td></tr><tr><td>onToggle</td><td>VoidCallBack Function</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

***

## Behaviours

|                                                                                                                           |                                                                                                                                                                  |
| ------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (20) (1).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Chip Wrapping</strong></p><p>When multiple items are selected, the chips automatically wrap to a new line without breaking layout or readability.</p> |

***

## Usage Guide

***

| <p><strong>Use only for the selection of more than one</strong></p><p>Use the Dropdown – Multi Select when users need to choose multiple options from a list. It is ideal for scenarios like assigning roles, filtering data, or selecting categories.  If only one option needs to be selected, prefer using the Dropdown – Single Select for a simpler and more focused user experience.</p> | <p></p><p><img src="../../../../../.gitbook/assets/image (22) (1).png" alt=""></p>                                        |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
|                                                                                                                                                                                                                                                                                                                                                                                                | <div><figure><img src="../../../../../.gitbook/assets/image (23) (1).png" alt=""><figcaption></figcaption></figure></div> |

## Changelog

***

| Date         | Number  | Notes                                                                                           |
| ------------ | ------- | ----------------------------------------------------------------------------------------------- |
| Dec 15, 2024 | v-0.0.2 | <p>This component is added to the website.<br>This component is now individually versioned.</p> |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Writing guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
