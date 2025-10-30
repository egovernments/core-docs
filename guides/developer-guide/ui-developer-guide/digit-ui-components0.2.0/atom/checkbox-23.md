---
description: Design System - Textblock component
---

# Textblock

The Text Block component provides a structured typographic layout, combining various levels of hierarchy such as headings, subheadings, captions, and descriptions. It ensures clarity, consistency, and adaptability in presenting textual information across different screens and use cases.

<figure><img src="../../../../../.gitbook/assets/image (502).png" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="Component React" %}
```
// Sample code
<TextBlock caption="Note" header="Important Information" subHeader="Please read carefully" body="Make sure to follow the guidelines." wrapperClassName="custom-wrapper" captionClassName="custom-caption" headerClasName="custom-header" subHeaderClasName="custom-subheader" bodyClasName="custom-body" />
```
{% endtab %}

{% tab title="Component Flutter" %}
```
// Sample code
DigitTextBlock(
          caption: 'Caption Text',
          heading: 'Heading',
          subHeading: 'Sub heading',
          description: 'This is the description of the TextBlock component.',
        ),
```
{% endtab %}

{% tab title="Component Design" %}

{% endtab %}
{% endtabs %}

## Anatomy

<figure><img src="../../../../../.gitbook/assets/image (503).png" alt=""><figcaption></figcaption></figure>

***

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (504).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Default</strong></p><p>The default Text Block displays a structured combination of a caption, heading, subheading, and description. Each section can be individually toggled on or off based on the context or content requirement.</p></td></tr></tbody></table>

***

## Properties

|                                                                                                                                                                                  |                                                                                                                        |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| <p><strong>Heading Label</strong></p><p>Displays a prominent title or main heading. Turning this off removes the main visual anchor of the text block.</p>                       | <div><figure><img src="../../../../../.gitbook/assets/image (505).png" alt=""><figcaption></figcaption></figure></div> |
| <p><strong>Subheading Label</strong> </p><p>Adds supporting information below the heading. Can be turned off to simplify the text hierarchy.</p>                                 | <div><figure><img src="../../../../../.gitbook/assets/image (506).png" alt=""><figcaption></figcaption></figure></div> |
| <p><strong>Caption Label</strong> </p><p>Offers a small label above the heading, often used for categorization or section labeling.</p>                                          | <div><figure><img src="../../../../../.gitbook/assets/image (507).png" alt=""><figcaption></figcaption></figure></div> |
| <p><strong>Description Label</strong> </p><p>Provides a detailed explanation or contextual information below the subheading. Turning it off results in a more compact block.</p> | <div><figure><img src="../../../../../.gitbook/assets/image (508).png" alt=""><figcaption></figcaption></figure></div> |

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>wrapperClassName</td><td>text</td><td></td></tr><tr><td>headerContentClassName</td><td>text</td><td></td></tr><tr><td>caption</td><td>yes/no</td><td>no</td></tr><tr><td>captionClassName</td><td>yes/no</td><td>no</td></tr><tr><td>header</td><td>number</td><td></td></tr><tr><td>headerClasName</td><td>yes/no</td><td></td></tr><tr><td>subHeader</td><td>yes/no</td><td>no</td></tr><tr><td>subHeaderClasName</td><td>yes/no</td><td>no</td></tr><tr><td>body</td><td>yes/no</td><td>no</td></tr><tr><td>bodyClasName</td><td>number</td><td>no</td></tr><tr><td>style</td><td>yes/no</td><td>no</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>caption</td><td>String</td><td>-</td></tr><tr><td>captionStyle</td><td>TextStyle</td><td>-</td></tr><tr><td>heading</td><td>String</td><td>-</td></tr><tr><td>headingStyle</td><td>TextStyle</td><td>-</td></tr><tr><td>subHeading</td><td>String</td><td>-</td></tr><tr><td>subHeadingStyle</td><td>TextStyle</td><td>-</td></tr><tr><td>description</td><td>String</td><td>-</td></tr><tr><td>descriptionStyle</td><td>TextStyle</td><td>-</td></tr><tr><td>padding</td><td>EdgeInsets</td><td>-</td></tr><tr><td>spacing</td><td>double</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

***

## Usage Guide

***

| <p><strong>Use Textblocks for Clear and Structured Content</strong></p><p>Use Textblocks to present readable, well-organised text with proper hierarchy (e.g., headings, subheadings, and body).  </p><p></p><p>Never use Textblocks inconsistently or without a logical structure.</p> | <div><figure><img src="../../../../../.gitbook/assets/image (509).png" alt=""><figcaption></figcaption></figure></div> |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
|                                                                                                                                                                                                                                                                                         | <div><figure><img src="../../../../../.gitbook/assets/image (510).png" alt=""><figcaption></figcaption></figure></div> |

## Changelog

***

| Date         | Number  | Notes                                                                                           |
| ------------ | ------- | ----------------------------------------------------------------------------------------------- |
| Dec 15, 2024 | v-0.0.2 | <p>This component is added to the website.<br>This component is now individually versioned.</p> |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Writing guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
