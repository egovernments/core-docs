# CSS Customisation

## **Overview**

This document describes how to publish CSS if there are any CSS Customization/changes. While customising, if any changes are made In the CSS folder it has to be compiled and published to npm.

## Customisation Steps

Currently, the CSS is published in npm as **@egovernments/digit-ui-css**&#x20;

Refer to the NPM link here - [digit-ui-css](https://www.npmjs.com/package/@egovernments/digit-ui-css).

So any changes to the CSS folder locally must be published in different organisations and in the same or different package name. For example - @xyz/digit-ui-css and version 1.0.0 then the following changes have to be made in the code to reflect in the digit-ui

​[index.html](https://github.com/egovernments/DIGIT-Works/blob/master/frontend/micro-ui/web/public/index.html) - file location

_**frontend/micro-ui/web/public/index.html**_

The style sheet link must be updated as follows,

`<link rel="stylesheet" href="https://unpkg.com/@xyz/digit-ui-css@1.0.0/dist/index.css"/>`

Use either of the following commands to publish the CSS

* In the `frontend/micro-ui/web/micro-ui-internals` folder run `yarn run publish:css` or
* In the `frontend/micro-ui/web/micro-ui-internals/packages/css` folder run `yarn run publish --access public`

There are two ways to customize the CSS -

1. Override the required CSS only without changing in the CSS folder and making changes only in the custom CSS folder. Both CSS will be present in the index.html the order of the package mentioned in the HTML determines which CSS needs to be taken ie the box mentioned in the last will have more precedence. example of overriding CSS as follow - [index.html](https://github.com/egovernments/DIGIT-Works/blob/9fbd790b6136261d538dd14fcd63b3a9061cc6c9/frontend/micro-ui/web/public/index.html#L10)
2. Overwrite the complete existing CSS.

{% hint style="info" %}
**Note:** If there is overwriting of the complete CSS, future upgrades will need manual work to take the upgrade/difference changes.
{% endhint %}

**Reference** doc for publishing any package to npm -

​[​![](https://docs.npmjs.com/favicon-32x32.png?v=f44ec608ba91563f864a30a276cd9065)Creating and publishing scoped public packages | npm Docs](https://docs.npmjs.com/creating-and-publishing-scoped-public-packages)​
