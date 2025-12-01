---
description: Front-end module project structure
---

# Project Structure

{% tabs %}
{% tab title="React17(legacy)" %}
## Overview

Before starting with the Module code, ensure your local development environment is set up. You can refer to the local development setup guide link given below for detailed instructions.

[Local-Development-Setup](https://core.digit.org/guides/developer-guide/ui-developer-guide/local-development-setup)

## Steps

{% hint style="info" %}
Download the UI code from the link here [Digit-Frontend](https://github.com/egovernments/Digit-Frontend). if not done earlier
{% endhint %}

Follow the steps given below to create the project structure.

1. Once you have cloned the repository from Digit-Frontend, do the following.
2. Go to `micro-ui-internals → packages → modules`.
3. Create a new folder with module's name , For example (**Sample**).
4. Create a folder called **src** and add the **components** , **configs**, **hooks** and **pages** inside that.
5. The project structure should be as in the image below:

<div align="left"><figure><img src="../../../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1).png" alt="" width="351"><figcaption></figcaption></figure></div>

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
{% endtab %}

{% tab title="React19(Recommended)" %}
## Overview

Before you begin working on the module, ensure that your local development environment is properly set up. Refer to the [**Local Development Setup Guide**](../local-development-setup.md) provided below for detailed configuration steps.

This section specifically covers **React 19**. Make sure the branch you are working on is configured with React 19 compatible dependencies. You may refer to the [console](https://github.com/egovernments/DIGIT-Frontend/tree/console) branch, which has already been fully migrated to React 19.

## Steps

{% hint style="info" %}
Download the UI code from the link here [Digit-Frontend](https://github.com/egovernments/Digit-Frontend). if not done earlier
{% endhint %}

Follow the steps given below to create the project structure.

1. Once you have cloned the repository from Digit-Frontend, do the following.
2. Go to `micro-ui-internals → packages → modules`.
3. Create a new folder with module's name , For example (**Sample**).
4. Create a folder called **src** and add the **components** , **configs**, **hooks** and **pages** inside that.
5. The project structure should be as in the image below:\
   ![](<../../../../.gitbook/assets/image (559).png>)
6. After creating the new `Sample` module, we need to create a `package.json` file for the module, specifying the module name, version, scripts, and required dependencies.

```json
{
  "name": "@egovernments/digit-ui-module-sample",
  "version": "0.0.1",
  "description": "Sample Module UI",
  "main": "dist/index.js",
  "module": "dist/main.js",
  "source": "src/Module.js",
  "files": [
    "dist"
  ],
  "scripts": {
    "start": "microbundle-crl watch --no-compress --format modern,cjs",
    "build": "webpack --mode development --config webpack.config.js",
    "prepublish": "yarn build"
  },
  "peerDependencies": {
    "react": "^19.0.0",
    "react-dom": "^19.0.0",
    "@tanstack/react-query": "^5.62.16"
  },
  "dependencies": {
    "@egovernments/digit-ui-components": "0.0.2-webpack-23",
    "@egovernments/digit-ui-react-components": "1.8.16-upgrade.14",
    "react": "^19.0.0",
    "react-date-range": "^1.4.0",
    "react-dom": "^19.0.0",
    "react-hook-form": "^7.47.2",
    "react-i18next": "15.0.0",
    "react-router-dom": "6.25.1"
  },
  "author": "Jagankumar <jagan.kumar@egov.org.in>",
  "license": "MIT"
}
```

7.  We'd also require a webpack config file, so create a webpack.config.js file. Initial configuration should look something like this : <br>

    ```json
    const path = require("path");
    const webpack = require("webpack");
    const CompressionPlugin = require("compression-webpack-plugin");
    // const { BundleAnalyzerPlugin } = require("webpack-bundle-analyzer"); // enable when needed

    // Environment-based configuration
    const isProduction = process.env.NODE_ENV === "production";
    const isDevelopment = !isProduction;

    module.exports = {
      mode: isProduction ? "production" : "development",

      entry: "./src/Module.js",

      output: {
        filename: "[name].js", // Use [name] to support multiple entry points
        chunkFilename: "[name].[contenthash:8].chunk.js", // For lazy-loaded chunks
        path: path.resolve(__dirname, "dist"),
        library: {
          name: "@egovernments/digit-ui-module-campaign-manager",
          type: "umd",
        },
        globalObject: "this",
        clean: true,
        publicPath: "auto", // Auto-detect public path for lazy loading
      },

      resolve: {
        extensions: [".js", ".jsx"],
      },

      optimization: {
        usedExports: true,
        sideEffects: false, // Enable tree-shaking
        concatenateModules: isProduction,
        minimize: isProduction,
        runtimeChunk: false, // Keep runtime in main bundle for library compatibility
        splitChunks: {
          chunks: "async", // Only split async chunks (for lazy loading)
          cacheGroups: {
            default: false,
            vendors: false,
            // Only create chunks for lazy-loaded modules
            async: {
              chunks: "async",
              minSize: 20000,
              minChunks: 1,
              priority: 10,
            },
          },
        },
        moduleIds: isProduction ? 'deterministic' : 'named',
      },

      performance: {
        maxAssetSize: 100000, // raise a bit since React 19 is heavier
        maxEntrypointSize: 100000,
        hints: isProduction ? "warning" : false,
      },

      externals: {
        // Core React ecosystem
        react: "React",
        "react-dom": "ReactDOM",
        "react-router-dom": "react-router-dom",
        "react-i18next": "react-i18next",
        "@tanstack/react-query": "@tanstack/react-query",
        // Redux ecosystem
        "react-redux": "react-redux",
        redux: "redux",
        "redux-thunk": "redux-thunk",
        // DIGIT UI cross-dependencies
        "@egovernments/digit-ui-components": "@egovernments/digit-ui-components",
        "@egovernments/digit-ui-react-components": "@egovernments/digit-ui-react-components",
        "@egovernments/digit-ui-libraries": "@egovernments/digit-ui-libraries",
        "@egovernments/digit-ui-svg-components": "@egovernments/digit-ui-svg-components",
      },

      module: {
        rules: [
          {
            test: /\.(js|jsx)$/,
            exclude: /node_modules/,
            use: {
              loader: "babel-loader",
              options: {
                cacheDirectory: true,
                cacheCompression: false,
                presets: [
                  [
                    "@babel/preset-env",
                    {
                      // Modern browser targets (React 19 requires modern browsers)
                      targets: { esmodules: true },
                      modules: false,
                    },
                  ],
                  [
                    "@babel/preset-react",
                    {
                      runtime: "automatic", // React 17+ JSX transform
                    },
                  ],
                ],
                plugins: [...(isProduction ? [["transform-remove-console", { exclude: ["error", "warn"] }]] : [])],
              },
            },
          },
          {
            test: /\.(png|jpe?g|gif|svg)$/,
            type: "asset",
            parser: {
              dataUrlCondition: {
                maxSize: 10 * 1024, // inline small images
              },
            },
            generator: {
              filename: "images/[name].[hash][ext]",
            },
          },
          {
            test: /\.(woff|woff2|eot|ttf|otf)$/,
            type: "asset/resource",
            generator: {
              filename: "fonts/[name].[hash][ext]",
            },
          },
        ],
      },

      devtool: isProduction ? "hidden-source-map" : "cheap-module-source-map", // faster rebuilds in dev

      devServer: isDevelopment
        ? {
            static: {
              directory: path.join(__dirname, "dist"),
            },
            hot: true,
            historyApiFallback: true,
            watchFiles: {
              paths: ["src/**/*"], // watch your source files
              options: {
                ignored: [path.resolve(__dirname, "node_modules"), path.resolve(__dirname, "dist")],
                poll: 1000,
                aggregateTimeout: 300,
              },
            },
          }
        : undefined,

      plugins: [
        new webpack.DefinePlugin({
          "process.env.NODE_ENV": JSON.stringify(process.env.NODE_ENV || "development"),
        }),
        ...(isDevelopment ? [new webpack.HotModuleReplacementPlugin()] : []),
        ...(isProduction
          ? [
              new CompressionPlugin({
                algorithm: "brotliCompress", // or gzip
                test: /\.(js|css|html|svg)$/,
              }),
              // new BundleAnalyzerPlugin(), // enable when debugging bundle size
            ]
          : []),
      ],

      stats: {
        errorDetails: true,
        children: false,
        modules: false,
        entrypoints: false,
      },
    };
    ```
8. We need to add a .babelrc file\
   `{`   \
   `"presets": ["@babel/preset-env", "@babel/preset-react"]`   \
   `}`

The next step is to initialise the Dependency, refer [here](install-dependency.md) to learn more about the setup
{% endtab %}
{% endtabs %}
