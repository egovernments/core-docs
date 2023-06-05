# Customisation

## Overview

This document says about the customisation of Digit-UI. Customisation can be classified broadly into two types.

1. Overriding the Component/Hooks/Css
2. Overwriting the required changes directly into the Micro-ui-internals

### Overriding

Overriding is how to make all the customization changes only in the micro-ui/web directory.

#### For CSS:

In the custom CSS module, with the same class name or ID define the customized CSS and publish. Mention this in the index.html to reflect changes in the website

```
<link rel="stylesheet" href="https://unpkg.com/@egovernments/digit-ui-css@1.5.22/dist/index.css" />
<link rel="stylesheet" href="https://unpkg.com/@egovernments/digit-ui-custom-css@0.2.6/dist/index.css" />// Some code
```

#### For Components/Hooks:

For overriding any components, re-register the same component in the same name in the customization folder. The latest changes are reflected.

### Overwriting Changes

Overwriting is the other way of Customisation, where the changes were directly made in the micro-ui-internals directory, by this way taking the latest changes will be slightly harder.

So while overwriting the docker file should be updated as follows and must include install-deps.sh

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

The workspace in the web/package.json should be updated as follows:

````
```json
 "workspaces": [
    "micro-ui-internals/packages/libraries",
    "micro-ui-internals/packages/react-components",
```
````

