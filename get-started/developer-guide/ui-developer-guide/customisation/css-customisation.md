# CSS Customisation

## **Overview**

This page explores the steps to publish CSS if there are any CSS Customization/changes. While customising, if any changes are made In the CSS folder it has to be compiled and published to npm.

## Steps

Currently, the CSS is published in npm as **@egovernments/digit-ui-css**

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

​[​<img src="https://docs.npmjs.com/favicon-32x32.png?v=f44ec608ba91563f864a30a276cd9065" alt="" data-size="line">Creating and publishing scoped public packages | npm Docs](https://docs.npmjs.com/creating-and-publishing-scoped-public-packages)

***

**Note:** The CSS has also been migrated from **Node 14** to **Node 20**. The most significant change in this process was transitioning the build system from **Gulp** to **Webpack**. You can find the Webpack configuration file here:

```
const path = require("path");
const MiniCssExtractPlugin = require("mini-css-extract-plugin");
const CssMinimizerPlugin = require("css-minimizer-webpack-plugin");
const TerserPlugin = require("terser-webpack-plugin");
const fs = require("fs");

// Read package.json metadata for banner
const { name, version, author } = JSON.parse(fs.readFileSync("package.json", "utf8"));

const header = `
@charset "UTF-8";
/*!
 * ${name} - ${version}
 *
 * Copyright (c) ${new Date().getFullYear()} ${author}
 */
`;

module.exports = {
  mode: process.env.NODE_ENV === "production" ? "production" : "development",

  entry: {
    styles: "./src/index.scss",
  },

  output: {
    path: path.resolve(__dirname, process.env.NODE_ENV === "production" ? "dist" : "example"),
    filename: "[name].js", // CSS is extracted separately
    clean: true,
  },

  module: {
    rules: [
      {
        test: /\.(scss|css)$/,
        use: [
          MiniCssExtractPlugin.loader,
          {
            loader: "css-loader",
            options: { importLoaders: 1 },
          },
          {
            loader: "postcss-loader",
            options: {
              postcssOptions: require("./postcss.config"),
            },
          },
          "sass-loader",
        ],
      },
    ],
  },

  optimization: {
    minimize: process.env.NODE_ENV === "production",
    minimizer: [
      new CssMinimizerPlugin(),
      new TerserPlugin(),
    ],
  },

  plugins: [
    new MiniCssExtractPlugin({
      filename: "index.css",
    }),
    {
      apply: (compiler) => {
        compiler.hooks.emit.tap("AddHeaderPlugin", (compilation) => {
          for (const name in compilation.assets) {
            if (name.endsWith(".css")) {
              const source = compilation.assets[name].source();
              compilation.assets[name] = {
                source: () => header + source,
                size: () => Buffer.byteLength(header + source, "utf8"),
              };
            }
          }
        });
      },
    },
  ],

  devServer: {
    static: path.resolve(__dirname, "example"),
    hot: true,
    port: 3000,
    open: true,
    watchFiles: ["src/**/*.scss"],
  },
};
```

NPM package [link](../../../../guides/developer-guide/ui-developer-guide/digit-ui-components0.2.0/) for latest css version after upgrade.
