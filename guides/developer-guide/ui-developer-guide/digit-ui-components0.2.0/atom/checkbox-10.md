---
description: Design System - Loader component
---

# Loader

The Loader component is a fundamental UI element. It visually communicates ongoing processes such as data fetching, form submission, or navigation transitions. The loader helps set user expectations by indicating that a background action is in progress, reducing uncertainty and improving perceived performance.

<figure><img src="../../../../../.gitbook/assets/image (491).png" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="Component React" %}
```
// Sample code

<Loader variant={"PageLoader"}/>

<Loader variant={"OverlayLoader"}/>
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

<figure><img src="../../../../../.gitbook/assets/image (493).png" alt=""><figcaption></figcaption></figure>

***

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (494).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Default</strong></p><p>A simple spinner with optional loading text. Typically used for inline or section-based loading indicators.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (495).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Page Loader</strong></p><p>A fullscreen loader that appears during full-page transitions or major data loads, ensuring users are aware of system-level activity.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (496).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Overlay Loader</strong></p><p>Appears over existing content with a dimmed background. Ideal for actions like uploading media or submitting forms, preventing user interaction during processing.</p></td></tr></tbody></table>

***

## Properties

|                                                                                                                                                                  |                                                                                                                        |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| <p><strong>Loader Text</strong></p><p>Optional text (e.g., "Loading...") can be displayed alongside the spinner to clarify the ongoing process for the user.</p> | <div><figure><img src="../../../../../.gitbook/assets/image (497).png" alt=""><figcaption></figcaption></figure></div> |

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>variant</td><td>text</td><td></td></tr><tr><td>className</td><td>text</td><td></td></tr><tr><td>style</td><td>yes/no</td><td>no</td></tr><tr><td>loaderText</td><td>yes/no</td><td>no</td></tr><tr><td>animationStyles</td><td>number</td><td></td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>Title</td><td>String</td><td>required(if header is not passed)</td></tr><tr><td>Number</td><td>double</td><td>-</td></tr><tr><td>Icon</td><td>Icon widget</td><td>-</td></tr><tr><td>header</td><td>Widget</td><td>-</td></tr><tr><td>content</td><td>Widget</td><td>required</td></tr><tr><td>divider</td><td>bool</td><td>false</td></tr><tr><td>initiallyExpanded</td><td>bool</td><td>false</td></tr><tr><td>showBorder</td><td>bool</td><td>false</td></tr><tr><td>onToggle</td><td>VoidCallBack Function</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

***

## Behaviours

|                                                                                                                        |                                                                                                                                                                                                |
| ---------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (498).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Blocks Interaction</strong></p><p>While the loader is active, especially in page or overlay mode, user interaction is restricted to avoid conflicting inputs during processing.</p> |
| <div><figure><img src="../../../../../.gitbook/assets/image (499).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Auto Dismiss</strong></p><p>Loaders are dismissed automatically upon completion of the associated process, ensuring smooth transitions and minimising wait perception.</p>          |

***

## Usage Guide

***

| <p><strong>Use loaders for content that is loading</strong></p><p>Use medium or large loaders for content that is loading in large areas, without space constraints, such as web pages, panels, or dashboards.  </p><p></p><p>Avoid using small loaders for full-page or overlay loading, as they may not be noticeable or may seem visually unbalanced.</p> | <div><figure><img src="../../../../../.gitbook/assets/image (500).png" alt=""><figcaption></figcaption></figure></div> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------- |
|                                                                                                                                                                                                                                                                                                                                                              | <div><figure><img src="../../../../../.gitbook/assets/image (501).png" alt=""><figcaption></figcaption></figure></div> |

## Changelog

***

| Date         | Number  | Notes                                                                                           |
| ------------ | ------- | ----------------------------------------------------------------------------------------------- |
| Dec 15, 2024 | v-0.0.2 | <p>This component is added to the website.<br>This component is now individually versioned.</p> |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Writing guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
