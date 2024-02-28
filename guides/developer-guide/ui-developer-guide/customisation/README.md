# Customisation

## Overview

This document provides the customisation details for DIGIT-UI. Customisation can be classified broadly into two types.

1. Overriding the Component/Hooks/CSS
2. Overwriting the required changes directly into the Micro-ui-internals

## Overriding

Overriding involves making all customization changes exclusively within the micro-ui/web directory.

#### For CSS

Within the custom CSS module, define customized CSS using the same class name or ID. Afterward, publish the changes. Ensure to reference this custom CSS file in the index.html to reflect the modifications on the website.

```
<link rel="stylesheet" href="https://unpkg.com/@egovernments/digit-ui-css@1.5.22/dist/index.css" />
<link rel="stylesheet" href="https://unpkg.com/@egovernments/digit-ui-custom-css@0.2.6/dist/index.css" />// Some code
```

#### For Components/Hooks

For overriding any components, re-register the same component in the same name in the customization folder. The latest changes are reflected.

## Overwriting Changes

Overwriting involves directly modifying the micro-ui-internals directory. This is slightly more challenging method to incorporate changes. Make sure the docker file is updated as per the code below and includes the install-deps.sh script.

````
```
dockerfile

RUN cd web/ \
    && node envs.js \
    &&  ./install-deps.sh \
    && yarn install \
    && yarn build 
```
````

The workspace in the web/package.json should be updated as below:

````
```json
 "workspaces": [
    "micro-ui-internals/packages/libraries",
    "micro-ui-internals/packages/react-components",
```
````

