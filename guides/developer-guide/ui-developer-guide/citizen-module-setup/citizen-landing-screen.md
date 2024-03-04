# Citizen Landing Screen

## Overview <a href="#description" id="description"></a>

This page provides details about how the Banner image and Citizen Services Card are rendered.

## Steps

### UI Implementation <a href="#ui-implementation" id="ui-implementation"></a>

The link to banner images and the labels and links of citizen services on the citizen services card are defined in the below MDMS file.

[egov-mdms-data/data/pb/common-masters/uiHomePage.json at DEV · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/common-masters/uiHomePage.json)

### Banner Image <a href="#banner-image" id="banner-image"></a>

For mobile and desktop we have different banner images link. We can change the images link on the below object

```
"appBannerDesktop":{
"code": "APP_BANNER_DESKTOP",
"name": "App Banner Desktop View",
"bannerUrl": "https://s3.ap-south-1.amazonaws.com/egov-qa-assets/app-banner-web.jpg", "enabled": true},
"appBannerMobile":{
"code": "APP_BANNER_MOBILE",
"name": "App Banner Mobile View",
"bannerUrl": "https://s3.ap-south-1.amazonaws.com/egov-qa-assets/app-banner-mobile.jpg", "enabled": true}
```

### Citizen Services Card/Information/Updates Props <a href="#citizen-services-card-and-information-and-updates-props" id="citizen-services-card-and-information-and-updates-props"></a>

Here we have two objects `citizenServicesCard` and `informationAndUpdatesCard`. Both of them have `sideOption` object which is a link to View All page.

`props` object contains the objects that we want to show on these two cards.

Change the label of the cards and add the navigation URL for each prop. Click on the card redirects users to the respective screen.

```
"citizenServicesCard":{
"code": "HOME_CITIZEN_SERVICES_CARD",
"name": "Home Citizen services Card",
"enabled": true,
"headerLabel": "DASHBOARD_CITIZEN_SERVICES_LABEL",
"sideOption": {
"name": "DASHBOARD_VIEW_ALL_LABEL",
"enabled": true,
"navigationUrl": "/digit-ui/citizen/all-services" },
"props": [
{
"code": "CITIZEN_SERVICE_PGR",
"name": "Complaints",
"label": "ES_PGR_HEADER_COMPLAINT",
"enabled": true,
"navigationUrl": "/digit-ui/citizen/pgr-home"},]},
```

### WhatsApp Banner Image / Link To WhatsApp Bot <a href="#whatsapp-banner-image-and-link-to-whatsapp-bot" id="whatsapp-banner-image-and-link-to-whatsapp-bot"></a>

Similar to Banner image, for WhatsApp Banner Image, we have two objects for mobile and desktop view. On click of the image it will redirect to WhatsApp bot. The redirection URL is defined in the navigation URL param.

```
"whatsAppBannerDesktop":{
"code": "WHATSAPP_BANNER_DESKTOP",
"name": "WhatsApp Banner Desktop View",
"bannerUrl": "https://s3.ap-south-1.amazonaws.com/egov-qa-assets/whatsapp-web.jpg", "enabled": true,
"navigationUrl": "https://api.whatsapp.com/send?phone=918744060444&text=mSeva"},
"whatsAppBannerMobile":{
"code": "WHATSAPP_BANNER_MOBILE",
"name": "WhatsApp Banner Mobile View",
"bannerUrl": "https://s3.ap-south-1.amazonaws.com/egov-qa-assets/whatsapp-mobile.jpg", "enabled": true,
"navigationUrl": "https://api.whatsapp.com/send?phone=918744060444&text=mSeva"}
```

Multiple options can be selected.

## Citizen Home Screen Configuration

Details about how the module cards are rendered in the Citizen Home screen and how to add a new Card.

### UI Implementation <a href="#ui-implementation" id="ui-implementation"></a>

All the modules that are enabled are defined in this file

[DIGIT-Dev/frontend/micro-ui/web/micro-ui-internals/example/src/index.js](https://github.com/egovernments/DIGIT-Dev/blob/67d1f4b925fa9f3ff28e80278e3e0e3cb951c929/frontend/micro-ui/web/micro-ui-internals/example/src/index.js)

```javascript
const enabledModules = [   "PGR",   "FSM",   "Payment",   "PT",   "QuickPayLinks",   "DSS",   "MCollect",   "HRMS",   "TL",   "Receipts",   "OBPS",   "Engagement",   "NOC",   "WS",   "CommonPT",   "NDSS",   "Bills", ];
```

This array contains a list of modules that are enabled in DIGIT-UI. This array is passed down to DigitUIWrapper Component defined here: [frontend/micro-ui/web/micro-ui-internals/packages/modules/core/src/Module.js](https://github.com/egovernments/DIGIT-Dev/blob/67d1f4b925fa9f3ff28e80278e3e0e3cb951c929/frontend/micro-ui/web/micro-ui-internals/packages/modules/core/src/Module.js). Here this array is passed down to this hook:

```
const { isLoading, data: initData } = Digit.Hooks.useInitStore(stateCode, enabledModules);
```

Now initData.modules will be containing an array of modules containing the following details about each module. Example object is shown here as PT module:

```
{ "module": "PT", "code": "PT", "bannerImage": "https://egov-qa-assets.s3.amazonaws.com/PT.png", "active": true, "order": 1, "tenants": [ { "code": "pb.jalandhar" }, { "code": "pb.nawanshahr" }, { "code": "pb.amritsar" } ] }
```

This array is further passed down to the CitizenHome component present in the file

[frontend/micro-ui/web/micro-ui-internals/packages/modules/core/src/components/Home.js](https://github.com/egovernments/DIGIT-Dev/blob/67d1f4b925fa9f3ff28e80278e3e0e3cb951c929/frontend/micro-ui/web/micro-ui-internals/packages/modules/core/src/components/Home.js)

This component will render a CitizenHomeCard component for every module that is present in the passed-down array of modules according to some conditions that are explained below.

#### How cards are rendered along with links and icons: <a href="#how-cards-are-rendered-along-with-links-and-icons" id="how-cards-are-rendered-along-with-links-and-icons"></a>

As you can see in the home screen of Citizen, every module card has some links for it. Details of those links is stored in MDMS so that it becomes configurable. In the UI those details are fetched and accordingly module cards are rendered with the information fetched from the MDMS.

This module card data is stored in this file [data/pb/ACCESSCONTROL-ACTIONS-TEST/actions-test.json](https://github.com/egovernments/egov-mdms-data/blob/4ca3f3244faafc75e03dc996269e2d248f5019ba/data/pb/ACCESSCONTROL-ACTIONS-TEST/actions-test.json). The format of the link data is described in such a way that every link object will have these key properties among others:

1. url → every link in the citizen side has this property set to “digit-ui-card”. It is used to filter all the links that belong to Citizen side
2. parentModule → describes to which module this link belongs
3. navigationURL → describes the destination url

In the UI this above mentioned data is fetched using this hook which calls this API `egov-mdms-service/v1/_search`.

```
const { isLoading: islinkDataLoading, data: linkData, isFetched: isLinkDataFetched } = Digit.Hooks.useCustomMDMS()
```

This hook call is made in this file [frontend/micro-ui/web/micro-ui-internals/packages/modules/core/src/pages/citizen/index.js](https://github.com/egovernments/DIGIT-Dev/blob/67d1f4b925fa9f3ff28e80278e3e0e3cb951c929/frontend/micro-ui/web/micro-ui-internals/packages/modules/core/src/pages/citizen/index.js)

After some processing in the UI this linkData will be an array in which every key will be module name and its value would be an object containing the links array and iconName and module Header, it will look like this:

Using this data every card along with it’s icon, header and links will be rendered in Citizen Home.

This rendering is done in this component [frontend/micro-ui/web/micro-ui-internals/packages/modules/core/src/components/Home.js](https://github.com/egovernments/DIGIT-Dev/blob/67d1f4b925fa9f3ff28e80278e3e0e3cb951c929/frontend/micro-ui/web/micro-ui-internals/packages/modules/core/src/components/Home.js) using CitizenHomeCard component.

**Icon Configuration / Naming Convention**

Every module icon is stored as an svg component in this file [svgindex.js](https://github.com/egovernments/DIGIT-Dev/blob/67d1f4b925fa9f3ff28e80278e3e0e3cb951c929/frontend/micro-ui/web/micro-ui-internals/packages/react-components/src/atoms/svgindex.js). Name of every svg component follows a common format which is the name of the module followed by Icon string. For instance, PTIcon is the icon name for PT module. This icon name details are also stored in the MDMS file, which is used to display appropriate icons on the module cards.

#### Add New Card <a href="#how-to-add-a-new-card" id="how-to-add-a-new-card"></a>

Now that we are aware of how the module cards are rendered with their respective data , let’s discuss how to add a new module Card.

To add a new module card , we need to add the name of the module in the list of enabled modules. The details of this module will be fetched using this same hook as explained above:

`const { isLoading, data: initData } = Digit.Hooks.useInitStore(stateCode, enabledModules);`

By doing this a new module card will be rendered but it’s header, links, and icon will not be rendered because we need to add this data in the MDMS. We need to add this data in this file as explained above [actions-test.json](https://github.com/egovernments/egov-mdms-data/blob/4ca3f3244faafc75e03dc996269e2d248f5019ba/data/pb/ACCESSCONTROL-ACTIONS-TEST/actions-test.json) and accordingly add matching ids in this file [roleactions.json](https://github.com/egovernments/egov-mdms-data/blob/41ee023689cca3d6ffe5c623b9326ac30479b6d6/data/pb/ACCESSCONTROL-ROLEACTIONS/roleactions.json) with rolecode property set to ‘CITIZEN’

**Sample actions-test and roleactions object**

**Sample actions-test object**

```
{ "id": 2307, "name": "BPA_CITIZEN_HOME_VIEW_APP_BY_CITIZEN_LABEL", "url": "digit-ui-card", "displayName": "View applications by Citizen", "orderNumber": 1, "parentModule": "OBPS", "enabled": true, "serviceCode": "", "code": "", "path": "", "navigationURL": "/digit-ui/citizen/obps/my-applications", "leftIcon": "OBPSIcon", "rightIcon": "", "queryParams": "" }
```

**Sample roleactions Object**

```
{ "rolecode": "CITIZEN", "actionid": 2307, "actioncode": "", "tenantId": "pb" }
```

Multiple options can be selected.\
