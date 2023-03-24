# Creating a React-MUI-TypeScript Template
The purpose of this tutorial is to document the step by step on how to create a [React-MUI-TypeScript Template](https://github.com/equisoide/react-mui-ts-template) from scratch, so that it will serve as a reference guide for myself and for others.

## 1. Install required libraries
- [React App with TypeScript template](https://github.com/facebook/create-react-app/tree/main/packages/cra-template-typescript):
  - `npx create-react-app react-mui-ts-template --template typescript`
  - `cd react-mui-ts-template`
  - Go to **package.json** file and rearrange **dependencies** as follow (keep your current versions):
    ```json
    "dependencies": {
      "react": "^18.2.0",
      "react-dom": "^18.2.0",
      "react-scripts": "5.0.1",
      "web-vitals": "^2.1.4"
    },
    "devDependencies": {
      "@testing-library/jest-dom": "^5.16.4",
      "@testing-library/react": "^13.3.0",
      "@testing-library/user-event": "^13.5.0",
      "@types/jest": "^27.5.2",
      "@types/node": "^16.11.42",
      "@types/react": "^18.0.14",
      "@types/react-dom": "^18.0.5",
      "typescript": "^4.7.4"
    },
    ```
  - Save
  - Delete **node_modules** and **package-lock.json** file
  - `npm install`
- [SASS](https://sass-lang.com/install):
  - `npm i sass --save-dev`
- [MUI (Material UI)](https://mui.com/material-ui/getting-started/installation):
  - `npm i @mui/material @emotion/react @emotion/styled`
  - `npm i @fontsource/roboto`
  - `npm i @mui/icons-material`
  -  `npm i @mui/x-date-pickers`
- [react-i18next](https://react.i18next.com/guides/quick-start):
  - `npm i i18next react-i18next`
  - `npm i i18next-browser-languagedetector`
- [env-cmd](https://github.com/toddbluhm/env-cmd):
  - `npm i env-cmd --save-dev`
- [Stylelint](https://stylelint.io/user-guide/get-started):
  - `npm i stylelint stylelint-config-standard-scss --save-dev`
- [ESLint](https://eslint.org/docs/user-guide/getting-started):
  - `npm i eslint --save-dev`
  - `npm init @eslint/config`
    - To check syntax, find problems, and enforce code style
    - JavaScript modules (import/export)
    - React
    - Does your project use TypeScript? › **Yes**
    - Where does your code run? › **Browser**
    - Use a popular style guide › **Standard: https://github.com/standard/eslint-config-standard-with-typescript**
    - What format do you want your config file to be in? › **JavaScript**
    - Would you like to install them now? › **Yes**
    - Which package manager do you want to use? › **npm**
- [Storybook](https://storybook.js.org/docs/react/get-started/install):
  - `npx storybook init`
    - Do you want to run the 'eslintPlugin' migration on your project? › **y**
    - Do you want to run the 'npm7' migration on your project? » (Y/n) › **y**
  - `npm i --save-dev react-docgen-typescript-plugin`
- [React Router](https://reactrouter.com/docs/en/v6/getting-started/installation)
  - `npm i react-router-dom@6`

## 2. Install VS Code recomented extensions
- [DotENV](https://marketplace.visualstudio.com/items?itemName=mikestead.dotenv)
- [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
- [EditorConfig](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig)
- [Icons](https://marketplace.visualstudio.com/items?itemName=robertohuertasm.vscode-icons)
- [MDX](https://marketplace.visualstudio.com/items?itemName=silvenon.mdx)
- [NpmIntellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.npm-intellisense)
- [SCSS Formatter](https://marketplace.visualstudio.com/items?itemName=sibiraj-s.vscode-scss-formatter)
- [SortLines](https://marketplace.visualstudio.com/items?itemName=Tyriar.sort-lines)
- [Stylelint](https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint)

## 3. Add [.editorconfig](https://editorconfig.org)
- Create **.editorconfig** file at the app's root level
- Add the following configuration:
  ```env
  # EditorConfig helps maintain consistent coding styles
  # for multiple developers working on the same project.
  # Learn more: https://editorconfig.org
  root = true

  [*]
  charset = utf-8
  end_of_line = lf
  indent_size = 2
  indent_style = space
  insert_final_newline = true
  trim_trailing_whitespace = true
  ```
- Save twice (the 2nd save is to apply coding style to the **.editorconfig** file)

## 4. Update [package.json](https://docs.npmjs.com/cli/v7/configuring-npm/package-json)
- Add **description** after **version**:
  - `"description": "React, MUI and TypeScript template",`
- Set the package as [public](https://docs.npmjs.com/cli/v7/configuring-npm/package-json#private):
  - `"private": false,`
- Add the [homepage](https://stackoverflow.com/questions/43011207/using-homepage-in-package-json-without-messing-up-paths-for-localhost) URL after **private**:
  - `"homepage": "./",`
- Add **keywords** after **homepage**:
  ```json
  "keywords": [
    "emotion",
    "es6",
    "eslint",
    "hooks",
    "i18next",
    "jest",
    "mui",
    "react",
    "roboto",
    "router",
    "sass",
    "spa",
    "storybook",
    "stylelint",
    "typescript",
    "vscode"
  ],
  ```
- Replace **scripts** object with the following:
  ```json
  "scripts": {
    "build": "env-cmd --no-override -f ./.env-override/.env.production react-scripts build",
    "build:d": "env-cmd --no-override -f ./.env-override/.env.development react-scripts build",
    "build:l": "env-cmd --no-override -f ./.env-override/.env.local react-scripts build",
    "build:q": "env-cmd --no-override -f ./.env-override/.env.qa react-scripts build",
    "build:s": "env-cmd --no-override -f ./.env-override/.env.staging react-scripts build",
    "eject": "react-scripts eject",
    "init": "npm ci --loglevel=error --no-audit --no-fund",
    "lint": "eslint --ext .js,.jsx,.ts,.tsx src/",
    "lint:f": "eslint --fix --ext .js,.jsx,.ts,.tsx src/",
    "sb-build": "env-cmd --no-override -f ./.env-override/.env.production build-storybook -s public -o ./out/storybook/production",
    "sb-build:d": "env-cmd --no-override -f ./.env-override/.env.development build-storybook -s public -o ./out/storybook/development",
    "sb-build:l": "env-cmd --no-override -f ./.env-override/.env.local build-storybook -s public -o ./out/storybook/local",
    "sb-build:q": "env-cmd --no-override -f ./.env-override/.env.qa build-storybook -s public -o ./out/storybook/qa",
    "sb-build:s": "env-cmd --no-override -f ./.env-override/.env.staging build-storybook -s public -o ./out/storybook/staging",
    "sbook": "env-cmd --no-override -f ./.env-override/.env.local start-storybook -p 4002 -s public",
    "sbook-https": "env-cmd --no-override -f ./.env-override/.env.https.local start-storybook -p 4003 -s public --https --ssl-cert localhost.pem --ssl-key localhost-key.pem",
    "slint": "stylelint \"src/**/*.{css,scss}\"",
    "slint:f": "stylelint --fix \"src/**/*.{css,scss}\"",
    "start": "env-cmd --no-override -f ./.env-override/.env.local react-scripts start",
    "start-https": "env-cmd --no-override -f ./.env-override/.env.https.local react-scripts start",
    "test": "env-cmd --no-override -f ./.env-override/.env.test react-scripts test --env=jsdom --coverage --coverageDirectory='./out/coverage' --watchAll=false"
  },
  ```
- Remove **eslintConfig** object
- Add [jest](https://jestjs.io/docs/configuration) object after **scripts**:
  ```json
  "jest": {
    "collectCoverageFrom": [
      "src/**/*.ts",
      "src/**/*.tsx",
      "!src/**/*.stories.tsx",
      "!src/index.tsx",
      "!src/react-app-env.d.ts",
      "!src/util/web-vitals.ts",
      "!src/app/index.tsx"
    ]
  },
  ```
- Save

## 5. Update [tsconfig.json](https://www.typescriptlang.org/tsconfig)
- Add the following comments before **compilerOptions**:
  ```js
    // Specifies the root files and the compiler options required
    // to compile the TypeScript project.
    // Learn more: https://www.typescriptlang.org/tsconfig
  ```
- Enable [ES6](http://es6-features.org) features:
  - `"target": "es6",`
- Disable **TypeScript** [incremental](https://www.typescriptlang.org/tsconfig#incremental) compilation (I had experienced cache issues with it):
  - `"incremental": false,`
- Put **lib** on a single line:
  - `"lib": ["dom", "dom.iterable", "esnext"],`
- Sort **compilerOptions** items by selecting all of them and pressing `F9` (SortLines Plugin)
- Remove trailing comma from the last item of **compilerOptions**
- Replace **include** array with the following:
  - `"include": ["src/**/*"]`
- Save

## 6. Update [.eslintrc](https://eslint.org/docs/user-guide/configuring)
- Rename **.eslintrc.js** to **.eslintrc**
- Remove `module.exports = ` (the file is now a JSON document)
- Remove semicolon at the end of the file
- Replace all **single quotes** by **double quotes**
- Enclose all property names in **double quotes**
- Add the following comments before **env**:
  ```js
    // EsLint helps to check syntax, find problems, and enforce a code style.
    // Learn more: https://stylelint.io/user-guide/configure
  ```
- Add `"jest": true` to the `"env"` object
- Replace **extends** array with the following:
  ```json
  "extends": [
    "eslint:recommended",
    "plugin:react/recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:jest/recommended",
    "plugin:storybook/recommended"
  ],
  ```
- Replace **plugins** array with the following:
  ```json
  "plugins": [
    "react",
    "react-hooks",
    "@typescript-eslint"
  ],
  ```
- Replace **rules** object with the following:
  ```json
   "rules": {
    "@typescript-eslint/no-empty-function": "off",
    "comma-dangle": ["error", "always-multiline"],
    "jsx-a11y/alt-text": "off",
    "max-len": ["error", { "code": 120, "tabWidth": 2, "ignoreComments": true, "ignoreTrailingComments": true, "ignoreUrls": true, "ignoreStrings": true, "ignoreTemplateLiterals": true, "ignoreRegExpLiterals": true }],
    "no-duplicate-imports": "error",
    "no-empty": "off",
    "no-plusplus": "off",
    "no-shadow": "off",
    "quotes": ["error", "single"],
    "react-hooks/exhaustive-deps": "warn",
    "react-hooks/rules-of-hooks": "error",
    "react/function-component-definition": "off",
    "react/jsx-filename-extension": ["error", { "extensions": [".tsx"] }],
    "react/jsx-indent-props": ["error", 2],
    "react/jsx-props-no-spreading": "off",
    "react/react-in-jsx-scope": "off"
  },
  ```
- Add **settings** object after **rules**:
  ```json
  "settings": {
    "import/resolver": {
      "node": {
        "extensions": [".js", ".jsx", ".ts", ".tsx"]
      }
    },
    "react": {
      "version": "detect"
    }
  }
  ```
- Add **parser** after **overrides**,
  ```json
  "parser": "@typescript-eslint/parser",
  ```
- Add **ecmaFeatures** inside **parserOptions**,
  ```json
  "parserOptions": {
    "ecmaFeatures": {
      "jsx": true
    },
  },
  ```
- Save

## 7. Add [.eslintignore](https://eslint.org/docs/user-guide/configuring/ignoring-code#the-eslintignore-file)
- Create **.eslintignore** file at the app's root level
- Add the following configuration:
  ```gitignore
  # Tells ESLint to ignore specific files and directories.
  # Learn more: https://eslint.org/docs/user-guide/configuring/ignoring-code
  node_modules/
  out/
  ```
- Save

## 8. Add [.stylelintrc](https://stylelint.io/user-guide/configure)
- Create **.stylelintrc** file at the app's root level
- Add the following configuration:
  ```json
  {
    "extends": "stylelint-config-standard-scss",
    "rules": {
      "declaration-no-important": true,
    }
  }
  ```
- Save

## 9. Add [VS Code Settings](https://code.visualstudio.com/docs/getstarted/settings)
- Create **.vscode** folder at the app's root level
- Inside **.vscode** folder, create **extensions.json** file with the following configuration:
  ```js
  {
    // Workspace recommended extensions.
    // Learn more:  http://go.microsoft.com/fwlink/?LinkId=827846
    "recommendations": [
      "christian-kohler.npm-intellisense",
      "dbaeumer.vscode-eslint",
      "editorconfig.editorconfig",
      "mikestead.dotenv",
      "sibiraj-s.vscode-scss-formatter",
      "silvenon.mdx",
      "stylelint.vscode-stylelint",
      "tyriar.sort-lines",
      "vscode-icons-team.vscode-icons"
    ]
  }
  ```
- Save
- Inside **.vscode** folder, create **launch.json** file with the following configuration:
  ```js
  {
    // Launch Chrome when debugging from VS Code.
    // Learn more: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
      {
        "type": "chrome",
        "request": "launch",
        "name": "Launch Chrome against localhost",
        "url": "http://localhost:4000",
        "webRoot": "${workspaceFolder}"
      }
    ]
  }
  ```
- Save
- Inside **.vscode** folder, create **settings.json** file with the following configuration:
  ```js
  {
    // VS Code workspace settings.
    // Learn more: https://code.visualstudio.com/docs/getstarted/settings
    "editor.codeActionsOnSave": {
      "source.fixAll": true
    },
    "files.eol": "\n",
    "javascript.preferences.quoteStyle": "single",
    "typescript.preferences.quoteStyle": "single",
    "search.exclude": {
      "node_modules": true,
      "out": true,
      "package-lock.json": true
    },
    "css.validate": false,
    "scss.validate": false,
    "stylelint.validate": ["css", "scss"],
    "[scss]": {
      "editor.defaultFormatter": "sibiraj-s.vscode-scss-formatter"
    },
    "files.associations": {
      ".env.https.local": "dotenv"
    }
  }
  ```
- Save

## 10. Update [.gitignore](https://git-scm.com/docs/gitignore)
- Replace **.gitignore** with the following content:
  ```gitignore
  # See https://help.github.com/articles/ignoring-files for more about ignoring files.

  # dependencies
  /node_modules
  /.pnp
  .pnp.js

  # production
  /out

  # misc
  .DS_Store

  # certificates
  *.pem

  # log
  npm-debug.log*
  yarn-debug.log*
  yarn-error.log*
  ```
- Save

## 11. Add [Environment Files](https://create-react-app.dev/docs/adding-custom-environment-variables/#adding-development-environment-variables-in-env)
- Create **.env** file at the app's root level
- Add the following configuration:
  ```env
  # This file defines variables common to all environments.
  # Variables in this file will be overridden by each specific environment.
  # Shell variables never get overridden.
  # Name variables beginning with "REACT_APP_".
  # Access variables from the "process.env." object.
  # Restart the development server every time you change a variable.
  # Learn more: https://create-react-app.dev/docs/adding-custom-environment-variables
  # Advanced config: https://create-react-app.dev/docs/advanced-configuration

  # Path to resolve SASS imports.
  # Ref: https://create-react-app.dev/docs/adding-a-sass-stylesheet
  SASS_PATH='./src/styles'

  # Package Name and Version come from the package.json file.
  # They are used to render App Info in some places, for example
  # in the Storybook intro page, or in the App <title>.
  REACT_APP_PACKAGE_NAME=${npm_package_name}
  REACT_APP_PACKAGE_VERSION=${npm_package_version}
  
  # Lets you find common bugs in your components early during development.
  # Learn more: https://react.dev/reference/react/StrictMode
  REACT_APP_SCRICT_MODE=false
  ```
- Save
- Create **.env-override** folder at the app's root level
- Inside **.env-override** folder, create the following files:
  - **.env.development**
    ```env
    # Variables in this file are injected by the following scripts:
    # - "build:d"     Builds the App to `out/build/development`
    # - "sb-build:d"  Builds Storybook to `out/storybook/development`

    # Don't touch
    BUILD_PATH='./out/build/development'
    REACT_APP_ENV='development'

    # Add variables below, starting with REACT_APP_
    REACT_APP_API_URL='https://development.com/api/v1'
    REACT_APP_SCRICT_MODE=true
    ```
  - **.env.https.local**
    ```env
    # Variables in this file are injected by the following scripts:
    # - "start-https" Runs the App in https://localhost:4001 (HTTPS)
    # - "sbook-https" Runs Storybook in https://localhost:4003 (HTTPS)

    # Don't touch
    PORT=4001
    HTTPS=true
    SSL_CRT_FILE=localhost.pem
    SSL_KEY_FILE=localhost-key.pem
    REACT_APP_ENV='local'

    # Add variables below, starting with REACT_APP_
    REACT_APP_API_URL='https://localhost:5000/api/v1'
    REACT_APP_SCRICT_MODE=true
    ```
  - **.env.local**
    ```env
    # Variables in this file are injected by the following scripts:
    # - "start"       Runs the App in http://localhost:4000
    # - "sbook"       Runs Storybook in http://localhost:4002
    # - "build:l"     Builds the App to `out/build/local`
    # - "sb-build:l"  Builds Storybook to `out/storybook/local`

    # Don't touch
    PORT=4000
    HTTPS=false
    BUILD_PATH='./out/build/local'
    REACT_APP_ENV='local'

    # Add variables below, starting with REACT_APP_
    REACT_APP_API_URL='http://localhost:5001/api/v1'
    REACT_APP_SCRICT_MODE=true
    ```
  - **.env.production**
    ```env
    # Variables in this file are injected by the following scripts:
    # - "build"     Builds the App to `out/build/production`
    # - "sb-build"  Builds Storybook to `out/storybook/production`

    # Don't touch
    BUILD_PATH='./out/build/production'
    REACT_APP_ENV='production'

    # Add variables below, starting with REACT_APP_
    REACT_APP_API_URL='https://production.com/api/v1'
    ```
  - **.env.qa**
    ```env
    # Variables in this file are injected by the following scripts:
    # - "build:q"     Builds the App to `out/build/qa`
    # - "sb-build:q"  Builds Storybook to `out/storybook/qa`

    # Don't touch
    BUILD_PATH='./out/build/qa'
    REACT_APP_ENV='qa'

    # Add variables below, starting with REACT_APP_
    REACT_APP_API_URL='https://qa.com/api/v1'
    ```
  - **.env.staging**
    ```env
    # Variables in this file are injected by the following scripts:
    # - "build:s"     Builds the App to `out/build/staging`
    # - "sb-build:s"  Builds Storybook to `out/storybook/staging`

    # Don't touch
    BUILD_PATH='./out/build/staging'
    REACT_APP_ENV='staging'

    # Add variables below, starting with REACT_APP_
    REACT_APP_API_URL='https://staging.com/api/v1'
    ```
  - **.env.test**
    ```env
    # Variables in this file are injected by the following scripts:
    # - "test" Executes Unit Tests outputting to `out/coverage`

    # Don't touch
    REACT_APP_ENV='test'

    # Add variables below, starting with REACT_APP_
    REACT_APP_API_URL=='https://test.com/api/v1'
    ```

## 12. Add [LICENSE](https://docs.github.com/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository)
- Create **LICENSE** file at the app's root level
- Add the following terms:
  ```
  MIT License

  Copyright (c) 2022 Juan Cuartas

  Permission is hereby granted, free of charge, to any person obtaining a copy
  of this software and associated documentation files (the "Software"), to deal
  in the Software without restriction, including without limitation the rights
  to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
  copies of the Software, and to permit persons to whom the Software is
  furnished to do so, subject to the following conditions:

  The above copyright notice and this permission notice shall be included in all
  copies or substantial portions of the Software.

  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
  IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
  FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
  AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
  LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
  OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
  SOFTWARE.

  ```
- Save

## 13. Update [README.md](https://docs.github.com/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-readmes)
- Replace **README.md** with the following content:
  ````markdown
  # React, MUI and TypeScript Template
  This template is intended to help you start a new `React SPA` project from scratch with a comprehensive file structure, required dependencies, built-in configurations, example components and good practices for React Web Development.
  
  The project was bootstrapped with [Create React App](https://create-react-app.dev) following this [Tutorial](https://github.com/equisoide/react-mui-ts-steps). Below you will find some information about main features and how to perform common tasks.

  ## Supported Language Features
  This project supports a superset of the latest `JavaScript`/`TypeScript` standard. In addition to [ES6](http://es6-features.org) syntax features, it also supports:
  - [Exponentiation Operator](https://github.com/tc39/proposal-exponentiation-operator) (ES2016)
  - [Async/await](https://github.com/tc39/proposal-async-await) (ES2017)
  - [Object Rest/Spread Properties](https://github.com/tc39/proposal-object-rest-spread) (ES2018)
  - [Dynamic import()](https://github.com/tc39/proposal-dynamic-import) (stage 4 proposal)
  - [Class Fields and Static Properties](https://github.com/tc39/proposal-class-public-fields) (part of stage 3 proposal)
  - [TSX](https://www.typescriptlang.org/docs/handbook/jsx.html) and [TypeScript](https://www.typescriptlang.org)

  Constant enums and namespaces are not supported, you can learn about the constraints of using [Babel with TypeScript here](https://babeljs.io/docs/en/babel-plugin-transform-modules-amd).

  ## Core Libraries
  - [React 18.2.0](https://reactjs.org) with `React Scripts 5.0.1`
  - [SASS 1.60.0](https://sass-lang.com) with [CSS Modules](https://github.com/css-modules/css-modules)
  - [MUI 5.11.14](https://mui.com) with `Emotion` styling engine, `Roboto Fonts` and `Material Icons`
  - [TypeScript 5.0.2](https://www.typescriptlang.org) with [ES6](http://es6-features.org)
  - [I18next 22.4.13](https://react.i18next.com) for internationalization
  - [React Router 6.9.0](https://reactrouter.com/) for the routing system

  ## Documentation Tools
  - [Storybook 6.5.16](https://storybook.js.org) to document components

  ## Code Quality & Performance
  - [ESLint 8.36.0](https://eslint.org) with `TypeScript`, `React`, `React Hooks` and `Jest` configuration
  - [Stylelint 15.3.0](https://stylelint.io) to analyse `CSS`/`SCSS` files
  - [Jest 27.5.2](https://jestjs.io/docs/getting-started) to test `JavaScript`/`TypeScript` files
  - [React Testing Library 13.4.0](https://testing-library.com/docs/react-testing-library/intro) to test components
  - [Web Vitals 2.1.4](https://web.dev/vitals) to meassure performance

  ## Built-in Settings
  - [.editorconfig](https://editorconfig.org) settings to standardize charset, ending of lines and indentation
  - [.vscode](https://code.visualstudio.com/docs/getstarted/settings) settings with integrated Chrome Debugger, faster search results and auto-format on save
  - [Environment files](https://create-react-app.dev/docs/adding-custom-environment-variables) for `Local`, `Test`, `Development`, `QA`, `Staging` and `Production`

  ## Environment Quick Setup
  1. Install [NodeJs](https://nodejs.org/es/download)
  2. Install [Git](https://git-scm.com/downloads)
  3. Install [VS Code](https://code.visualstudio.com/download)
  4. Install VS Code recomented extensions:
     * [DotENV](https://marketplace.visualstudio.com/items?itemName=mikestead.dotenv)
     * [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
     * [EditorConfig](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig)
     * [Icons](https://marketplace.visualstudio.com/items?itemName=robertohuertasm.vscode-icons)
     * [MDX](https://marketplace.visualstudio.com/items?itemName=silvenon.mdx)
     * [NpmIntellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.npm-intellisense)
     * [SCSS Formatter](https://marketplace.visualstudio.com/items?itemName=sibiraj-s.vscode-scss-formatter)
     * [SortLines](https://marketplace.visualstudio.com/items?itemName=Tyriar.sort-lines)
     * [Stylelint](https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint)
  5. Install [React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi) for Google Chrome

  ## Running & Debugging the application for the first time
  1. Open a new [VS Code](https://code.visualstudio.com/download) window:
     - `File` > `New Window`
  3. Open a parent folder that will host this project (e.g. `~/Projects`):
     - `File` > `Open Folder`
  4. Open a new terminal:
     - `Terminal` > `New Terminal`
  5. Clone repo:
     - `git clone https://github.com/equisoide/react-mui-ts-template.git`
  6. Install project dependencies:
     - `cd react-mui-ts-template`
     - `npm run init` (performs a [Clean Install](https://docs.npmjs.com/cli/v8/commands/npm-ci))
  7. Restart VS Code to refresh TypeScript Intellisense, otherwise you might see errors in the editor:
     - Close VS Code
     - Open a new VS Code window
     - Open the folder where the project was cloned
  8. Start the application:
     - Open a new terminal
     - `npm start`
  9. Start debugging in VS Code:
     - Press `F5` or click on `Run and Debug` > `Green Debug Icon`
     - You can set breakpoints and inspect components in the [React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)

  ## Available Scripts
  | Command               | Description                                      | Evironment File  |
  | :---                  | :---                                             | :---             |
  | `npm run init`        | Installs project dependencies for the first time | N/A              |
  | `npm run lint`        | Analyses **JavaSript**/**TypeScript** code       | N/A              |
  | `npm run lint:f`      | Try to fix **JavaSript**/**TypeScript** errors   | N/A              |
  | `npm run slint`       | Analyses **CSS**/**SCSS** styles                 | N/A              |
  | `npm run slint:f`     | Try to fix **CSS**/**SCSS** errors               | N/A              |
  | `npm test`            | Executes Unit Tests outputting to `out/coverage` | .env.test        |
  | `npm start`           | Runs the App in http://localhost:4000            | .env.local       |
  | `npm run start-https` | Runs the App in https://localhost:4001 (HTTPS)   | .env.https.local |
  | `npm run build:l`     | Builds the App to `out/build/local`              | .env.local       |
  | `npm run build:d`     | Builds the App to `out/build/development`        | .env.development |
  | `npm run build:q`     | Builds the App to `out/build/qa`                 | .env.qa          |
  | `npm run build:s`     | Builds the App to `out/build/staging`            | .env.staging     |
  | `npm run build`       | Builds the App to `out/build/production`         | .env.production  |
  | `npm run sbook`       | Runs Storybook in http://localhost:4002          | .env.local       |
  | `npm run sbook-https` | Runs Storybook in https://localhost:4003 (HTTPS) | .env.https.local |
  | `npm run sb-build:l`  | Builds Storybook to `out/storybook/local`        | .env.local       |
  | `npm run sb-build:d`  | Builds Storybook to `out/storybook/development`  | .env.development |
  | `npm run sb-build:q`  | Builds Storybook to `out/storybook/qa`           | .env.qa          |
  | `npm run sb-build:s`  | Builds Storybook to `out/storybook/staging`      | .env.staging     |
  | `npm run sb-build`    | Builds Storybook to `out/storybook/production`   | .env.production  |
  
  ## Project Structure
  After cloning, your project should look like this:

  ```
  📦 react-mui-ts-template
  ├── 📜 .editorconfig                EditorConfig settings
  ├── 📜 .env                         Variables common to all environments
  ├── 📜 .eslintignore                Folders and files ignored by ESLint
  ├── 📜 .eslintrc                    ESLint configuration
  ├── 📜 .gitignore                   Folders and files ignored by Git
  ├── 📜 .npmrc                       Npm settings
  ├── 📜 .stylelintrc                 Stylelint configuration
  ├── 📜 LICENSE                      License information
  ├── 📜 package-lock.json            Npm dependency tree to recreate node_modules
  ├── 📜 package.json                 Project dependencies, scripts and more
  ├── 📜 README.md                    Project documentation
  ├── 📜 tsconfig.json                TypeScript configuration
  ├── 📂 .env-override
  │   ├── 📜 .env.development         Environment variables for Development
  │   ├── 📜 .env.https.local         Environment variables for Local (HTTPS)
  │   ├── 📜 .env.local               Environment variables for Local
  │   ├── 📜 .env.production          Environment variables for Production
  │   ├── 📜 .env.qa                  Environment variables for QA
  │   ├── 📜 .env.staging             Environment variables for Staging
  │   └── 📜 .env.test                Environment variables for Unit Test
  ├── 📂 .storybook
  │   ├── 📜 favicon.svg              Favicon for Storybook
  │   ├── 📜 main.js                  Storybook server behavior
  │   ├── 📜 manager.js               Customize how Storybook App renders
  │   └── 📜 preview.js               Global code that applies to all stories
  ├── 📂 .vscode
  │   ├── 📜 extensions.json          Recomended extensions to load in VS Code
  │   ├── 📜 launch.json              Launch Chrome against localhost
  │   └── 📜 settings.json            Settings for VS Code
  ├── 📂 public
  │   ├── 📜 favicon.ico              The icon found in the URL address bar
  │   ├── 📜 index.html               HTML where the React App is rendered
  │   ├── 📜 logo192.png              PWA icon (192x192)
  │   ├── 📜 logo512.png              PWA icon (512x512)
  │   ├── 📜 manifest.json            Metadata to install the App as a PWA
  │   └── 📜 robots.txt               Instructions for search crawlers
  └── 📂 src
      ├── 📜 index.tsx                The application entry point
      ├── 📜 react-app-env.d.ts       TypeScript declarations for React App
      ├── 📜 setupTests.ts            Global setup before running tests
      ├── 📂 app
      │   └── 📜 index.tsx            The main App component with routes
      ├── 📂 components/HelloWorld
      │   ├── 📜 index.module.scss    Component styles
      │   ├── 📜 index.stories.tsx    Storybook documentation
      │   ├── 📜 index.test.tsx       Jest testing file
      │   └── 📜 index.tsx            Example component definition
      ├── 📂 lang
      │   ├── 📜 index.ts             i18next configuration
      │   ├── 📜 resources.en.json    Application texts in English
      │   └── 📜 resources.es.json    Application texts in Spanish
      ├── 📂 pages
      │   └── ...                     React components for each page  
      ├── 📂 stories
      │   └── ...                     Files for the Storybook intro page
      ├── 📂 styles
      │   ├── 📜 _reset.scss          Simple CSS reset for consistent styles
      │   └── 📜 main.scss            Main SASS file
      └── 📂 util
          └── 📜 web-vitals.ts        Web Vitals reporting
  ```
  For the project to build, these files must exist with exact filenames:
  - `public/index.html` is the page template
  - `src/index.tsx` is the TypeScript entry point

  You may create subdirectories inside `src`. For faster rebuilds, only files inside `src` are processed by webpack. You need to put any TypeScript and SCSS files inside `src`, otherwise webpack won’t see them.

  Only files inside public can be used from `public/index.html`.

  ## File extensions
  Most of the files you will create in the `src` folder will be **TypeScript**, **TypeScript with React** or **SASS**:
  - `.ts`: TypeScript files (Don't use `.js`). Use it for:
    - Utilities. e.g. `arrays.ts`
    - Test of utilities. e.g. `arrays.test.ts`
  - `.tsx`: TypeScript with React (Don't use `.jsx`). Use it for:
    - Components. e.g. `HelloWorld/index.tsx`
    - Test of components. e.g. `HelloWorld/index.test.tsx`
    - Storybook stories. e.g. `HelloWorld/index.stories.tsx`
  - `.scss`: Superset of CSS (Don't use `.css`). Use it for:
    - Global styles. e.g. `main.css`
    - Component styles. e.g. `HelloWorld/index.module.scss`

  ## Adding a Stylesheet
  This project supports [Sass](https://sass-lang.com/guide) alongside [CSS Modules](https://github.com/css-modules/css-modules):
  - `Sass` is CSS with superpowers
  - `CSS Modules` scopes CSS by automatically creating a unique **className**

  `Sass` supports two syntaxes:
  - `.scss`: Is an extension of CSS where every valid CSS is a valid **.scss** as well
  - `.sass`: Is an older indented syntax not recommended for use in new **Sass** files

  In this project we use the `.scss` syntax.

  To express that a component depends on a **.scss module**, you should use the `[name].module.scss` convention:
  ```tsx
  import styles from './index.module.scss';

  function MyComponent() {
    return <div className={styles.myClass}>My Component</div>;
  }
  ```

  In development, expressing dependencies this way allows your styles to be reloaded on the fly as you edit them. In production, all `.scss` files will be concatenated into a single minified `.css` file in the build output.

  To share variables between **Sass** files, you can use Sass's [@use](https://sass-lang.com/documentation/at-rules/use) rule. There is a `SASS_PATH` variable in the `.env` file that is used to locate `.scss` files. Supposing that `SASS_PATH='./src/styles'` and that you have `_colors.scss` in that directory, then you can use it like this:
  ```scss
  @use 'colors';

  .info {
    color: colors.$primary;
  }
  ```

  For information about how to structure a SASS codebase using the **7-1 Pattern** you can read this [article](https://remote.com/blog/how-to-structure-your-sass-project) or take a look to the following [boilerplate](https://github.com/KittyGiraudel/sass-boilerplate).

  ## Adding Images and Files
  With webpack, using static assets like images and files works similarly to `SCSS`.

  To reduce the number of requests to the server, importing images that are less than 10,000 bytes returns a data URI instead of a path. This applies to the following file extensions: bmp, gif, jpg, jpeg, and png. You can control the 10,000 byte threshold by setting the `IMAGE_INLINE_SIZE_LIMIT` environment variable as documented in the [advanced configuration](https://create-react-app.dev/docs/advanced-configuration).

  ```tsx
  import logo from './logo.png';

  function Header() {
    return <img src={logo} alt="Logo" />;
  }
  ```

  ## Using HTTPS in Local Environment
  You may require the local server to run the App or Storybook over [HTTPS](https://create-react-app.dev/docs/using-https-in-development):
  - Use `npm run start-https` to run the APP over HTTPS
  - Use `npm run sbook-https` to run Storybook over HTTPS

  Note that you might get an error in the console telling that `localhost.pem` or `localhost-key.pem` files can't be found. This is because when running the App over HTTPS a valid **Certificate Authority** and an **SSL certificate** are needed.

  To generate those files use [mkcert](https://www.mariokandut.com/how-to-setup-https-ssl-in-localhost-react):
  - You need a package manager to install **mkcert**:
    - **MacOS**: Use Homebrew (`brew install mkcert`)
    - **Linux**: Use Certutil
    - **Windows**: Use Chocolatey
  - Once installed **mkcert**:
    - Open a terminal at the root of the project
    - Create a locally trusted CA with `mkcert -install`
    - Generate an SSL certificate with `mkcert localhost`
    - `localhost.pem` and `localhost-key.pem` will be generated
    - Note that these files are included in the `.gitignore`
  
  ## Working in StrictMode
  `<StrictMode>` lets you find common bugs in your components early during development. It also helps you to prepare your app for the future. You can read more about it [here](https://react.dev/reference/react/StrictMode).

  Strict Mode enables the following development-only behaviors:
  - Your components will re-render an extra time to find bugs caused by impure rendering
  - Your components will re-run Effects an extra time to find bugs caused by missing Effect cleanup
  - Your components will be checked for usage of deprecated APIs.

  To enabble/disable StrictMode you can use the `REACT_APP_STRICT_MODE` environment variable. By default it's set to `true` in the following files:
  - `.env.development`
  - `.env.https.local`
  - `.env.local`

  ## Working Guidelines
  - Never delete and re-generate the `package-lock.json` file from scratch, it will break the App and Storybook! Let `npm` update that file every time you install a new dependency
  - Create reusable components inside the `src/components` folder. Define each component in its own folder with the following structure:
    ```
    ├── 📂 src/components/MyComponent   Component name in PascalCase
        ├── 📜 index.module.cs          Component styles (optional)
        ├── 📜 index.stories.tsx        Storybook documentation
        ├── 📜 index.test.tsx           Jest testing file
        └── 📜 index.tsx                Component definition
    ```
  - Prefer [Function Components](https://www.robinwieruch.de/react-function-component) over **Class Components**, they offer almost the same: state and lifecycle methods, with the plus they are more lightway, have a sophisticated API and require less code. With the introduction of [React Hooks](https://reactjs.org/docs/hooks-intro.html) it's possible to write your entire application with just functions as React Components:
    ```tsx
    // External imports
    import Box from '@mui/material/Box';
    import { BoxProps } from '@mui/material';
    import { useTranslation } from 'react-i18next';

    // Local imports
    import styles from './index.module.scss';

    // Component props
    export interface MyComponentProps {
      /**
       * The box container styles.
       * See: https://mui.com/material-ui/api/box
       */
      box?: BoxProps
    }

    // Component definition
    function MyComponent({ box } : MyComponentProps) {
      const { t } = useTranslation();

      const defaults = MyComponent.defaultProps;
      const boxProps = { ...defaults.box, ...box } as BoxProps;

      return (
        <Box className={styles.box} {...boxProps}>
          {t('hello-world')}
        </Box>
      );
    }

    // Default props
    MyComponent.defaultProps = {
      box: {
        sx: { background: 'blue' },
      },
    };

    // Default export
    export default MyComponent;
    ```
  - Use default `imports` and `exports` when a module only exports a single thing (for example, a component). Named exports are useful for utility modules that export several functions. A module may have at most one default export and as many named exports as you like.
  - In general use [Trailing Commas](https://blog.logrocket.com/best-practices-using-trailing-commas-javascript) (except on `JSON` files), many coding styles now recommend using them all the time because they make it easier to add new parameters to your functions or copy/paste properties in arrays and objects and also helps with producing cleaner diff output
  - Add your own environment variables to the `.env-override/.env.local` file, this file should not be commited
  - Before running or building this application always run linters and unit tests
  
  ## Troubleshooting
  - **When running `npm run lint` you get this error: "Expected linebreaks to be 'LF' but found 'CRLF'"**
    - This happens because on Windows, Git converts linebreaks from `LF` to `CRLF` when you checkout the code, but esLint is configured to accept valid ending of lines as `LF` (unix style)
    - To avoid Git converting from `LF` to `CRLF`, run the following commands:
      ```shell
      git config --global core.autocrlf false
      git config --global core.eol lf
      git rm --cached -r .
      git reset --hard
      ```
  - **On VS Code you get this errors: "JSX element implicitly has type 'any'..."**
    - This happens because your Typescript IntelliSense is not working properly
    - To fix it reload your code editor: `Ctrl + p` > `Developer: Reload Window`

  ## More Topics
  - [Configuring Supported Browsers](https://create-react-app.dev/docs/supported-browsers-features#configuring-supported-browsers)
  - [Updating React to New Releases](https://create-react-app.dev/docs/updating-to-new-releases)

  ## Documentation & Training
  - [Official React Documentation](https://es.reactjs.org)
  - [React Function Components](https://www.robinwieruch.de/react-function-component)
  - [The TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
  - [ES6](http://es6-features.org/#Constants)
  - [Sass Basics](https://sass-lang.com/guide)
  - [MUI Crash Course](https://www.youtube.com/watch?v=o1chMISeTC0)
  - [MUI From Zero to Hero](https://www.youtube.com/playlist?list=PLDxCaNaYIuUlG5ZqoQzFE27CUOoQvOqnQ)
  - [MUI Components](https://mui.com/material-ui/react-autocomplete)
  - [MUI Templates](https://mui.com/material-ui/getting-started/templates)

  ## Creator
  **Juan Cuartas** https://github.com/equisoide

  ## Copyright and License
  Code and documentation released under [the MIT license](https://github.com/equisoide/react-mui-ts-template/blob/master/LICENSE)
  ````
- Save

## 14. Delete unnecessary files
- Go to **src** folder and delete the following files:
  - **App.css**
  - **App.test.tsx**
  - **App.tsx**
  - **index.css**
  - **logo.svg**

## 15. Update [reportWebVitals.ts](https://web.dev/vitals)
  - Create **src/util** folder
  - Move **reportWebVitals.ts** file to that folder:
    - Update imports for 'reportWebVitals.ts'? > **Yes** (VS Code)
  - Rename **reportWebVitals.ts** to **web-vitals.ts**:
    - Update imports for 'reportWebVitals.ts'? > **Yes** (VS Code)
  - Replace **web-vitals.ts** with the following code:
    ```ts
    // Web Vitals is an initiative by Google to provide unified guidance
    // for quality signals that are essential to delivering a great user
    // experience on the web.
    // Learn more: https://web.dev/vitals
    import { ReportHandler } from 'web-vitals';

    // Initializes Web Vitals with a custom reporter
    const reportWebVitals = (onPerfEntry?: ReportHandler) => {
      if (onPerfEntry && onPerfEntry instanceof Function) {
        import('web-vitals').then(({
          getCLS,
          getFID,
          getFCP,
          getLCP,
          getTTFB,
        }) => {
          getCLS(onPerfEntry);
          getFID(onPerfEntry);
          getFCP(onPerfEntry);
          getLCP(onPerfEntry);
          getTTFB(onPerfEntry);
        });
      }
    };

    // Default export
    export default reportWebVitals;
    ```
  - Save

## 16. Update index.html
- Open **pubic/index.html** file
- After the `apple-touch-icon` link reference, add the following:
  ```html
      <!--
        The easiest way to set up icon fonts for use in any web page is through Google Fonts
        See: https://developers.google.com/fonts/docs/material_icons
      -->
      <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
  ```
- Replace the **title** by the following:
  ```html
  <title>%REACT_APP_PACKAGE_NAME%</title>
  ```
- Save

## 17. Create styles
- Create **src/styles** folder
- Inside **src/styles** folder, create **_reset.scss** file with the following styles:
  ```scss
  /**
   * A simple set of CSS rules that resets the styling
   * of all HTML elements to a consistent baseline.
   */
  *,
  *::before,
  *::after {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  html {
    font-size: 100%; /* 1rem = 16px */
  }

  body {
    font-size: 1rem; /* 16px */
    font-family: Roboto, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }
  ```
- Save
- Inside **src/styles** folder, create **main.scss** file with the following styles:
  ```scss
  // External imports
  @import "@fontsource/roboto/300.css";
  @import "@fontsource/roboto/400.css";
  @import "@fontsource/roboto/500.css";
  @import "@fontsource/roboto/700.css";

  // Local imports
  @import "reset";
  ```
- Save

## 18. Configure [i18next](https://react.i18next.com)
- Create **src/lang** folder
- Inside **src/lang** folder, create **resources.en.json** file with the following content:
  ```json
  {
    "hello-world": "Hello World!"
  }
- Save
- Inside **src/lang** folder, create **resources.es.json** file with the following content:
  ```json
  {
    "hello-world": "¡Hola Mundo!"
  }
- Save
- Inside **src/lang** folder, create **index.ts** file with the following code:
  ```ts
  /**
   * react-i18next is a powerful internationalization framework for
   * React/ReactNative which is based on i18next.
   * Learn more: https://react.i18next.com
   */

  // External imports
  import LanguageDetector from 'i18next-browser-languagedetector';
  import i18n from 'i18next';
  import { initReactI18next } from 'react-i18next';

  // Local imports
  import resourcesEn from './resources.en.json';
  import resourcesEs from './resources.es.json';

  // Init the i18next module with the resource files
  const initI18n = () => {
    i18n
      .use(LanguageDetector)
      .use(initReactI18next)
      .init({
        resources: {
          en: {
            translations: { ...resourcesEn },
          },
          es: {
            translations: { ...resourcesEs },
          },
        },
        fallbackLng: 'en',
        debug: false,
        ns: ['translations'],
        defaultNS: 'translations',
        keySeparator: false,
        interpolation: {
          escapeValue: false,
        },
      });
  };

  // Default export
  export default initI18n;
  ```
- Save

## 19. Configure [Storybook](https://storybook.js.org)
- Open **.storybook/main.js** file:
- Add the following comments at the top of the file:
  ```js
  /**
   * This file controls the Storybook server's behavior.
   * You must restart Storybook’s process when you change it.
   * Learn more: https://storybook.js.org/docs/react/configure/overview
   */
  ```
- [Disable Telemetry](https://storybook.js.org/docs/react/configure/telemetry):
  ```js
  "core": {
    ...
    "disableTelemetry": true,
  }
  ```
- Add **typescript** and **webpackFinal** after **core**:
  ```js
  "typescript": {
    "reactDocgen": 'react-docgen-typescript-plugin'
  },
  "webpackFinal": async (config) => {
    injectEnvVariables(config);
    return config;
  },
  ```
- Add **injectEnvVariables** after **module.exports**:
  ```js
  // Manually inject environment variables into the webpack config object.
  // Note that otherwise, only `STORYBOOK_*` prefix env vars are supported.
  // Ref: https://github.com/storybookjs/storybook/issues/12270
  function injectEnvVariables(config) {
    const findPlugin = (name) => config.plugins.find(
      ({ constructor }) => constructor && constructor.name === name,
    );

    const definePlugin = findPlugin('DefinePlugin');
    const interpolateHtmlPlugin = findPlugin('InterpolateHtmlPlugin');
    const definitions = Object.keys(definePlugin.definitions);
    const replacements = Object.keys(interpolateHtmlPlugin.replacements);
    const isMissingKey = (key) => !definitions.includes(`process.env.${key}`);
    const missingKeys = replacements.filter(isMissingKey);

    missingKeys.forEach((key) => {
      definePlugin.definitions[`process.env.${key}`] = JSON.stringify(
        interpolateHtmlPlugin.replacements[key],
      );
    });
  };
  ```
- Add trailing commas where missing
- Save
- Open **.storybook/preview.js** file:
- Add the following code at the top of the file:
  ```js
  /**
   * Use preview.js for global code that applies to all stories.
   * Learn more: https://storybook.js.org/docs/react/configure/overview
   */
  import { addParameters } from '@storybook/client-api';
  import initI18n from '../src/lang';
  import '../src/styles/main.scss';

  // Global initialization
  initI18n();
  ```
- Save
- Create **.storybook/favicon.svg** file with the following content:
  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <svg width="16px" height="20px" viewBox="0 0 16 20" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
      <title>storybook-icon/default</title>
      <defs>
          <path d="M0.620279251,18.4293378 L0.000720094879,1.92089246 C-0.0197415137,1.37568327 0.398305374,0.913624829 0.942835893,0.879591672 L14.984425,0.00199234997 C15.5386921,-0.0326493419 16.016097,0.388590257 16.0507387,0.942857327 C16.0520438,0.963739972 16.0526969,0.984658267 16.0526969,1.00558166 L16.0526969,18.9944525 C16.0526969,19.549801 15.6024979,20 15.0471494,20 C15.0321047,20 15.017062,19.9996624 15.0020325,19.9989873 L1.58000252,19.3961612 C1.05726753,19.3726835 0.639903368,18.9522316 0.620279251,18.4293378 Z" id="path-1"></path>
      </defs>
      <g id="storybook-icon/default" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
          <mask id="mask-2" fill="white">
              <use xlink:href="#path-1"></use>
          </mask>
          <use id="path1_fill-path" fill="#FF4785" fill-rule="nonzero" xlink:href="#path-1"></use>
          <path d="M11.8537041,2.4583186 L11.9496157,0.15151183 L13.8779482,0 L13.9610222,2.37893005 C13.9639134,2.46172229 13.8991408,2.53118243 13.8163485,2.53407359 C13.780898,2.53531156 13.7461558,2.52394606 13.7182911,2.50199528 L12.9746642,1.91619251 L12.094228,2.584057 C12.0282261,2.63412351 11.934134,2.62120528 11.8840675,2.55520331 C11.862992,2.52741977 11.8522554,2.49316117 11.8537041,2.4583186 Z" id="path2_fill-path" fill="#FFFFFF" fill-rule="nonzero" mask="url(#mask-2)"></path>
          <path d="M9.38755179,7.53827354 C9.38755179,7.92949033 12.0227349,7.74199033 12.376485,7.4671875 C12.376485,4.80309448 10.9469952,3.40315552 8.32935804,3.40315552 C5.71172085,3.40315552 4.24510144,4.82487559 4.24510144,6.95745682 C4.24510144,10.6717025 9.25759817,10.7427885 9.25759817,12.7687407 C9.25759817,13.337429 8.97912613,13.6750877 8.36648764,13.6750877 C7.56820113,13.6750877 7.25259948,13.2673973 7.28972909,11.8812195 C7.28972909,11.5805064 4.24510144,11.4867564 4.15227743,11.8812195 C3.91590969,15.2404217 6.0087577,16.2093445 8.40361725,16.2093445 C10.7242176,16.2093445 12.5435683,14.9724079 12.5435683,12.7331976 C12.5435683,8.75237935 7.45681231,8.85900841 7.45681231,6.88637078 C7.45681231,6.08665282 8.050886,5.98002376 8.40361725,5.98002376 C8.7749133,5.98002376 9.4432462,6.04546668 9.38755179,7.53827354 Z" id="path9_fill-path" fill="#FFFFFF" fill-rule="nonzero" mask="url(#mask-2)"></path>
      </g>
  </svg>
  ```
- Save
- Create file **.storybook/manager.js** with the following code:
  ```js
  /**
   * This file allows you to customize how Storybook’s app UI renders.
   * That is, everything outside of the Canvas (preview iframe).
   * Learn more: https://storybook.js.org/blog/declarative-storybook-configuration
   */
  import favicon from './favicon.svg';

  // Change Storybook Favicon.
  // Ref: https://github.com/storybookjs/storybook/issues/6155
  const injectFavicon = () => {
    const link = document.createElement('link');

    link.setAttribute('rel', 'icon');
    link.setAttribute('href', favicon);
    link.setAttribute('type', 'image/svg+xml');

    document.head.appendChild(link);
  };

  injectFavicon();
  ```
- Save
- Go to **src/stories** folder and delete the following files:
  - **button.css**
  - **Button.stories.tsx**
  - **Button.tsx**
  - **header.css**
  - **Header.stories.tsx**
  - **Header.tsx**
  - **page.css**
  - **Page.stories.tsx**
  - **Page.tsx**
- Rename **Introduction.stories.mdx** to **introduction.stories.mdx**
- Open **introduction.stories.mdx** file:
  - Replace `Example/Introduction` by `Introduction`
  - Replace **# Welcome to Storybook** by the following:
    ```html
    <h1>{process.env.REACT_APP_PACKAGE_NAME}</h1>
    <h2>{process.env.REACT_APP_PACKAGE_VERSION}</h2>
    ```
  - Replace `stories/Introduction.stories.mdx` by `stories/introduction.stories.mdx`
- Save

## 20. Update [setupTests.ts](https://github.com/testing-library/jest-dom)
- Open **src/setupTests.ts** file and replace with the following code:
  ```ts
  /**
   * jest-dom adds custom jest matchers for asserting on DOM nodes.
   * It allows you to do things like:
   * expect(element).toHaveTextContent(/react/i)
   * Learn more: https://github.com/testing-library/jest-dom
   */
  import '@testing-library/jest-dom';
  import initI18n from './lang';

  // Global initialization
  initI18n();
  ```
- Save

## 21. Create HelloWorld component
- Create **src/components/HelloWorld** folder
- Inside **src/components/HelloWorld** folder, create **index.module.scss** file with the following code:
  ```scss
  /**
   * Style file for the HelloWorld component.
   */
  .info {
    font-size: 0.875rem; /* 14px */
  }
  ```
- Save
- Inside **src/components/HelloWorld** folder, create **index.tsx** file with the following code:
  ```tsx
  /**
   * The HelloWorld component renders an alert with
   * the package name, version and environment.
   */

  // External imports
  import Alert from '@mui/material/Alert';
  import AlertTitle from '@mui/material/AlertTitle';
  import Box from '@mui/material/Box';
  import { AlertProps, BoxProps } from '@mui/material';
  import { useTranslation } from 'react-i18next';

  // Local imports
  import styles from './index.module.scss';

  // Component props
  export interface HelloWorldProps {
    /**
     * The alert message styles.
     * See: https://mui.com/material-ui/api/alert
     */
    alert?: AlertProps,
    /**
     * The box container styles.
     * See: https://mui.com/material-ui/api/box
     */
    box?: BoxProps,
  }

  // Component definition
  function HelloWorld({ alert, box } : HelloWorldProps) {
    const { t } = useTranslation();

    const defaults = HelloWorld.defaultProps;
    const boxProps = { ...defaults.box, ...box } as BoxProps;
    const alertProps = { ...defaults.alert, ...alert } as AlertProps;

    const name = process.env.REACT_APP_PACKAGE_NAME;
    const version = process.env.REACT_APP_PACKAGE_VERSION;
    const env = process.env.REACT_APP_ENV;

    return (
      <Box {...boxProps}>
        <Alert {...alertProps}>
          <AlertTitle>{t('hello-world')}</AlertTitle>
          <div className={styles.info}>{name}</div>
          <div className={styles.info}>{version}</div>
          <div className={styles.info}>{env}</div>
        </Alert>
      </Box>
    );
  }

  // Default props
  HelloWorld.defaultProps = {
    alert: {
      severity: 'success',
      sx: { width: 300 },
      variant: 'filled',
    },
    box: {},
  };

  // Default export
  export default HelloWorld;
  ```
- Save
- Inside **src/components/HelloWorld** folder, create **index.test.tsx** file with the following code:
  ```tsx
  /**
   * Testing file for the HelloWorld component.
   */
  import { render, screen } from '@testing-library/react';
  import HelloWorld from '.';

  test('Render HelloWorld Component', () => {
    render(<HelloWorld />);
    const element = screen.getByText(/Hello World!/i);
    expect(element).toBeInTheDocument();
  });
  ```
- Save
- Inside **src/components/HelloWorld** folder, create **index.stories.tsx** file with the following code:
  ```tsx
  /**
   * Storybook file for the HelloWorld component.
   */
  import { ComponentMeta, ComponentStory } from '@storybook/react';
  import HelloWorld from '.';

  // Story placement in the story list
  export default {
    title: 'Components/HelloWorld',
    component: HelloWorld,
  } as ComponentMeta<typeof HelloWorld>;

  const Template: ComponentStory<typeof HelloWorld> = (args) => <HelloWorld {...args} />;

  // Story #1
  export const Green = Template.bind({});
  Green.args = {
  };

  // Story #2
  export const Red = Template.bind({});
  Red.args = {
    alert: { severity: 'error' },
  };
  ```
- Save

## 22. Create Home page
- Create **src/pages/Home** folder
- Inside **src/pages/Home** folder, create **index.tsx** file with the following code:
  ```tsx
  // Local imports
  import HelloWorld from '../../components/HelloWorld';

  // Component definition
  function HomePage() {
    return (
      <HelloWorld
        box={{
          sx: {
            background: 'rgb(0, 30, 60)',
            height: '100vh',
            display: 'flex',
            justifyContent: 'center',
            alignItems: 'center',
          },
        }}
      />
    );
  }

  // Default export
  export default HomePage;
  ```
- Save
- Inside **src/pages/Home** folder, create **index.test.tsx** file with the following code:
  ```tsx
  // External imports
  import { render, screen } from '@testing-library/react';

  // Local imports
  import HomePage from '.';

  test('Render HomePage', () => {
    render(<HomePage />);
    const element = screen.getByText(/Hello World!/i);
    expect(element).toBeInTheDocument();
  });
  ```
- Save
- Inside **src/pages/Home** folder, create **index.stories.tsx** file with the following code:
  ```tsx
  // External imports
  import { ComponentMeta } from '@storybook/react';

  // Local imports
  import HomePage from '.';

  // Story placement in the story list
  export default {
    title: 'Pages/Home',
    component: HomePage,
    parameters: {
      layout: 'fullscreen',
    },
  } as ComponentMeta<typeof HomePage>;

  // Default export
  export const Default = () => <HomePage />;
  ```
- Save

## 23. Create App component
- Create **src/app** folder
- Inside **src/app** folder, create **index.tsx** file with the following code:
  ```tsx
  // External imports
  import { Routes, Route } from 'react-router-dom';

  // Local imports
  import HomePage from '../pages/Home';

  // Component definition
  function App() {
    return (
      <Routes>
        <Route path="/" element={<HomePage />} />
        <Route path="home" element={<HomePage />} />
      </Routes>
    );
  }

  // Default export
  export default App;
  ```
- Save

## 24. Update index.tsx
- Open **src/index.tsx** file and replace all code with the following:
  ```tsx
  // External imports
  import ReactDOM from 'react-dom/client';
  import { BrowserRouter } from 'react-router-dom';
  import { StrictMode } from 'react';

  // Local imports
  import App from './app';
  import initI18n from './lang';
  import reportWebVitals from './util/web-vitals';
  import './styles/main.scss';

  // Global initialization
  initI18n();

  const htmlRoot = document.getElementById('root') as HTMLElement;
  const reactRoot = ReactDOM.createRoot(htmlRoot);

  reactRoot.render(
    process.env.REACT_APP_SCRICT_MODE === 'true' ? (
      <StrictMode>
        <BrowserRouter>
          <App />
        </BrowserRouter>
      </StrictMode>
    ) : (
      <BrowserRouter>
        <App />
      </BrowserRouter>
    ),
  );

  if (process.env.REACT_APP_ENV !== 'production') {
    // If you want to start measuring performance in your app, pass a function
    // to log results (for example: reportWebVitals(console.log))
    // or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
    // eslint-disable-next-line no-console
    reportWebVitals(console.log);
  }
  ```
- Save

## 25. Test everything is working fine
- Delete **node_modules** folder
- Install project dependencies for the first time: `npm run init`
- Restart VS Code in order to refresh **TypeScript Intellisense**
- Analyse **JavaSript/TypeScript** code: `npm run lint`
- Try to fix **JavaSript/TypeScript** errors: `npm run lint:f`
- Analyses **CSS**/**SCSS** styles: `npm run slint`
- Try to fix **CSS**/**SCSS** errors: `npm run slint:f`
- Execute Unit Tests outputting to **out/coverage**: `npm test`
- Run the App in http://localhost:4000: `npm start`
- Create a locally trusted CA: `mkcert -install`
- Generate an SSL certificate: `mkcert localhost`
- Run the App in https://localhost:4001: `npm run start-https` (HTTPS)
- Build the App to **out/build/local**: `npm run build:l`
- Build the App to **out/build/development**: `npm run build:d`
- Build the App to **out/build/qa**: `npm run build:q`
- Build the App to **out/build/staging**: `npm run build:s`
- Build the App to **out/build/production**: `npm run build`
- Run Storybook in http://localhost:4002: `npm run sbook`
- Run Storybook in https://localhost:4003: `npm run sbook-https` (HTTPS)
- Build Storybook to **out/storybook/local**: `npm run sb-build:l`
- Build Storybook to **out/storybook/development**: `npm run sb-build:d`
- Build Storybook to **out/storybook/qa**: `npm run sb-build:q`
- Build Storybook to **out/storybook/staging**: `npm run sb-build:s`
- Build Storybook to **out/storybook/production**: `npm run sb-build`

## Creator
**Juan Cuartas** https://github.com/equisoide

## Copyright and license
Code and documentation released under [the MIT license](https://github.com/equisoide/react-mui-ts-steps/blob/master/LICENSE)
