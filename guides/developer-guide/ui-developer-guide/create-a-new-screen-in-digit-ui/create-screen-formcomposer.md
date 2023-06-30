# Create Screen (FormComposer)

## Overview

This document provides details about the FormComposer and the steps to configure it.

//Need to add more details

## Configuration Details

For Complex Config or screen \
Refer to documentation on[ Utility - preprocess](../customisation/utility-pre-process-mdms-config.md)

### Other Variants (FormComposerV2)

There are 3 new use cases added to the FormComposer in addition to the default one where the whole form was rendered in a single card. Those 2 are the following:

* Multiple Cards
* Cards with Navigation Menu
* Multiple Cards with Navigation Menu on a single Card

The following use cases are covered in the DIGIT-WORKS repo:

[GitHub - egovernments/DIGIT-Works](https://github.com/egovernments/DIGIT-Works)

URL to access:/works-ui/employee/works/sampleForm

### Multiple Cards <a href="#multiple-cards" id="multiple-cards"></a>

This can be done by setting the `showMultipleCards` prop to the FormComposer as true. In this case, every object in the formConfig will be treated as a separate Card and will be rendered accordingly.

config Link → [DIGIT-Works/frontend/micro-ui/web/micro-ui-internals/packages/modules/works/src/pages/employee/Checklist/configTest1.js at develop · egovernments/DIGIT-Works](https://github.com/egovernments/DIGIT-Works/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/works/src/pages/employee/Checklist/configTest1.js)

<figure><img src="../../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

### Cards With Navigation Menu <a href="#cards-with-navigation-menu" id="cards-with-navigation-menu"></a>

A navigation menu can be enabled in the FormComposer which will be rendered on top of the card and it will render an appropriate card for every navigation link in the menu. This can be enabled by sending an array config for the Navigation Menu as a prop to the FormComposer and mapping each card with a link in the Navigation Menu config array using a key called `navLink` and set this key to a value in Navigation Menu Config.

Config Link → [DIGIT-Works/frontend/micro-ui/web/micro-ui-internals/packages/modules/works/src/pages/employee/Checklist/configTest.js at develop · egovernments/DIGIT-Works](https://github.com/egovernments/DIGIT-Works/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/works/src/pages/employee/Checklist/configTest.js)

<figure><img src="../../../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

### Multiple Cards With Navigation Menu On A Single Card <a href="#multiple-cards-with-navigation-menu-on-a-single-card" id="multiple-cards-with-navigation-menu-on-a-single-card"></a>

This use case is the same as above. The only difference will be the `navLink` property in the config. If this property is present and valid for a Card config, the corresponding card will be mapped to a Navigation Menu Link. On the other hand, if `navLink` If not present or invalid, the corresponding card will be rendered as a separate Card.

Multiple options can be selected.

<figure><img src="../../../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>
