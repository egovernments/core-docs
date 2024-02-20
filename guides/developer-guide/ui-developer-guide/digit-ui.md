# DIGIT-UI

## Frontend Components <a href="#frontend-components" id="frontend-components"></a>

Broadly, the frontend components can be categorized as followings:

1. Libraries
2. CSS Library
3. React Components
4. UI Modules
5. Templates

<div align="left">

<figure><img src="../../../.gitbook/assets/image (8) (2).png" alt="" width="563"><figcaption><p>DIGIT UI</p></figcaption></figure>

</div>

### Nomenclature <a href="#nomenclature" id="nomenclature"></a>

The first line contains the Architecture Component name or info, the second line has npm-package and in the bracket, we have a template based on which the component will be created.

<div align="left">

<figure><img src="../../../.gitbook/assets/image (2) (1) (2).png" alt="" width="543"><figcaption><p>module naming convention</p></figcaption></figure>

</div>

### Features <a href="#features" id="features"></a>

* Easy-to-use CLI
* Handles all modern JS features
* Bundles `commonjs` and `es` module formats
* [create-react-app](https://github.com/facebookincubator/create-react-app) for example usage and local dev for React-based libraries
* [Rollup](https://rollupjs.org/) for bundling
* [Babel](https://babeljs.io/) for transpiling
* Supports complicated peer-dependencies
* Supports CSS modules

### Templates <a href="#templates" id="templates"></a>

The templates have the following folder structure:



The components related to the template are inside the `src` folder of the template and an example is created to use and showcase the app created by the template.

## Architecture <a href="#architecture" id="architecture"></a>

We have two main React Apps:

* `micro-ui-internals`&#x20;
  * Meant for the eGov development team to build components and default modules.
  * Contains the following modules:
    * CSS Library
    * UI Components (presently `react-components`)
    * Utils Library: Contains Services, Localization handling and React Hooks.
    * UI Modules
      * Core - containing login, routing and global state.
      * PGR
      * FSM
      * PT
      * Payment
      * etc ...
* `micro-ui`
  * Meant for the state team to manage, make changes, and deploy
  * Import `digit-ui-internals` modules.
  * Customizations
    * View
    * Services
  * Build and deploy scripts
    * Dockerfile & nginx.conf
    * build-config.yaml

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

### CSS Library

The CSS Library will have all the classes both in the module and compiled form.

<div align="left">

<figure><img src="../../../.gitbook/assets/Screenshot 2023-06-16 at 12.05.10 PM.png" alt="" width="521"><figcaption><p>css folder structure</p></figcaption></figure>

</div>

Can be imported like

`import "@egovernments/digit-ui.css/Button"`

or like this for full CSS import

`import "@egovernments/digit-ui.css"`

### Component Libraries <a href="#component-libraries" id="component-libraries"></a>

Component Library will have a set of all the required components defined in them.



<div align="left">

<figure><img src="../../../.gitbook/assets/Screenshot 2023-06-16 at 12.06.23 PM.png" alt="" width="540"><figcaption><p>react-components</p></figcaption></figure>

</div>

### Libraries and Utils <a href="#utils-library" id="utils-library"></a>

This will have the followings:

* LocalizationWorkflows
* API handling - API caching and handling strategies will be here, imported, and shared by all modules. Published as a function, can be used by anyone.
* Localisation

<div align="left">

<figure><img src="../../../.gitbook/assets/Screenshot 2023-06-16 at 12.07.18 PM.png" alt="" width="534"><figcaption><p>libraries</p></figcaption></figure>

</div>

&#x20;

### Modules <a href="#modules" id="modules"></a>

The module will be a black box for the states, they will only access throw `node_modules` or `CDN`. Any state-specific components can be passed during the initialization of the module inside the state’s employee or citizen app.

The modules structure will look like:

<div align="left">

<figure><img src="../../../.gitbook/assets/Screenshot 2023-06-16 at 12.09.36 PM.png" alt="" width="365"><figcaption><p>modules</p></figcaption></figure>

</div>

&#x20;

Modules will have the following inbuilt

* Theme - this may change if we later decide to use any `css-in-js` library, like `styled-components`.
* Components
* Routes
* State management
* Business logic
* API integrations

### Employee / Citizen App <a href="#employee-citizen-app" id="employee-citizen-app"></a>

The app will import the developed module.

`import './index.css' import { initPGR } from '@egovernments/pgr-module'; import punjabLogo from './assets/logo.png' const theme = { "--primary-color": "#3f51b5", "--text-color": "#212121" } const PGRComponents = { "logo": punjabLogo } const initPunjabPGR = (onRouteChange) => initPGR({ state: "pb", element: "#appWrapper", components: PGRComponents, onRouteChange, theme }); export default initPunjabPGR;`\


In the next phase, the Employee and Citizen app can be rewritten as a single app with the role and permissions-based rendering.\
\
[Prerequisite reference study materials](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/2269085701)

[Troubleshoot using Browser network Tab](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/2088009739)
