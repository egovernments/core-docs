---
description: >-
  We followed a structured testing process by first validating each upgraded
  package in a simple React app, then integrating them into the DIGIT core
  module to ensure compatibility and stability.
---

# Testing the Upgraded Packages

### 1. Testing Upgraded Packages in a Simple React Application

Before integrating the upgraded packages into the DIGIT application, we created a minimal React application to test their functionality. The following steps were performed:

1. Creating a simple React app
2. A lightweight React application was set up to import and test components from each upgraded package.
3. The goal was to ensure that basic component rendering and interactions worked without errors.
4. Observations and Results
5. All packages performed as expected in the standalone React environment.
6. No major issues were encountered at this stage, indicating that the package upgrades were stable in an isolated setup.

***

### 2. Integration Testing: Running Upgraded Packages in the DIGIT Core Module

After verifying individual package functionality, the next step was to test their integration within the DIGIT application. This involved modifying configurations and dependencies in the core DIGIT module.\
\
2.1 Updating package.json in the DIGIT Frontend

The package.json file in DIGIT-Frontend/micro-ui/web/micro-ui-internals was updated to include:

* The latest dependencies from the upgraded packages.
* Additional dependencies for compatibility with React 19.
* Ensuring alignment with the existing DIGIT application setup.

Below is the updated package.json file:

```
{
  "name": "egovernments",
  "version": "1.0.0",
  "main": "index.js",
  "workspaces": [
    "packages/libraries",
    "packages/react-components",
    "packages/ui-components",
    "example",
    "packages/modules/*"
  ],
  "author": "JaganKumar <jagan.kumar@egov.org.in>",
  "license": "MIT",
  "private": true,
  "engines": {
    "node": ">=14"
  },
  "scripts": {
    "start": "cross-env SKIP_PREFLIGHT_CHECK=true run-s build start:dev",
    "sprint": "SKIP_PREFLIGHT_CHECK=true run-s start:script",
    "start:dev": "run-p dev:**",
    "start:script": "./scripts/create.sh",
    "build": "run-S build:**",
    "buildD:svg-components": "cd packages/svg-components && yarn build",
    "build:ui-components": "cd packages/ui-components && yarn build",
    "build:react-components": "cd packages/react-components && yarn build",
    "build:libraries": "cd packages/libraries && yarn build",
    "build:core": "cd packages/modules/core && yarn build",
    "build:assignment": "cd packages/modules/assignment && yarn build",
    "build:workbench": "cd packages/modules/workbench && yarn build",
    "dev:example": "cd example && yarn start",
    "clean": "rm -rf node_modules && yarn clean:ui-components && yarn clean:react-components && yarn clean:libraries && yarn clean:core && yarn clean:workbench && yarn clean:assignment && yarn clean:example && yarn clean:ui-components-dist && yarn clean:react-components-dist && yarn clean:libraries-dist && yarn clean:core-dist && yarn clean:workbench-dist && yarn clean:assignment-dist && yarn clean:yarnLock",
    "clean-nm": "rm -rf node_modules && yarn clean:ui-components && yarn clean:react-components && yarn clean:libraries && yarn clean:core && yarn clean:assignment && yarn clean:example",
    "clean-dist": "yarn clean:ui-components-dist && yarn clean:react-components-dist && yarn clean:libraries-dist && yarn clean:core-dist && yarn clean:assignment-dist && yarn clean:workbench-dist",
    "clean:ui-components": "cd packages/ui-components && rm -rf node_modules",
    "clean:react-components": "cd packages/react-components && rm -rf node_modules",
    "clean:libraries": "cd packages/libraries && rm -rf node_modules",
    "clean:core": "cd packages/modules/core && rm -rf node_modules",
    "clean:workbench": "cd packages/modules/workbench && rm -rf node_modules",
    "clean:assignment": "cd packages/modules/assignment && rm -rf node_modules",
    "clean:example": "cd example && rm -rf node_modules",
    "clean:ui-components-dist": "cd packages/ui-components && rm -rf dist",
    "clean:react-components-dist": "cd packages/react-components && rm -rf dist",
    "clean:libraries-dist": "cd packages/libraries && rm -rf dist",
    "clean:core-dist": "cd packages/modules/core && rm -rf dist",
    "clean:workbench-dist": "cd packages/modules/workbench && rm -rf dist",
    "clean:assignment-dist": "cd packages/modules/assignment && rm -rf dist",
    "clean:yarnLock": "rm -rf yarn.lock"
  },
  "resolutions": {
    "**/@babel/runtime": "7.20.1",
    "**/babel-preset-react-app": "10.0.0",
    "**/styled-components": "5.0.0",
    "fast-uri": "2.1.0"
  },
  "devDependencies": {
    "clean-webpack-plugin": "^4.0.0",
    "eslint-config-react-app": "^7.0.1",
    "html-webpack-plugin": "^5.6.3",
    "husky": "7.0.4",
    "lint-staged": "12.3.7",
    "npm-run-all": "4.1.5",
    "prettier": "2.1.2",
    "vite": "^6.1.0",
    "webpack": "^5.97.1",
    "webpack-cli": "^6.0.1",
    "webpack-dev-server": "^5.2.0",
    "dotenv-webpack": "^8.0.0"
  },
  "husky": {},
  "lint-staged": {
    "*.{js,css,md}": "prettier --write"
  },
  "eslintConfig": {
    "extends": [
      "react-app"
    ]
  },
  "dependencies": {
    "@egovernments/digit-ui-components": "0.0.2-beta.4-webpack.2",
    "@egovernments/digit-ui-react-components": "1.8.16-upgrade.2",
    "@tanstack/react-query": "^5.62.16",
    "lodash": "4.17.21",
    "microbundle-crl": "0.13.11",
    "process": "^0.11.10",
    "react": "^19.0.0",
    "react-dom": "^19.0.0",
    "react-hook-form": "7.52.2",
    "react-i18next": "15.0.0",
    "react-redux": "^9.2.0",
    "react-router-dom": "6.25.1"
  }
}
```

#### 2.2 Updating package.json in DIGIT-Frontend/micro-ui/web/micro-ui-internals/examples

Since the examples directory serves as the entry point for our application, it was crucial to update its dependencies to align with the latest package upgrades and ensure compatibility with React 19.

Below is the updated package.json file:

```
{
  "name": "@egovernments/digit-ui-example",
  "version": "1.0.0",
  "license": "MIT",
  "private": true,
  "homepage": "digit-ui",
  "scripts": {
    "start": "webpack serve --config webpack.config.js --mode development",
    "start:old": "react-scripts start"
  },
  "devDependencies": {
    "@egovernments/digit-ui-libraries": "1.8.1-upgrade.6",
    "@egovernments/digit-ui-module-core": "1.9.1-test.100",
    "@egovernments/digit-ui-components": "0.0.2-beta.4-webpack.2",
    "@egovernments/digit-ui-react-components": "1.8.16-upgrade.2",
    "@egovernments/digit-ui-module-assignment": "0.0.1",
    "@egovernments/digit-ui-module-workbench": "1.0.19-test.1",
    "http-proxy-middleware": "^1.0.5",
    "react": "19.0.0",
    "react-dom": "19.0.0",
    "react-i18next": "15.0.0",
    "react-router-dom": "6.25.1",
    "react-scripts": "4.0.1",
    "webpack": "^5.97.1",
    "webpack-cli": "^6.0.1",
    "webpack-dev-server": "^5.2.0",
    "dotenv-webpack": "^8.0.0"
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  }
}
```

#### Key Changes and Updates

1. Latest Dependencies
2. All upgraded dependencies have been incorporated to ensure stability and feature compatibility.
3. Updated critical libraries like React, React Router, and other essential dependencies.
4. Migration from react-scripts to Webpack
5. One of the most significant changes in this update is the removal of react-scripts.
6. We have transitioned to Webpack for build and compilation, providing greater flexibility and control over the bundling process.
7. A new build script using Webpack has been added to the scripts section.
8. Webpack Integration
9. To support this transition, Webpack and its necessary dependencies have been added under devDependencies.
10. This shift improves build performance, allows better optimizations, and reduces unnecessary dependencies.

In the next section, we will discuss the specific changes made for Webpack integration and the new configuration files added.

#### 2.3 Webpack Configuration for the Example App

Previously, the example application was built on top of Create React App (CRA), which relied on react-scripts for compilation and bundling. However, since we have migrated to Webpack, we now require a dedicated Webpack configuration file (webpack.config.js) and a Babel configuration file (.babelrc) to handle the build process.

Below is the Webpack configuration file:

```
const path = require("path");
const webpack = require("webpack");
const HtmlWebpackPlugin = require("html-webpack-plugin");
const { CleanWebpackPlugin } = require("clean-webpack-plugin");


module.exports = {
  mode: "development", // Set mode to development
  entry: path.resolve(__dirname, 'src/index.js'),
  devtool: "source-map", // Enable source maps for easier debugging in development
  module: {
    rules: [
      {
        test: /\.(js)$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader",
          options: {
            presets: ["@babel/preset-env", "@babel/preset-react"],
            plugins: ["@babel/plugin-proposal-optional-chaining"]
          }
        },
      },
      {
        test: /\.css$/i,
        use: ["style-loader", "css-loader"],
      }
    ],
  },
  output: {
    filename: "[name].bundle.js",
    path: path.resolve(__dirname, "build"),
    publicPath: "/",
  },
  optimization: {
    splitChunks: {
      chunks: 'all',
      minSize: 20000,
      maxSize: 50000,
      enforceSizeThreshold: 50000,
      minChunks: 1,
      maxAsyncRequests: 30,
      maxInitialRequests: 30
    },
  },
  plugins: [
    new webpack.ProvidePlugin({
      process: "process/browser",
    }),
    new CleanWebpackPlugin(),
    new HtmlWebpackPlugin({ inject: true, template: "public/index.html" }),
  ],
  resolve: {
    modules: [path.resolve(__dirname, 'src'), 'node_modules'],
    extensions: ['.js', '.jsx', '.ts', '.tsx'],
    preferRelative: true, // Try resolving relatively if needed
    fallback: {
      process: require.resolve("process/browser"),
    },
  },
  devServer: {
    static: path.join(__dirname, "dist"), // Change this to "dist"
    compress: true,
    port: 3000,
    hot: true,
    historyApiFallback: true,
    proxy: [
      {
        context: ["/egov-mdms-service",
          "/access/v1/actions/mdms",
          "/tenant-management",
          "/user-otp",
          "/egov-mdms-service",
          "/mdms-v2",
          "/egov-idgen",
          "/egov-location",
          "/localization",
          "/egov-workflow-v2",
          "/pgr-services",
          "/filestore",
          "/egov-hrms",
          "/user-otp",
          "/user",
          "/fsm",
          "/billing-service",
          "/collection-services",
          "/pdf-service",
          "/pg-service",
          "/vehicle",
          "/vendor",
          "/property-services",
          "/fsm-calculator/v1/billingSlab/_search",
          "/pt-calculator-v2",
          "/dashboard-analytics",
          "/echallan-services",
          "/egov-searcher/bill-genie/mcollectbills/_get",
          "/egov-searcher/bill-genie/billswithaddranduser/_get",
          "/egov-searcher/bill-genie/waterbills/_get",
          "/egov-searcher/bill-genie/seweragebills/_get",
          "/egov-pdf/download/UC/mcollect-challan",
          "/egov-hrms/employees/_count",
          "/tl-services/v1/_create",
          "/tl-services/v1/_search",
          "/egov-url-shortening/shortener",
          "/inbox/v1/_search",
          "/inbox/v2/_search",
          "/tl-services",
          "/tl-calculator",
          "/org-services",
          "/edcr",
          "/hcm-moz-impl",
          "/bpa-services",
          "/noc-services",
          "/egov-user-event",
          "/egov-document-uploader",
          "/egov-pdf",
          "/egov-survey-services",
          "/ws-services",
          "/sw-services",
          "/ws-calculator",
          "/sw-calculator/",
          "/audit-service/",
          "/egov-searcher",
          "/report",
          "/inbox/v1/dss/_search",
          "/loi-service",
          "/project/v1/",
          "/estimate-service",
          "/loi-service",
          "/works-inbox-service/v2/_search",
          "/egov-pdf/download/WORKSESTIMATE/estimatepdf",
          "/muster-roll",
          "/individual",
          "/mdms-v2",
          "/facility/v1/_search",
          "/project/staff/v1/_create",
          "/product/v1/_create",
          "/boundary-service",
          "/project-factory",
          "/project-factory/v1/data/_autoGenerateBoundaryCode",
          "/billing-service/bill/v2/_fetchbill",
          "/tenant-management",
          "/default-data-handler",
          "/facility/v1/_create"
        ], // Add all endpoints that need to be proxied
        target: "https://unified-qa.digit.org",
        changeOrigin: true,
        secure: false,
      },
    ],
}
};
```

#### Key Changes and Considerations

1. Replacing react-scripts with Webpack
2. CRA previously handled bundling and compilation internally via react-scripts.
3. Now, Webpack explicitly manages the entire build process, allowing greater customization and optimizations.
4. Handling Proxy Configuration Inside Webpack
5. One critical change is the migration of proxy settings from the separate setupProxy.js file to inside the Webpack config itself.
6. This change was necessary because Webpack does not recognize setupProxy.js, which was previously utilized by react-scripts.
7. Integrating proxies directly within webpack.config.js ensures smooth API request handling and local development without additional configurations.

#### 2.4 Adding the Core Module Locally for Testing

Since the Core Module was not upgraded along with the other packages, we added it locally inside:

📂 DIGIT-Frontend/micro-ui/web/micro-ui-internals/packages/modules

#### Key Updates & Changes

**(a) Migration to Webpack**

Similar to other packages, we migrated the Core Module from Microbundle to Webpack for better compatibility and optimization. Below is the updated Webpack configuration file:

```
const path = require("path");


module.exports = {
  mode: "development",
  entry: "./src/Module.js",
  output: {
    filename: "main.js",
    path: path.resolve(__dirname, "dist"),
    library: {
      name: "@egovernments/digit-ui-module-core",
      type: "umd",
    },
    globalObject: 'this', // Add this line to ensure compatibility in different environments
  },
  resolve: {
    extensions: [".js"],
  },
  externals: {
    react: {
      commonjs: 'react',
      commonjs2: 'react',
      amd: 'react',
      root: 'React',
    },
    'react-dom': {
      commonjs: 'react-dom',
      commonjs2: 'react-dom',
      amd: 'react-dom',
      root: 'ReactDOM',
    },
    'react-i18next': 'react-i18next',
    'react-router-dom': 'react-router-dom'
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader",
          options: {
            presets: ["@babel/preset-env", "@babel/preset-react"],
          },
        },
      },
    ],
  },
};
```

**(b) Upgrading package.json**

The Core Module’s package.json was also updated to align with:

* The latest package upgrades
* React 19 compatibility

```
{
  "name": "@egovernments/digit-ui-module-core",
  "version": "1.9.1-test.100",
  "license": "MIT",
  "main": "dist/main.js",
  "module": "dist/main.js",
  "source": "src/Module.js",
  "files": [
    "dist"
  ],
  "scripts": {
    "example": "cd example && npm run start",
    "start": "react-scripts start",
    "build": "webpack  --mode=development --node-env=production --config webpack.config.js",
    "prepare": "yarn build",
    "publish:components": "npm publish --tag core-webpack-v0.1",
    "predeploy": "cd example && yarn install && yarn run build",
    "deploy": "gh-pages -d example/build"
  },
  "dependencies": {
    "@egovernments/digit-ui-components": "0.0.2-beta.4-webpack.2",
    "@egovernments/digit-ui-react-components": "1.8.16-upgrade.2",
    "@egovernments/digit-ui-module-workbench": "1.0.19-test.1",
    "@tanstack/react-query": "^5.62.16",
    "react": "19.0.0",
    "react-dom": "19.0.0",
    "react-i18next": "11.16.2",
    "react-redux": "7.2.8",
    "react-router-dom": "5.3.0",
    "react-tooltip": "4.1.2",
    "redux": "5.0.0",
    "redux-thunk": "2.4.1"
  },
  "author": "JaganKumar <jagan.kumar@egov.org.in>",
  "keywords": [
    "digit",
    "egov",
    "dpg",
    "digit-ui",
    "core"
  ],
  "devDependencies": {
    "sass": "^1.83.4",
    "sass-loader": "^16.0.4",
    "@babel/core": "^7.23.3",
    "@babel/preset-env": "^7.23.3",
    "@babel/preset-react": "^7.23.3",
    "babel-loader": "8.0.0",
    "cross-env": "7.0.3",
    "lint-staged": "12.3.7",
    "react": "19.0.0",
    "react-dom": "19.0.0",
    "webpack": "^5.97.1",
    "webpack-cli": "^4.10.0"
  }
}
```
