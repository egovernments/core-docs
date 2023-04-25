---
description: Setting up localisation strings
---

# Localisation Module

## Overview

This guide goes through inserting basic localisation for core DIGIT modules post-installation. Currently, localisation is an extra step post-install. We enter localisation data in bulk via REST API calls. [Postman collection](https://www.postman.com/collections/a140e7426ab4419ed5b5) is available to facilitate this process.

## Localisation Structure - Brief

The [releasekit](https://github.com/egovernments/releasekit/tree/master/localisation) repository contains all the localisation strings separated per module.

Base localisation strings are provided in the baseline folder. Localization is done per module per release. New strings in each release are contained in the respective release version folder. Depending on what modules have been installed, the localization strings have to be collated and then seeded using Postman Scripts.

For example, if DIGIT v2.7 with the PGR module has been installed, the localization strings for the PGR module have to be collated in the following order in JSON:

1. Baseline localization strings
2. v2.3
3. v2.4
4. v2.5
5. v2.6
6. v2.7

For convenience, a consolidated JSON file per module is created with each release under the [consolidated folder](https://github.com/egovernments/releasekit/tree/master/localisation/consolidated). To add the messages, copy the json string of one module and paste it into the body of the [JSON request](https://www.getpostman.com/collections/082221e70ad98af9877b) and hit upsert. Repeat this for each module.

## Localisation Setup&#x20;

1. Download the [postman collection](https://www.postman.com/collections/a140e7426ab4419ed5b5) - Setup an environment in postman and add the following variables:
   * authToken&#x20;
   * tenantId
2. Login to DIGIT as a citizen user from the browser. To get auth token on your webpage, right-click and go to Inspect > Network > payload > RequestInfo. Here you will find a variable named authToken which will be a 32-bit string. Paste it in the values field of the `authToken` variable in Postman and click "Save".
3. Run the “Insert Localization” script after adding the required localization messages for each module from [releasekit consolidated folder](https://github.com/egovernments/releasekit/tree/master/localisation/consolidated/en\_IN) in the Postman script body.&#x20;

{% hint style="info" %}
Run each module separately. Else, the server will throw a 40x error.&#x20;
{% endhint %}

The modules to set up depending on what has been installed as part of DIGIT. For the DIGIT core, we require localisation to be set up for the user module.&#x20;

| Module    | Localization folder                                                                                         |
| --------- | ----------------------------------------------------------------------------------------------------------- |
| egov-user | [localization/digit\_core](https://github.com/egovernments/releasekit/tree/master/localisation/digit\_core) |

* Search endpoint: _domain_/localization/messages/v1/\_search
* Upsert endpoint: _domain_/localization/messages/v1/\_upsert
