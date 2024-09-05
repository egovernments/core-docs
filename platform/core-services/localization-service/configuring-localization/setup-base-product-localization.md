# Setup Base Product Localization

## Overview <a href="#overview" id="overview"></a>

The main reason to set up the. base product localization is because the DIGIT system supports multiple languages. By setting up Localization, we can have multiple language support for the UI. So, that user can easily understand the Digit Operations

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before you proceed with the configuration, make sure the following pre-requisites are met -

* Before starting the localization setup one should know the React and eGov FrameWork.
* Before setting up localization, make sure that all the keys are pushed to the Create API and also get prepared with the Values that need to be added to the Localization key specific to particular languages that are being added to the product.
* Make sure where to add the Localization in the Code.

## Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

Once the Localization is done, the user can view the DIGIT screens in the selected language. To complete the whole application process is easy since DIGIT UI allows the user to select the language of their choice.

## Deployment Details <a href="#deployment-details" id="deployment-details"></a>

* Once the key is added to the code as per requirement, the Deployment can be done in the same way as the code is deployed.

## Configuration Details <a href="#configuration-details" id="configuration-details"></a>

* Select a label that needs to be localized from the Product code. Here is the example code for a header before setting up Localization.

<figure><img src="../../../../.gitbook/assets/spaces_X13sH0e4xi7bV1juDmGX_uploads_5E0CgclMUoAYGb69A0lT_example-2.png" alt=""><figcaption></figcaption></figure>

* As we see the above which supports only the English language, To set up Localization to that header we need to the code in the following manner.

<figure><img src="../../../../.gitbook/assets/spaces_X13sH0e4xi7bV1juDmGX_uploads_t0oSQ4i438GPw7trhRc1_example-1 (1).png" alt=""><figcaption></figcaption></figure>

* we can see below code is added when we compare it with the code before the Localization setup.

{

labelName: "Trade Unit ",

labelKey: "TL\_NEW\_TRADE\_DETAILS\_TRADE\_UNIT\_HEADER"

},

* Here the Values to the key can be added by two methods - either by using the localization screen which was developed recently or by updating the values to the keys to create API using the Postman application.

### Reference Docs <a href="#reference-docs" id="reference-docs"></a>

#### Doc Links <a href="#doc-links" id="doc-links"></a>

| Title                                                                                                        | Link                                                                                                                                                                   |
| ------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Adding New Language to DIGIT System. You can refer to the link provided for how languages are added in DIGIT | [Adding New Language](https://urban.digit.org/platform/configure-digit/configuring-digit-services/configuring-common-services/setting-up-a-language/adding-a-language) |
