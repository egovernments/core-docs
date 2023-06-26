---
description: New Screen in Digit-ui
---

# Create a New Screen in Digit-ui

## Overview

This document says about the creation of new screen in the digit-ui

Creating a Simple Screen in DIgit UI Is made simple and it can be classified into 4 types of screens

1. Create
2. View
3. Inbox
4. Search

### **Create Screen:**

While Creating any new screen of type Create, we will use a **FormcomposerV2** and send the config as mentioned in the

[sample.js](https://github.com/jagankumar-egov/DIGIT-OSS/blob/Ui-Dev-Certification/frontend/micro-ui/web/micro-ui-internals/packages/modules/br/src/pages/employee/Sample.js) file

To check the different types of config refer [`fieldSelector`](https://github.com/egovernments/DIGIT-OSS/blob/92018d43fb0cdf8929f4a66dc61857af8cdc5140/frontend/micro-ui/web/micro-ui-internals/packages/react-components/src/hoc/FormComposerV2.js#L128) function.

### View Screen:

For using any view screen the hook has to be created for making API call and form the config for the View Part

\
Check the screen integrated with **ApplicationDetailsTemplate**\
\
[ViewProperty.js](https://github.com/egovernments/DIGIT-OSS/blob/master/frontend/micro-ui/web/micro-ui-internals/packages/modules/commonPt/src/pages/pageComponents/ViewProperty.js)

the hook for the same is mentioned in

[useGenericViewProperty](https://github.com/egovernments/DIGIT-OSS/blob/master/frontend/micro-ui/web/micro-ui-internals/packages/libraries/src/hooks/pt/useGenericViewProperty.js).js

the service where the config mentioned is detailed in

[Search.js](https://github.com/egovernments/DIGIT-OSS/blob/master/frontend/micro-ui/web/micro-ui-internals/packages/libraries/src/services/molecules/PT/Search.js)

### Inbox Screen

For creating any inbox screen we have this **InboxComposer** to which the following configurations must be added.\
Main file: [EdcrInbox](https://github.com/egovernments/DIGIT-OSS/blob/master/frontend/micro-ui/web/micro-ui-internals/packages/modules/obps/src/pages/citizen/EdcrInbox/index.js)

Check the following [folder](https://github.com/egovernments/DIGIT-OSS/tree/master/frontend/micro-ui/web/micro-ui-internals/packages/modules/obps/src/pages/citizen/EdcrInbox) which contains other configs like filter, table, search, and mobile responsiveness,

The hook for the same is defined in [useEDCRInbox.js](https://github.com/egovernments/DIGIT-OSS/blob/master/frontend/micro-ui/web/micro-ui-internals/packages/libraries/src/hooks/obps/useEDCRInbox.js)



Using the Latest [InboxSearchComposer](inbox-search-screen.md) (InboxV2),

Both Inbox and Search screens can be shown based on the input config passed to that component\
\
[BillInbox.js](https://github.com/egovernments/DIGIT-Works/blob/master/frontend/micro-ui/web/micro-ui-internals/packages/modules/Expenditure/src/pages/employee/Bills/BillInbox.js)\
Config is mentioned in [InboxConfig](https://github.com/egovernments/DIGIT-Works/blob/master/frontend/micro-ui/web/micro-ui-internals/packages/modules/Expenditure/src/configs/InboxBillConfig.js) for local reference and it will be fetched from the mdms [BillInboxConfig](https://github.com/egovernments/works-mdms-data/blob/DEV/data/pg/commonMuktaUiConfig/InboxBillConfig.json)

An example for Search screen would be [SearchConfig](https://github.com/egovernments/works-mdms-data/blob/DEV/data/pg/commonMuktaUiConfig/SearchBillWMSConfig.json)\
\
