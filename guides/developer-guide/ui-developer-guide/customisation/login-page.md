---
description: Configuration of privacy policy component on the login screen
---

# Login Page

## Overview

A new feature, the Privacy Component, has been added to the login screen to enhance user transparency. This component displays privacy policy information based on the login configuration. Follow the steps below to configure this component on the login screen.

## Steps

### Integrate With Login Configuration

To render the Privacy Component, you must include specific configurations in the MDMS :

* **Master Name:** `commonUiConfig`
* **Module Name:** `LoginConfig`

If these configurations are not present, the [default login](login-page.md#default-screen) configuration will be rendered instead.

### Filter Privacy Data&#x20;

The content displayed within the Privacy Component's pop-up will be filtered according to the `module code` specified in the schema.&#x20;

### Customise Login Fields

The fields on the login screen are fully configurable. Users can add or remove fields according to their specific requirements.&#x20;

### Set Login Button&#x20;

To ensure all mandatory fields are completed, the login button will be disabled until all required fields are filled. This ensures that users provide all necessary information before proceeding.

### Example Configurations

Here are some examples of different configurations for the login screen and their corresponding displays:

These configs will help to enable/disable the privacy declaration, at an instance level.&#x20;

{% tabs %}
{% tab title="Config without Privacy Declaration" %}
Screen:

<figure><img src="../../../../.gitbook/assets/image (329).png" alt=""><figcaption><p>Login screen</p></figcaption></figure>

Config:

```javascript
"inputs": [
                  {
                      "label": "CORE_LOGIN_USERNAME",
                      "type": "text",
                      "key": "username",
                      "isMandatory": true,
                      "populators": {
                          "name": "username",
                          "validation": {
                              "required": true
                          },
                          "error": "ERR_USERNAME_REQUIRED"
                      }
                  },
                  {
                      "label": "CORE_LOGIN_PASSWORD",
                      "type": "password",
                      "key": "password",
                      "populators": {
                          "name": "password",
                          "validation": {
                              "required": true
                          },
                          "error": "ERR_PASSWORD_REQUIRED"
                      },
                      "isMandatory": true
                  }
              ]
```
{% endtab %}

{% tab title="Config with Privacy Declaration" %}
Screen:

<figure><img src="../../../../.gitbook/assets/image (331).png" alt=""><figcaption><p>Login screen</p></figcaption></figure>

Config: \


```javascript
[
                  {
                      "label": "CORE_LOGIN_USERNAME",
                      "type": "text",
                      "key": "username",
                      "isMandatory": true,
                      "populators": {
                          "name": "username",
                          "validation": {
                              "required": true
                          },
                          "error": "ERR_USERNAME_REQUIRED"
                      }
                  },
                  {
                      "label": "CORE_LOGIN_PASSWORD",
                      "type": "password",
                      "key": "password",
                      "populators": {
                          "name": "password",
                          "validation": {
                              "required": true
                          },
                          "error": "ERR_PASSWORD_REQUIRED"
                      },
                      "isMandatory": true
                  },
                  {
                      "isMandatory": false,
                      "key": "check",
                      "type": "component",
                      "component": "PrivacyComponent",
                      "withoutLabel": true,
                      "disable": false,
                      "customProps": {
                          "module": "HCM"
                      },
                      "populators": {
                          "name": "check"
                      }
                  }
              ]

```
{% endtab %}
{% endtabs %}

#### Default Screen :

<figure><img src="../../../../.gitbook/assets/image (328).png" alt=""><figcaption><p>login screen</p></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/Screenshot from 2024-08-27 12-29-48.png" alt=""><figcaption><p>Privacy policy pop up</p></figcaption></figure>

**Data Customisation:** The data can be modified through MDMS and localization updates.\
\
**MDMS Path:** \
[Login Configuration](https://github.com/egovernments/egov-mdms-data/blob/UNIFIED-DEV/data/mz/commonUIConfig/LoginConfig.json)\
\
[Privacy policy schema](https://github.com/egovernments/egov-mdms-data/blob/UNIFIED-DEV/data/mz/commonUIConfig/PrivacyPolicy.json)\
\
[Click here](https://github.com/egovernments/DIGIT-Frontend/blob/develop/micro-ui/web/micro-ui-internals/packages/modules/core/src/components/PrivacyComponent.js) to access the privacy component file.

**Localisation modules used:**&#x20;

[digit-privacy-policy](https://docs.google.com/spreadsheets/d/1XY0OYiLsC1eKHeD-WpQv6GV7Sxiy2LHR9KoeVz95q2o/edit?gid=1511586820#gid=1511586820)&#x20;

[rainmaker-common](https://docs.google.com/spreadsheets/d/1XY0OYiLsC1eKHeD-WpQv6GV7Sxiy2LHR9KoeVz95q2o/edit?gid=51685018#gid=51685018)
