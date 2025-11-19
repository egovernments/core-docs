# DIGIT-UI-LIBRARIES Changes Overview

The **DIGIT-UI-LIBRARIES** **repository** and its **develop-webpack** branch contain all the upgraded packages. This section provides a detailed breakdown of each package, covering:

* The changes made
* Challenges encountered
* Solutions implemented during the upgrade process

### 1. Major Updates

This package underwent significant modifications, including:

* Upgrading dependencies to ensure compatibility with React 19
* Refactoring code to align with the latest dependency syntax changes
* Migrating the build system from Microbundle to Webpack

#### Changes in package.json

The package.json file was updated to support the latest dependencies required for React 19 compatibility. Key updates include:

* Upgrading react-router-dom from version 5 to version 6
* Updating other dependencies to match the latest React ecosystem requirements

Since we migrated from Microbundle to Webpack, the build script was also updated accordingly. More details on Webpack configurations will be discussed later in this document. Additionally, Webpack-specific devDependencies have been added to support this transition.

Below is the latest package.json file for this package:

(Insert package.json content here)

***

### 2. Code & Syntax Changes for Latest Dependencies

Several major dependency updates required code modifications, particularly in the following libraries:

* react-router-dom
* react-i18next
* @tanstack/react-query

Here're few examples of syntax changes

react-router-dom@5 to react-router-dom@6

#### React Router v5 → v6

| Concept                     | React Router v5                                                                                               | React Router v6                                                                                            |
| --------------------------- | ------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| **Import**                  | `import { BrowserRouter, Switch, Route, Redirect } from "react-router-dom";`                                  | `import { BrowserRouter, Routes, Route, Navigate } from "react-router-dom";`                               |
| **Route Definition**        | `<Switch> <Route path="/home" component={Home} /> <Route path="/about" render={() => <About />} /> </Switch>` | `<Routes> <Route path="/home" element={<Home />} /> <Route path="/about" element={<About />} /> </Routes>` |
| **Redirect → Navigate**     | `<Redirect to="/login" />`                                                                                    | `<Navigate to="/login" replace />`                                                                         |
| **Access route params**     | `const { id } = props.match.params;`                                                                          | `const { id } = useParams();`                                                                              |
| **Programmatic navigation** | `props.history.push("/dashboard");`                                                                           | `const navigate = useNavigate(); navigate("/dashboard");`                                                  |
| **Nested Routes**           | `<Route path="/users" component={Users} />`                                                                   | `<Route path="/users" element={<Users />}> <Route path=":id" element={<UserDetail />} /> </Route>`         |
| **404 Fallback**            | `<Route component={NotFound} />`                                                                              | `<Route path="*" element={<NotFound />} />`                                                                |

#### React Query → TanStack Query (v5+)

| Concept                        | React Query (v3/v4)                                                         | TanStack Query (v5)                                                                   |
| ------------------------------ | --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| **Import**                     | `import { useQuery, QueryClient, QueryClientProvider } from "react-query";` | `import { useQuery, QueryClient, QueryClientProvider } from "@tanstack/react-query";` |
| **QueryClient Initialization** | `const queryClient = new QueryClient();`                                    | `const queryClient = new QueryClient();`                                              |
| **Provider Setup**             | `<QueryClientProvider client={queryClient}><App /></QueryClientProvider>`   | `<QueryClientProvider client={queryClient}><App /></QueryClientProvider>`             |
| **useQuery**                   | `useQuery("employeeData", Digit.Hooks.useEmployeeSearch);`                  | `useQuery({ queryKey: ["employeeData"], queryFn: Digit.Hooks.useEmployeeSearch });`   |
| **useMutation**                | `useMutation(Digit.Hooks.useCreateApplication);`                            | `useMutation({ mutationFn: Digit.Hooks.useCreateApplication });`                      |
| **Invalidate Queries**         | `queryClient.invalidateQueries("applicationSearch");`                       | `queryClient.invalidateQueries({ queryKey: ["applicationSearch"] });`                 |
| **setQueryData**               | `queryClient.setQueryData("employeeData", data);`                           | `queryClient.setQueryData(["employeeData"], data);`                                   |
| **Devtools Import**            | `import { ReactQueryDevtools } from "react-query/devtools";`                | `import { ReactQueryDevtools } from "@tanstack/react-query-devtools";`                |

These changes ensure smooth integration with React 19 while leveraging the latest features and best practices.

***

### 3. Migration to Webpack from Microbundle

Previously, the Microbundle tool was used for building packages. As part of this upgrade, we have migrated to Webpack, which offers:

* Better build performance
* Improved modular bundling
* Greater flexibility in configuration

This migration required the addition of:

* A dedicated Webpack configuration file (webpack.config.js)
* A Babel configuration file (.babelrc)

#### Key Webpack Configuration Details

The most critical elements in the Webpack configuration are:

* Entry file: index.js
* Output file: main.js (generated under dist/ after compilation)

Below is the webpack.config.js and .babelrc configuration:

webpack.config.js

```
const path = require("path");

module.exports = {
  mode: "production",
  entry: "./src/index.js",
  output: {
    filename: "main.js",
    path: path.resolve(__dirname, "dist"),
    library: {
      name: "@egovernments/digit-ui-components",
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

.babelrc

```
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```
