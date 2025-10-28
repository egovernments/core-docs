---
description: Design System - Header component
---

# Header

The Header component establishes a clear and consistent identity. Designed with accessibility and responsiveness in mind, the Header serves as a navigation anchor, contextual identifier, and personalisation hub. It ensures that users always know where they are, can quickly change settings like language or city, and recognise the governing body or service brand in view.

<figure><img src="../../../../../.gitbook/assets/image (511).png" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="Component React" %}
```
// Sample code

 <Header
      actionFields={[
        <ChangeCity dropdown={true} t={t} />,
        showLanguageChange && <ChangeLanguage dropdown={true} />,
        userDetails?.access_token && (
          <Dropdown
            option={userOptions}
            optionKey="name"
            profilePic={profilePic ? profilePic : userDetails?.info?.name || userDetails?.info?.userInfo?.name || "Employee"}
            select={handleUserDropdownSelection}
            showArrow={true}
            menuStyles={{ marginTop: "1rem" }}
            theme="light"
          />
        ),
      ]}
      onHamburgerClick={() => {
        toggleSidebar();
      }}
      className="digit-employee-header"
      img={logoUrl}
      logoWidth={"64px"}
      logoHeight={"48px"}
      logo={(loggedin ? cityDetails?.logoId : stateInfo?.statelogo)||DEFAULT_EGOV_LOGO}
      onImageClick={() => {}}
      onLogoClick={() => {}}
      props={{}}
      showDeafultImg
      style={{}}
      theme="light"
      ulb={
        loggedin ? (
          cityDetails?.city?.ulbGrade ? (
            <>
              {t(cityDetails?.i18nKey).toUpperCase()}{" "}
              {t(`ULBGRADE_${cityDetails?.city?.ulbGrade.toUpperCase().replace(" ", "_").replace(".", "_")}`).toUpperCase()}
            </>
          ) : (
            <ImageComponent className="state" src={logoUrlWhite} alt="State Logo" />
          )
        ) : (
          <>
            {t(`MYCITY_${stateInfo?.code?.toUpperCase()}_LABEL`)} {t(`MYCITY_STATECODE_LABEL`)}
          </>
        )
      }
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

<figure><img src="../../../../../.gitbook/assets/image (512).png" alt=""><figcaption></figcaption></figure>

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (513).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Light Mode</strong></p><p>A minimal white background header suited for daylight or bright-themed interfaces. It keeps the focus on the primary page content while maintaining clear brand visibility.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (514).png" alt=""><figcaption></figcaption></figure></div></td><td><strong>Dark Mode</strong><br>A bolder visual variant is typically used in high-contrast interfaces. Ideal for mobile or dashboard environments where visual hierarchy is important.</td></tr></tbody></table>

## Properties

<table data-header-hidden data-full-width="false"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Customise Name</strong><br>The name of the platform, department, or app can be tailored, making the header reusable across multiple services or city implementations. <br></td><td><div><figure><img src="../../../../../.gitbook/assets/image (515).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><p><strong>Language Selector</strong></p><p>Supports multilingual use by allowing users to change the interface language dynamically from the header.</p></td><td><div><figure><img src="../../../../../.gitbook/assets/image (516).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><p><strong>City Selection Dropdown</strong></p><p>Allows users to switch between different cities or localities, ensuring content and services stay relevant to the chosen jurisdiction.</p></td><td><div><figure><img src="../../../../../.gitbook/assets/image (517).png" alt=""><figcaption></figcaption></figure></div></td></tr></tbody></table>

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>wrapperClassName</td><td>text</td><td>-</td></tr><tr><td>headerContentClassName</td><td>text</td><td>-</td></tr><tr><td>caption</td><td>yes/no</td><td>no</td></tr><tr><td>captionClassName</td><td>yes/no</td><td>no</td></tr><tr><td>header</td><td>number</td><td>-</td></tr><tr><td>headerClasName</td><td>yes/no</td><td>-</td></tr><tr><td>subHeader</td><td>yes/no</td><td>no</td></tr><tr><td>subHeaderClasName</td><td>yes/no</td><td>no</td></tr><tr><td>body</td><td>yes/no</td><td>no</td></tr><tr><td>bodyClasName</td><td>number</td><td>no</td></tr><tr><td>style</td><td>yes/no</td><td>no</td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>Title</td><td>String</td><td>required(if header is not passed)</td></tr><tr><td>Number</td><td>double</td><td>-</td></tr><tr><td>Icon</td><td>Icon widget</td><td>-</td></tr><tr><td>header</td><td>Widget</td><td>-</td></tr><tr><td>content</td><td>Widget</td><td>required</td></tr><tr><td>divider</td><td>bool</td><td>false</td></tr><tr><td>initiallyExpanded</td><td>bool</td><td>false</td></tr><tr><td>showBorder</td><td>bool</td><td>false</td></tr><tr><td>onToggle</td><td>VoidCallBack Function</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

## Usage Guide

| <div><figure><img src="../../../../../.gitbook/assets/image (518).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Contrast Adaptation</strong></p><p>Use appropriate variants (Light/Dark) depending on the surrounding UI theme to ensure optimal readability and visual harmony with the interface environment.  Don't use the same header variant across different background contexts, as this creates poor contrast and reduces visibility when the header colour doesn't properly complement the surrounding theme.</p> |
| ---------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div><figure><img src="../../../../../.gitbook/assets/image (519).png" alt=""><figcaption></figcaption></figure></div> |                                                                                                                                                                                                                                                                                                                                                                                                                        |

## Change log

***

| Date         | Number  | Notes                                                                                           |
| ------------ | ------- | ----------------------------------------------------------------------------------------------- |
| Dec 15, 2024 | v-0.0.2 | <p>This component is added to the website.<br>This component is now individually versioned.</p> |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Content guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
