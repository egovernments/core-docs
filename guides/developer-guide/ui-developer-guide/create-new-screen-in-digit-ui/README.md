---
description: New Screen in Digit-ui
---

# Create New Screen In DIGIT-UI

## Overview

This document provides the steps for creating the new screen in the DIGIT-UI.

## Steps

Creating a screen in DIGIT UI is simple and it can be classified into 4 types of screens -

1. [Create](./#create-screen)
2. [View](./#view-screen)
3. [Inbox](./#inbox-screen)
4. [Search](./#search-screen)

### **Create Screen**

To create any new screen of the Create type, use the **FormcomposerV2** and transmit the configuration as specified in the [sample.js](https://github.com/jagankumar-egov/DIGIT-OSS/blob/Ui-Dev-Certification/frontend/micro-ui/web/micro-ui-internals/packages/modules/br/src/pages/employee/Sample.js) file.&#x20;

To check the different types of configurations, refer to the [`fieldSelector`](https://github.com/egovernments/DIGIT-OSS/blob/92018d43fb0cdf8929f4a66dc61857af8cdc5140/frontend/micro-ui/web/micro-ui-internals/packages/react-components/src/hoc/FormComposerV2.js#L128) function.

### View Screen

To use any view screen, create the hook for initiating API calls and structure the configurations for the View section.&#x20;

* Refer to the integrated screen with ApplicationDetailsTemplate - [ViewProperty.js](https://github.com/egovernments/DIGIT-OSS/blob/master/frontend/micro-ui/web/micro-ui-internals/packages/modules/commonPt/src/pages/pageComponents/ViewProperty.js).
* The hook details for the same is mentioned in [useGenericViewProperty](https://github.com/egovernments/DIGIT-OSS/blob/master/frontend/micro-ui/web/micro-ui-internals/packages/libraries/src/hooks/pt/useGenericViewProperty.js).js
* The service configuration details are available in [Search.js](https://github.com/egovernments/DIGIT-OSS/blob/master/frontend/micro-ui/web/micro-ui-internals/packages/libraries/src/services/molecules/PT/Search.js)

### Inbox Screen

To create any inbox screen, use the **InboxComposer** and add the following configurations:&#x20;

* Main file: [EdcrInbox](https://github.com/egovernments/DIGIT-OSS/blob/master/frontend/micro-ui/web/micro-ui-internals/packages/modules/obps/src/pages/citizen/EdcrInbox/index.js)
* Check the [folder](https://github.com/egovernments/DIGIT-OSS/tree/master/frontend/micro-ui/web/micro-ui-internals/packages/modules/obps/src/pages/citizen/EdcrInbox) which contains other configs like filter, table, search, and mobile responsiveness.
* The hook for the same is defined in [useEDCRInbox.js](https://github.com/egovernments/DIGIT-OSS/blob/master/frontend/micro-ui/web/micro-ui-internals/packages/libraries/src/hooks/obps/useEDCRInbox.js)
* Use the latest [InboxSearchComposer](inbox-search-screen.md) (InboxV2)
* Both Inbox and Search screens can be shown based on the input configurations passed to that component - [BillInbox.js](https://github.com/egovernments/DIGIT-Works/blob/master/frontend/micro-ui/web/micro-ui-internals/packages/modules/Expenditure/src/pages/employee/Bills/BillInbox.js)
* Configuration are mentioned in [InboxConfig](https://github.com/egovernments/DIGIT-Works/blob/master/frontend/micro-ui/web/micro-ui-internals/packages/modules/Expenditure/src/configs/InboxBillConfig.js) for local reference and it is fetched from the MDMS [BillInboxConfig](https://github.com/egovernments/works-mdms-data/blob/DEV/data/pg/commonMuktaUiConfig/InboxBillConfig.json).

### Search Screen

An example for Search screen is available in [SearchConfig](https://github.com/egovernments/works-mdms-data/blob/DEV/data/pg/commonMuktaUiConfig/SearchBillWMSConfig.json).
