# Create Screen (FormComposer)

## Overview

This page provides the steps to configure the FormComposer.

## Configuration Details

For complex configuration or screen details refer to documentation on[ Utility - preprocess](../customisation/utility-pre-process-mdms-config.md)

### Other Variants (FormComposerV2)

There are 3 new use cases added to the FormComposer in addition to the default one where the whole form was rendered in a single card. Those 2 are the following:

* Multiple cards
* Cards with navigation menu
* Multiple cards with navigation menu on a single card

The following use cases are covered in the [DIGIT-WORKS repo](https://github.com/egovernments/DIGIT-Works).&#x20;

URL to access:/works-ui/employee/works/sampleForm

### Multiple Cards <a href="#multiple-cards" id="multiple-cards"></a>

This can be done by setting the `showMultipleCards` prop to the FormComposer as true. In this case, every object in the formConfig will be treated as a separate Card and will be rendered accordingly.

Access [Config Link](https://github.com/egovernments/DIGIT-Works/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/works/src/pages/employee/Checklist/configTest.js).

<figure><img src="../../../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

### Cards With Navigation Menu <a href="#cards-with-navigation-menu" id="cards-with-navigation-menu"></a>

FormComposer provides the option to activate a navigation menu that appears on top of the card. Each link in the menu corresponds to a specific card. To enable this feature, provide an array configuration for the navigation menu as a prop to the FormComposer component. Then, map each card with a link from the navigation menu configuration array using a designated key named "navLink", associating it with a value in the Navigation Menu Config.

Access [Configuration link](https://github.com/egovernments/DIGIT-Works/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/works/src/pages/employee/Checklist/configTest.js).

<figure><img src="../../../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

### Multiple Cards With Navigation Menu On A Single Card <a href="#multiple-cards-with-navigation-menu-on-a-single-card" id="multiple-cards-with-navigation-menu-on-a-single-card"></a>

This use case is the same as above. The only difference is the `navLink` property in the config. If this property is present and valid for a card config, the corresponding card will be mapped to a navigation menu link. On the other hand, if `navLink` is not present or invalid, the corresponding card will be rendered as a separate Card.

Multiple options can be selected.

<figure><img src="../../../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>
