---
description: Design System - Selection Tags component
---

# Selection Tags

Selection Tags are compact, button-like elements that allow users to make single or multiple selections from a set of options. They offer a clean and intuitive interaction pattern, ensuring a smooth and responsive user experience across form elements, filters, and grouped choices.

<figure><img src="../../../../../.gitbook/assets/image (11) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="Component React" %}
```
// Sample code

<SelectionTag
  allowMultipleSelection
  errorMessage=""
  onSelectionChanged={function noRefCheck(){}}
  options={[
    {
      code: 'option1',
      name: 'Option 1',
      prefixIcon: 'Edit',
      suffixIcon: 'Edit'
    },
    {
      code: 'option2',
      name: 'Option 2',
      prefixIcon: 'Edit',
      suffixIcon: 'Edit'
    },
    {
      code: 'option3',
      name: 'Option 3',
      prefixIcon: 'Edit',
      suffixIcon: 'Edit'
    }
  ]}
  selected={[]}
  width=""
/>


```
{% endtab %}

{% tab title="Component Flutter" %}
```
// Sample code

SelectionCard<String>(
                showParentContainer: withParentContainer,
                valueMapper: (item) => item,
                options: [
                  'Start',
                  'Middle',
                  'End',
                ],
                initialSelection: ['Start'],
                readOnly: true,
                onSelectionChanged: (newSelectedOptions) {
                  setState(() {
                    selectedOptions = List.from(newSelectedOptions);
                  });
                },
                equalWidthOptions: context.knobs
                    .boolean(label: 'Equal Width Options', initial: false),
                prefixIconBuilder: iconState != null
                    ? (value) {
                        if (iconState == 'iconAfterSelection') {
                          // Show icons only after selection
                          if (selectedOptions.contains(value)) {
                            if (value == 'Start') {
                              return Icons.star;
                            } else if (value == 'Middle') {
                              return Icons.favorite;
                            }
                            return Icons.thumb_down;
                          }
                          return null; // No icon if not selected
                        } else {
                          // Always show icons for each option
                          if (value == 'Start') {
                            return Icons.star;
                          } else if (value == 'Middle') {
                            return Icons.favorite;
                          }
                          return Icons.thumb_down;
                        }
                      }
                    : null,
                errorMessage: errorMessage.isNotEmpty ? errorMessage : null,
              );
```
{% endtab %}

{% tab title="Component Design" %}

{% endtab %}
{% endtabs %}

## Anatomy

<figure><img src="../../../../../.gitbook/assets/image (12) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (13) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Single Select</strong></p><p>Allows the user to choose only one option from the group. Once a selection is made, the previously selected option is deselected automatically. This variant is ideal for use cases like survey forms or filter selections.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (14) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Multi Select</strong></p><p>Enables users to select multiple options simultaneously. Commonly used where more than one input or category applies, such as skill filters, tag selectors, or custom checklists.</p></td></tr></tbody></table>

***

## Interaction States

<table><thead><tr><th width="334.98046875"></th><th></th></tr></thead><tbody><tr><td><p><strong>Active State</strong> </p><p>When a tag is selected, the background colour changes to primary. This state clearly communicates which options are currently selected.</p></td><td><div><figure><img src="../../../../../.gitbook/assets/image (15) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><p><strong>Dismiss on Mouse Out</strong></p><p>Tooltips disappear when the user moves away or loses focus, maintaining a clean and distraction-free interface.</p></td><td><div><figure><img src="../../../../../.gitbook/assets/image (17) (1) (1).png" alt=""><figcaption></figcaption></figure></div></td></tr></tbody></table>

## Properties

|                                                                                                                                                                                                                                                     |                                                                                                                               |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>Error</strong></p><p>It displays a red border around the tag container and shows a supporting error message below.<br>This is also used for validation states to indicate missing or incorrect selection(s).</p>                         | <div><figure><img src="../../../../../.gitbook/assets/image (20) (1) (1).png" alt=""><figcaption></figcaption></figure></div> |
| <p><strong>Prefix Icon</strong> </p><p>An icon placed to the left of the label text that helps convey additional context or function visually (e.g., an edit or status indicator).</p>                                                              | <div><figure><img src="../../../../../.gitbook/assets/image (19) (1) (1).png" alt=""><figcaption></figcaption></figure></div> |
| <p><strong>Suffix Icon</strong></p><p>An icon placed to the right of the label text that is typically used for actions like removal, more options, or tagging.</p>                                                                                  | <div><figure><img src="../../../../../.gitbook/assets/image (18) (1) (1).png" alt=""><figcaption></figcaption></figure></div> |
| <p><strong>Container Disabled</strong></p><p>Disables interaction with the entire selection group, and tags appear visually muted and do not respond to hover or click states. This is useful in forms where selection is conditionally locked.</p> | <div><figure><img src="../../../../../.gitbook/assets/image (21) (1) (1).png" alt=""><figcaption></figcaption></figure></div> |

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>width</td><td>text</td><td></td></tr><tr><td>errorMessage</td><td>text</td><td></td></tr><tr><td>options</td><td>yes/no</td><td>no</td></tr><tr><td>onSelectionChanged</td><td>yes/no</td><td>no</td></tr><tr><td>allowMultipleSelection</td><td>number</td><td></td></tr><tr><td>selected</td><td>yes/no</td><td></td></tr><tr><td>withContainer</td><td>yes/no</td><td>no</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>width</td><td>double</td><td>-</td></tr><tr><td>options</td><td>List&#x3C;T></td><td>required</td></tr><tr><td>title</td><td>String</td><td>-</td></tr><tr><td>onSelectionChanged</td><td>Function(List&#x3C;T>)</td><td>-</td></tr><tr><td>initialSelection</td><td>List&#x3C;T></td><td>-</td></tr><tr><td>allowMultipleSelection</td><td>bool</td><td>false</td></tr><tr><td>readOnly</td><td>bool</td><td>false</td></tr><tr><td>equalWidthOptions</td><td>bool</td><td>false</td></tr><tr><td>valueMapper</td><td>String Function(T)</td><td>-</td></tr><tr><td>prefixIconBuilder</td><td>IconData? Function(T)</td><td></td></tr><tr><td>suffixIconBuilder</td><td>IconData? Function(T)</td><td></td></tr><tr><td>showParentContainer</td><td>bool</td><td>true</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

***

## Behaviours

|                                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ----------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (23) (1) (1).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Use for exclusive choices</strong></p><p>Use selection tags when you need users to make clear, mutually exclusive choices or multiple selections. This ensures optimal visual hierarchy and helps users quickly understand their available options while maintaining a clean and organised interface layout.</p><p></p><p>Don't overcrowd the selection tag group with more than 4 options. Overwhelming users with too many choices makes it difficult for users to scan and compare options effectively.</p> |
| <div><figure><img src="../../../../../.gitbook/assets/image (24) (1) (1).png" alt=""><figcaption></figcaption></figure></div> |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |

***

## Usage Guide

***

| <div><figure><img src="../../../../../.gitbook/assets/image (42) (2).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Use for compact information display</strong></p><p>Keep tooltips concise and clear, limiting the text to one or two short sentences for quick readability.</p><p>Avoid adding actions or links in tooltips, as they should only provide passive information and appear on hover or keyboard focus.</p> |
| ------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (43) (2).png" alt=""><figcaption></figcaption></figure></div> |                                                                                                                                                                                                                                                                                                                   |

## Changelog

***

| Date         | Number  | Notes                                                                                           |
| ------------ | ------- | ----------------------------------------------------------------------------------------------- |
| Dec 15, 2024 | v-0.0.2 | <p>This component is added to the website.<br>This component is now individually versioned.</p> |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Writing guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
