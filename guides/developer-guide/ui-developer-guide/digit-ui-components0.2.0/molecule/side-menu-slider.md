---
description: Design System - Side Panel component
---

# Side Panel

The Side Panel component serves as a supplementary container to present contextual or detailed information without navigating away from the current screen. It follows the principles of progressive disclosure and allows for efficient multitasking.

<figure><img src="../../../../../.gitbook/assets/image (542).png" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="Component React" %}
```
// Sample code

<SidePanel type="dynamic" position="right" defaultOpenWidth={300} defaultClosedWidth={64} header={<h3>Menu Header</h3>} footer={<p>Footer Content</p>} sections={[<p>Section 1</p>, <p>Section 2</p>]} closedContents={<p>Compact View</p>} isDraggable={true} > <p>Main Content Here</p> </SidePanel>
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

<figure><img src="../../../../../.gitbook/assets/image (543).png" alt=""><figcaption></figcaption></figure>

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (544).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Default/Static</strong></p><p>Displays structured content in a fixed panel with optional action buttons and a header. Commonly used for static information display and secondary actions.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (545).png" alt=""><figcaption></figcaption></figure></div></td><td><strong>Collapsible/Dynamic</strong><br>Features include expandable/collapsible sections with a toggle arrow. Useful for longer content or when managing dense interfaces while maintaining a clean layout.</td></tr></tbody></table>

## Properties

<table data-header-hidden data-full-width="false"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Sections</strong><br>Supports multiple vertical sections for chunking information logically; each section can include headers, content, and actions.<br></td><td><div><figure><img src="../../../../../.gitbook/assets/image (546).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Action Buttons</strong><br>Supports primary or secondary buttons at the bottom of each section or the entire panel to initiate actions like Submit, Save, or Next.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (547).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Header</strong><br>Contains a title and optional subheading. Can include a close (X) icon for dismissing the panel.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (548).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Arrow alignment - Left/Right</strong><br>The collapse/expand arrow can be positioned on either side of the panel based on the UI layout and reading direction.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (549).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Collapse by arrow</strong> <br>The panel can be dynamically collapsed into a thin strip, showing only the header or icon, and expanded with a click on the arrow.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (550).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><p><strong>Close Button</strong></p><p>Optional close (X) button at the top-right for dismissing or hiding the panel when needed</p></td><td><div><figure><img src="../../../../../.gitbook/assets/image (551).png" alt=""><figcaption></figcaption></figure></div></td></tr></tbody></table>

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>className</td><td>text</td><td>-</td></tr><tr><td>styles</td><td>text</td><td>-</td></tr><tr><td>type</td><td>yes/no</td><td>no</td></tr><tr><td>position</td><td>yes/no</td><td>no</td></tr><tr><td>children</td><td>yes/no</td><td>-</td></tr><tr><td>header</td><td>yes/no</td><td>-</td></tr><tr><td>footer</td><td>yes/no</td><td>no</td></tr><tr><td>addClose</td><td>yes/no</td><td>no</td></tr><tr><td>closedContents</td><td>yes/no</td><td>no</td></tr><tr><td>closedSections</td><td>yes/no</td><td>no</td></tr><tr><td>closedHeader</td><td>yes/no</td><td>no</td></tr><tr><td>closedFooter</td><td>yes/no</td><td>no</td></tr><tr><td>transitionDuration</td><td>yes/no</td><td>no</td></tr><tr><td>bgActive</td><td>yes/no</td><td>no</td></tr><tr><td>isOverlay</td><td>yes/no</td><td>no</td></tr><tr><td>isDraggable</td><td>yes/no</td><td>no</td></tr><tr><td>sections</td><td>yes/no</td><td>no</td></tr><tr><td>hideArrow</td><td>yes/no</td><td>no</td></tr><tr><td>hideScrollIcon</td><td>yes/no</td><td>no</td></tr><tr><td>defaultOpenWidth</td><td>yes/no</td><td>no</td></tr><tr><td>defaultClosedWidth</td><td>yes/no</td><td>no</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>Title</td><td>String</td><td>required(if header is not passed)</td></tr><tr><td>Number</td><td>double</td><td>-</td></tr><tr><td>Icon</td><td>Icon widget</td><td>-</td></tr><tr><td>header</td><td>Widget</td><td>-</td></tr><tr><td>content</td><td>Widget</td><td>required</td></tr><tr><td>divider</td><td>bool</td><td>false</td></tr><tr><td>initiallyExpanded</td><td>bool</td><td>false</td></tr><tr><td>showBorder</td><td>bool</td><td>false</td></tr><tr><td>onToggle</td><td>VoidCallBack Function</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

## Usage Guide

***

| <div><figure><img src="../../../../../.gitbook/assets/image (552).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Action accessibility</strong></p><p>Use the collapsible variant for panels that need to show or hide sections based on user interaction.  Don't keep long sections always expanded; it can overwhelm the user visually.</p> |
| ---------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (553).png" alt=""><figcaption></figcaption></figure></div> |                                                                                                                                                                                                                                        |

## Change log

***

<table><thead><tr><th width="200.4765625">Date</th><th width="155">Number</th><th>Notes</th></tr></thead><tbody><tr><td>Dec 15, 2024</td><td>v-0.0.2</td><td>This component is added to the website.<br>This component is now individually versioned.</td></tr></tbody></table>

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Content guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
