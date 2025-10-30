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

<FilterCard
  addClose
  equalWidthButtons
  layoutType="vertical"
  onClose={function noRefCheck(){}}
  onPrimaryPressed={function noRefCheck(){}}
  onSecondaryPressed={function noRefCheck(){}}
  primaryActionLabel="ApplyFilters"
  secondaryActionLabel="Clear Filters"
  title="Filter"
>
  <LabelFieldPair vertical>
    <TextBlock body="Name" />
    <TextInput type="text" />
  </LabelFieldPair>
  <LabelFieldPair vertical>
    <TextBlock body="Value" />
    <TextInput type="text" />
  </LabelFieldPair>
  <LabelFieldPair vertical>
    <TextBlock body="Gender" />
    <RadioButtons
      alignVertical
      name="gender"
      onSelect={function noRefCheck(){}}
      options={[
        {
          code: 'M',
          name: 'Male'
        },
        {
          code: 'F',
          name: 'Female'
        },
        {
          code: 'O',
          name: 'Others'
        }
      ]}
      optionsKey="name"
      style={{
        width: '100%'
      }}
    />
  </LabelFieldPair>
</FilterCard>

```
{% endtab %}

{% tab title="Component Flutter" %}
```
// Sample code

FilterCard.buildFilterCard(
        context: context,
        title: 'Filter Options',
        contentList: [
          LabeledField(
              label: 'Text Field',
              labelInline: false,
              child: DigitTextFormInput(
                controller: TextEditingController(),
              )),
          LabeledField(
            label: 'Search Field',
            labelInline: false,
            child: DigitSearchFormInput(
              controller: TextEditingController(),
            ),
          ),
        ],
        secondaryActionLabel: 'clear filters',
        onSecondaryPressed: (){},
        primaryActionLabel: 'Apply Filters',
        onPrimaryPressed: () {
          // Handle the button press
          // For example, you might want to save the selected filters
          print('Filters applied!');
        },
        layoutType: FilterCardLayout.vertical,
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
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>context</td><td>BuildContext</td><td>required</td></tr><tr><td>title</td><td>String</td><td>-</td></tr><tr><td>layoutType</td><td>FilterCardLayout</td><td>FilterCardLayout.horizontal</td></tr><tr><td>titleIcon</td><td>IconData</td><td>-</td></tr><tr><td>contentList</td><td>List&#x3C;Widget></td><td>-</td></tr><tr><td>primaryActionLabel</td><td>String</td><td>-</td></tr><tr><td>secondaryActionLabel</td><td>String</td><td>-</td></tr><tr><td>onPrimaryPressed</td><td>VoidCallback</td><td>-</td></tr><tr><td>onSecondaryPressed</td><td>VoidCallback</td><td>-</td></tr><tr><td>barrierDismissible</td><td>bool</td><td>true</td></tr></tbody></table>
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

| Date         | Number  | Notes                                                                                           |
| ------------ | ------- | ----------------------------------------------------------------------------------------------- |
| Dec 15, 2024 | v-0.0.2 | <p>This component is added to the website.<br>This component is now individually versioned.</p> |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Content guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
