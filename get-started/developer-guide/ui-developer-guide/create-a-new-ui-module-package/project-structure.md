---
description: Front-end module project structure
---

# Project Structure

## Overview

Before starting with the  Module code, ensure your local development environment is set up. You can refer to the local development setup guide link given below for detailed instructions.

[Local-Development-Setup](https://core.digit.org/guides/developer-guide/ui-developer-guide/local-development-setup)

## Steps

{% hint style="info" %}
Download the UI code from the link here [Digit-Frontend](https://github.com/egovernments/Digit-Frontend). if not done earlier
{% endhint %}

&#x20; Follow the steps given below to create the project structure.

1. Once you have cloned the repository from Digit-Frontend, do the following.
2. Go to `micro-ui-internals → packages → modules`.&#x20;
3. Create a new folder with module's name , For example (**Sample**).&#x20;
4. Create a folder called **src** and add the **components** , **configs**, **hooks** and **pages** inside that.
5. The project structure should be as in the image below:

<div align="left">

<figure><img src="../../../../.gitbook/assets/image (3).png" alt="" width="351"><figcaption></figcaption></figure>

</div>

6. After creating the new `Sample` module, we need to create a `package.json` file for the module, specifying the module name, version, scripts, and required dependencies.

```json
{
  "name": "@egovernments/digit-ui-module-sample",
  "version": "0.0.1",
  "description": "Sample Module UI",
  "main": "dist/index.js",
  "module": "dist/index.modern.js",
  "source": "src/Module.js",
  "files": [
    "dist"
  ],
  "scripts": {
    "start": "microbundle-crl watch --no-compress --format modern,cjs",
    "build": "microbundle-crl --compress --no-sourcemap --format cjs",
    "prepublish": "yarn build"
  },
  "peerDependencies": {
    "react": "17.0.2",
    "react-router-dom": "5.3.0"
  },
  "dependencies": {
    "@egovernments/digit-ui-react-components": "1.8.2-beta.5",
    "@egovernments/digit-ui-components": "0.0.2-beta.1",
    "react": "17.0.2",
    "react-date-range": "^1.4.0",
    "react-dom": "17.0.2",
    "react-hook-form": "6.15.8",
    "react-i18next": "11.16.2",
    "react-query": "3.6.1",
    "react-router-dom": "5.3.0"
  },
  "author": "Jagankumar <jagan.kumar@egov.org.in>",
  "license": "MIT"
}
```

Refer to the file here - [Package.json](https://github.com/egovernments/DIGIT-Frontend/blob/sample/micro-ui/web/micro-ui-internals/packages/modules/sample/package.json)

The next step is to initialise the Dependency, refer [here](install-dependency.md) to learn more about the setup
