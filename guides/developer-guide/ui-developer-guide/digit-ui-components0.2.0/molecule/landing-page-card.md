---
description: Design System - Landing Page component
---

# Landing Page Card

The Landing Page Card component serves as a navigational entry point, combining visual elements, summary data, and contextual menus. Built on principles of clarity, responsiveness, and customizability, this component helps users explore modules efficiently while displaying key actions and metrics upfront.

<figure><img src="../../../../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="Component React" %}
```
// Sample code

<LandingPageCard
  buttonSize="medium"
  centreChildren={[
    <div>Here you can add any text content between metrics and links</div>
  ]}
  endChildren={[
    <div>Here you can add any text content below links</div>
  ]}
  icon="SupervisorAccount"
  links={[
    {
      icon: 'Person',
      label: 'Create User',
      link: 'https://unified-dev.digit.org/storybook/?path=/story/atoms-backlink--primary'
    },
    {
      icon: 'Edit',
      label: 'Edit User',
      link: 'https://unified-dev.digit.org/storybook/?path=/story/atoms-backlink--primary'
    },
    {
      icon: 'Preview',
      label: 'View User',
      link: 'https://unified-dev.digit.org/storybook/?path=/story/atoms-backlink--primary'
    },
    {
      icon: 'Delete',
      label: 'Delete User',
      link: 'https://unified-dev.digit.org/storybook/?path=/story/atoms-backlink--primary'
    }
  ]}
  metrics={[
    {
      count: 40,
      label: 'Lorem Ipsum',
      link: 'https://unified-dev.digit.org/storybook/?path=/story/atoms-backlink--primary'
    },
    {
      count: 40,
      label: 'Lorem Ipsum',
      link: 'https://unified-dev.digit.org/storybook/?path=/story/atoms-backlink--primary'
    }
  ]}
  moduleName="Dashboards"
  onMetricClick={function noRefCheck(){}}
  style={{}}
  variation="one"
/>
```
{% endtab %}

{% tab title="Component Flutter" %}
```
// Sample code

MatrixListComponent(
            alignCenterMatrixList: true,
            icon: Icons.supervisor_account,
            filledIcon: true,
            showIconOnRight: true,
            heading: 'Heading',
            matrixList: [
              MatrixModel(
                  title: '30', description: 'Description of Matrix 1'),
              MatrixModel(
                  title: '30', description: 'Description of Matrix 2'),
            ] ,
            actions: [
              ActionItem(label: 'Action 1', icon: Icons.edit, onPressed: () {}),
              ActionItem(label: 'Action 2', icon: Icons.edit, onPressed: () {}),
            ],
            additionalWidget: const InfoCard(
              title: 'this is a custom widget',
              type: InfoType.info,
              description: 'which provide details about the card',
            ),
          ),
```
{% endtab %}

{% tab title="Component Design" %}

{% endtab %}
{% endtabs %}

## Anatomy

<figure><img src="../../../../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Default</strong></p><p>Displays a card with module title, optional icon, metrics, and a list of menu actions. It supports responsiveness across desktop, tablet, and mobile viewports.</p></td></tr></tbody></table>

## Properties

<table data-header-hidden data-full-width="false"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Icon</strong><br>Supports both filled and unfilled icon styles, customizable based on visual priority or branding needs.<br></td><td><div><figure><img src="../../../../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Icon Alignment</strong><br>Icons can be aligned either on the left (standard) or right (for visual distinction or emphasis).</td><td><div><figure><img src="../../../../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Metrics</strong><br>Cards can optionally show numerical data summaries to give quick insights.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Custom Content</strong><br>Custom text or widgets (like contextual notes) can be injected into the card to enrich the layout.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><strong>Menu Items</strong><br>Actionable items like Create User, Edit User, or Delete User can be toggled based on user roles or module-specific permissions.</td><td><div><figure><img src="../../../../../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure></div></td></tr></tbody></table>

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}


<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>icon</td><td>text</td><td>-</td></tr><tr><td>moduleName</td><td>text</td><td>-</td></tr><tr><td>moduleAlignment</td><td>yes/no</td><td>no</td></tr><tr><td>metrics</td><td>yes/no</td><td>no</td></tr><tr><td>metricAlignment</td><td></td><td>-</td></tr><tr><td>links</td><td>yes/no</td><td>-</td></tr><tr><td>className</td><td>yes/no</td><td>no</td></tr><tr><td>style</td><td>yes/no</td><td>no</td></tr><tr><td>index</td><td>number</td><td>no</td></tr><tr><td>hideDivider</td><td>yes/no</td><td>no</td></tr><tr><td>iconBg</td><td>yes/no</td><td>no</td></tr><tr><td>buttonSize</td><td>yes/no</td><td>no</td></tr><tr><td>onMetricClick</td><td>yes/no</td><td>no</td></tr><tr><td>centreChildren</td><td>yes/no</td><td>no</td></tr><tr><td>endChildren</td><td>yes/no</td><td>no</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>heading</td><td>String</td><td>required</td></tr><tr><td>matrixList</td><td>List&#x3C;MatrixModel></td><td>-</td></tr><tr><td>Icon</td><td>IconData</td><td>-</td></tr><tr><td>actions</td><td>List&#x3C;ActionItem></td><td>-</td></tr><tr><td>centerWidget</td><td>Widget</td><td>required</td></tr><tr><td>additionalWidget</td><td>Widget</td><td>-</td></tr><tr><td>filledIcon</td><td>bool</td><td>true</td></tr><tr><td>alignCenterMatrixList</td><td>bool</td><td>false</td></tr><tr><td>showIconOnRight</td><td>bool</td><td>false</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

## Usage Guide

***

| <div><figure><img src="../../../../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Hierarchical structure</strong></p><p>Enable tree selection for complex apps where submodules need to be grouped contextually.  Don’t flatten deep hierarchies if users need to frequently access child modules—it hinders navigation efficiency.</p> |
| --------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure></div> |                                                                                                                                                                                                                                                                  |

## Change log

***

| Date         | Number  | Notes                                                                                           |
| ------------ | ------- | ----------------------------------------------------------------------------------------------- |
| Dec 15, 2024 | v-0.0.2 | <p>This component is added to the website.<br>This component is now individually versioned.</p> |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Content guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
