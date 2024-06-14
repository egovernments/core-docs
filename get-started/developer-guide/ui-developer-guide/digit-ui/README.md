---
description: Key components of DIGIT-UI
---

# DIGIT-UI

## Overview <a href="#frontend-components" id="frontend-components"></a>

This page provides the architecture and key features of the DIGIT UI. Click on the broader headings below to find the details.

* [Frontend components](./#frontend-components-1)
* [UI Architecture](./#architecture)
* [Employee/Citizen App](./#employee-citizen-app)

## Frontend Components <a href="#frontend-components" id="frontend-components"></a>

Broadly, the DIGIT UI frontend components are categorized as below:

1. [Libraries](./#css-library)
2. [CSS Library](./#css-library)
3. [React Components](./#component-libraries)
4. [UI Modules](./#modules)
5. [Templates](./#templates)

<div align="left">

<figure><img src="../../../../.gitbook/assets/image (11).png" alt="" width="563"><figcaption><p>DIGIT UI</p></figcaption></figure>

</div>

### CSS Library

The CSS Library contains all the classes both in the module and compiled form.

<div align="left">

<figure><img src="../../../../.gitbook/assets/Screenshot 2023-06-16 at 12.05.10 PM.png" alt="" width="521"><figcaption><p>css folder structure</p></figcaption></figure>

</div>

This can be imported using `import "@egovernments/digit-ui.css/Button"`

or full CSS import using `import "@egovernments/digit-ui.css"`

### Component Libraries <a href="#component-libraries" id="component-libraries"></a>

Component Library contains a set of all the required components defined in them.

<div align="left">

<figure><img src="../../../../.gitbook/assets/Screenshot 2023-06-16 at 12.06.23 PM.png" alt="" width="540"><figcaption><p>react-components</p></figcaption></figure>

</div>

### Libraries & Utils <a href="#utils-library" id="utils-library"></a>

These contain the following:

* Localization workflows
* API handling - API caching and handling strategies will be here, imported, and shared by all modules. Published as a function, can be used by anyone.
* Localisation

<div align="left">

<figure><img src="../../../../.gitbook/assets/Screenshot 2023-06-16 at 12.07.18 PM.png" alt="" width="534"><figcaption><p>libraries</p></figcaption></figure>

</div>

### Modules <a href="#modules" id="modules"></a>

The module will function as a closed system for the states, limiting their access to node\_modules or CDNs only. Any components specific to a state can be provided during the module's initialization within the employee or citizen application's state.

Below is an illustration of how the modules structure looks like:

<div align="left">

<figure><img src="../../../../.gitbook/assets/Screenshot 2023-06-16 at 12.09.36 PM.png" alt="" width="365"><figcaption><p>modules</p></figcaption></figure>

</div>

Modules contain the following inbuilt

* Theme - this may change if we later decide to use any `css-in-js` library, like `styled-components`.
* Components
* Routes
* State management
* Business logic
* API integrations

### Nomenclature <a href="#nomenclature" id="nomenclature"></a>

1. The first line contains the Architecture Component name or info
2. The second line has npm-package and in the bracket there is a template based on which the component will be created.

<div align="left">

<figure><img src="../../../../.gitbook/assets/image (306).png" alt="" width="543"><figcaption><p>module naming convention</p></figcaption></figure>

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

The templates have the following folder structure: The components related to the template are inside the `src` folder of the template and an example is created to use and showcase the app created by the template.

## Architecture <a href="#architecture" id="architecture"></a>

We have two main React Apps:

1. `micro-ui-internals`&#x20;
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
2. `micro-ui`
   * Meant for the state team to manage, make changes, and deploy
   * Import `digit-ui-internals` modules
   * Customizations
     * View
     * Services
   * Build and deploy scripts
     * Dockerfile & nginx.conf
     * build-config.yaml

<figure><img src="../../../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Employee / Citizen App <a href="#employee-citizen-app" id="employee-citizen-app"></a>

The app imports the developed module.

```
import './index.css' import { initPGR } from '@egovernments/pgr-module'; import punjabLogo from './assets/logo.png' const theme = { "--primary-color": "#3f51b5", "--text-color": "#212121" } const PGRComponents = { "logo": punjabLogo } const initPunjabPGR = (onRouteChange) => initPGR({ state: "pb", element: "#appWrapper", components: PGRComponents, onRouteChange, theme }); export default initPunjabPGR;
```

In the next phase, the Employee and Citizen app can be rewritten as a single app with the role and permissions-based rendering.

## Related Links

\
[Prerequisite reference study materials](../../pre-requisites-training-resources.md)

[Troubleshoot using Browser network Tab](../faqs/troubleshoot-using-browser-network-tab.md)
