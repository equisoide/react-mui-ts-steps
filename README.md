# Creating a React-MUI-TypeScript Template

The purpose of this tutorial is to document the step by step on how to create a [React-MUI-TypeScript Template](https://github.com/equisoide/react-mui-ts-template) from scratch, so that it will serve as a reference guide for myself and for others.

## 1. Install required libraries
  - [React App with TypeScript template](https://github.com/facebook/create-react-app/tree/main/packages/cra-template-typescript):
    - `npx create-react-app react-mui-ts-template --template typescript`
    - `cd react-mui-ts-template`
    - Go to **package.json** file and rearrange `dependencies` as follow (keep your current versions):
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
        "@types/node": "^16.11.41",
        "@types/react": "^18.0.12",
        "@types/react-dom": "^18.0.5",
        "typescript": "^4.7.3"
      },
      ```
    - Save
    - Delete **node_modules** and **package-lock.json** file
    - `npm install`
  - [MUI (Material UI)](https://mui.com/material-ui/getting-started/installation):
    - `npm i @mui/material @emotion/react @emotion/styled`
    - `npm i @fontsource/roboto`
    - `npm i @mui/icons-material`
  - [react-i18next](https://react.i18next.com/guides/quick-start):
    - `npm i i18next react-i18next`
    - `npm i i18next-browser-languagedetector`
  - [env-cmd](https://github.com/toddbluhm/env-cmd):
    - `npm i env-cmd --save-dev`
  - [Stylelint](https://stylelint.io/user-guide/get-started):
    - `npm i stylelint stylelint-config-standard --save-dev`
  - [ESLint](https://eslint.org/docs/user-guide/getting-started):
    - `npm i eslint --save-dev`
    - `npm init @eslint/config`
      - To check syntax, find problems, and enforce code style
      - JavaScript modules (import/export)
      - React
      - Does your project use TypeScript? › **Yes**
      - Where does your code run? › **Browser**
      - Use a popular style guide › **Airbnb**
      - What format do you want your config file to be in? › **JavaScript**
      - Would you like to install them now? › **Yes**
      - Which package manager do you want to use? › **npm**
  - [Storybook](https://storybook.js.org/docs/react/get-started/install):
    - `npx storybook init`
      - Do you want to run the eslintPlugin migration on your project? › **y**

## 2. Install VS Code recomented extensions for this project
  - [DotENV](https://marketplace.visualstudio.com/items?itemName=mikestead.dotenv)
  - [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
  - [EditorConfig](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig)
  - [Icons](https://marketplace.visualstudio.com/items?itemName=robertohuertasm.vscode-icons)
  - [MDX](https://marketplace.visualstudio.com/items?itemName=silvenon.mdx)
  - [NpmIntellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.npm-intellisense)
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

## 4. Configure [package.json](https://docs.npmjs.com/cli/v7/configuring-npm/package-json)
  - Add **description** after **version**:
    > `"description": "React, MUI and TypeScript template",`
  - Set the package as [public](https://docs.npmjs.com/cli/v7/configuring-npm/package-json#private):
    > `"private": false,`
  - Add the [homepage](https://stackoverflow.com/questions/43011207/using-homepage-in-package-json-without-messing-up-paths-for-localhost) URL after **private**:
    > `"homepage": "./",`
  - Add **keywords** after **homepage**:
    ```json
    "keywords": [
      "airbnb",
      "emotion",
      "es6",
      "eslint",
      "hooks",
      "i18next",
      "jest",
      "mui",
      "react",
      "roboto",
      "spa",
      "storybook",
      "stylelint",
      "template", 
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
      "lint:c": "./node_modules/.bin/stylelint \"src/**/*.css\"",
      "sbook": "env-cmd --no-override -f ./.env-override/.env.local start-storybook -p 3001 -s public",
      "sbook:d": "env-cmd --no-override -f ./.env-override/.env.development build-storybook -s public -o ./out/storybook/development",
      "sbook:l": "env-cmd --no-override -f ./.env-override/.env.local build-storybook -s public -o ./out/storybook/local",
      "sbook:p": "env-cmd --no-override -f ./.env-override/.env.production build-storybook -s public -o ./out/storybook/production",
      "sbook:q": "env-cmd --no-override -f ./.env-override/.env.qa build-storybook -s public -o ./out/storybook/qa",
      "sbook:s": "env-cmd --no-override -f ./.env-override/.env.staging build-storybook -s public -o ./out/storybook/staging",
      "start": "env-cmd --no-override -f ./.env-override/.env.local react-scripts start",
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
        "!src/util/report-web-vitals.ts"
      ]
    },
    ```
  - Save

## 5. Configure [tsconfig.json](https://www.typescriptlang.org/tsconfig)
  - Add the following comments before **compilerOptions**:
    ```js
      // Specifies the root files and the compiler options required
      // to compile the TypeScript project.
      // Learn more: https://www.typescriptlang.org/tsconfig
    ```
  - Enable [ES6](http://es6-features.org) features:
    > `"target": "es6",`
  - Disable **TypeScript** [incremental](https://www.typescriptlang.org/tsconfig#incremental) compilation (I had experienced cache issues with it):
    > `"incremental": false,`
  - Put **lib** on a single line:
    > `"lib": ["dom", "dom.iterable", "esnext"],`
  - Sort **compilerOptions** items by selecting all of them and pressing `F9` (SortLines plugin)
  - Remove trailing comma from the last item of **compilerOptions**
  - Replace **include** array with the following:
    > `"include": ["src/**/*"]`
  - Save

## 6. Configure [.eslintrc](https://eslint.org/docs/user-guide/configuring)
  - Rename **.eslintrc.js** to **.eslintrc**
  - Remove `module.exports = ` (The file is now a **JSON** document)
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
      "airbnb",
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
      "import/extensions": ["error", "ignorePackages", { "js": "never", "jsx": "never", "ts": "never", "tsx": "never" }],
      "import/no-extraneous-dependencies": ["error", { "devDependencies": true }],
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
      }
    }
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
        "extends": "stylelint-config-standard",
        "rules": {
            "declaration-block-trailing-semicolon": "always",
            "declaration-no-important": true,
            "font-family-no-missing-generic-family-keyword": null,
            "indentation": 2
        }
    }
    ```
  - Save

## 9. Add [VS Code Settings](https://code.visualstudio.com/docs/getstarted/settings)
  - Create **.vscode** folder at the app's root level
  - Inside **.vscode** folder, create **extensions.json** file with the following configuration:
    ```js
    {
      // See http://go.microsoft.com/fwlink/?LinkId=827846
      // for the documentation about the extensions.json format
      "recommendations": [
        "EditorConfig.EditorConfig",
        "Tyriar.sort-lines",
        "christian-kohler.npm-intellisense",
        "dbaeumer.vscode-eslint",
        "mikestead.dotenv",
        "silvenon.mdx",
        "stylelint.vscode-stylelint",
        "vscode-icons-team.vscode-icons"
      ]
    }
    ```
  - Save
  - Inside **.vscode** folder, create **launch.json** file with the following configuration:
    ```js
    {
      // Use IntelliSense to learn about possible attributes.
      // Hover to view descriptions of existing attributes.
      // Learn more: https://go.microsoft.com/fwlink/?linkid=830387
      "version": "0.2.0",
      "configurations": [
        {
          "type": "pwa-chrome",
          "request": "launch",
          "name": "Launch Chrome against localhost",
          "url": "http://localhost:3000",
          "webRoot": "${workspaceFolder}"
        }
      ]
    }
    ```
  - Save
  - Inside **.vscode** folder, create **settings.json** file with the following configuration:
    ```js
    {
      // Use IntelliSense to learn about possible attributes.
      // Hover to view descriptions of existing attributes.
      // Learn more: https://code.visualstudio.com/docs/getstarted/settings
      "editor.codeActionsOnSave": {
        "source.fixAll": true
      },
      "explorer.sortOrder": "type",
      "files.eol": "\n",
      "search.exclude": {
        "**/node_modules": true,
        "**/out": true,
        "package-lock.json": true
      }
    }
    ```
  - Save

## 10. Configure [.gitignore](https://git-scm.com/docs/gitignore)
  - Remove `/coverage`
  - Remove `.env.local`
  - Remove `.env.development.local`
  - Remove `.env.test.local`
  - Remove `.env.production.local`
  - Replace `/build` by `/out`
  - Add `# log` comment before `npm-debug.log*`
  - Save

## 11. Add [Environment Files](https://create-react-app.dev/docs/adding-custom-environment-variables/#adding-development-environment-variables-in-env)
  - Create **.env** file at the app's root level
  - Add the following configuration:
    ```env
    # This file defines the variables common to all environments.
    # Variables in this file will be overridden by each specific environment.
    # Shell variables never get overridden.
    # Name variables beginning with "REACT_APP_".
    # Access variables from the "process.env." object.
    # Restart the development server every time you change a variable.
    # Learn more: https://create-react-app.dev/docs/adding-custom-environment-variables
    # Advanced config: https://create-react-app.dev/docs/advanced-configuration
    HTTPS=false
    PORT=3000
    REACT_APP_PACKAGE_NAME=${npm_package_name}
    REACT_APP_PACKAGE_VERSION=${npm_package_version}
    ```
  - Save
  - Create **.env-override** folder at the app's root level
  - Inside **.env-override** folder, create the following files:
    - **.env.development**
      ```env
      # Variables in this file are injected by the following scripts:
      # - "build:d" Builds the App to `out/build/development`
      # - "sbook:d" Builds Storybook to `out/storybook/development`
      BUILD_PATH='./out/build/development'
      REACT_APP_ENV='development'
      ```
    - **.env.local**
      ```env
      # Variables in this file are injected by the following scripts:
      # - "start"   Runs the App in http://localhost:3000
      # - "sbook"   Runs Storybook in http://localhost:3001
      # - "build:l" Builds the App to `out/build/local`
      # - "sbook:l" Builds Storybook to `out/storybook/local`
      BUILD_PATH='./out/build/local'
      REACT_APP_ENV='local'
      ```
    - **.env.production**
      ```env
      # Variables in this file are injected by the following scripts:
      # - "build"   Builds the App to `out/build/production`
      # - "sbook:p" Builds Storybook to `out/storybook/production`
      BUILD_PATH='./out/build/production'
      REACT_APP_ENV='production'
      ```
    - **.env.qa**
      ```env
      # Variables in this file are injected by the following scripts:
      # - "build:q" Builds the App to `out/build/qa`
      # - "sbook:q" Builds Storybook to `out/storybook/qa`
      BUILD_PATH='./out/build/qa'
      REACT_APP_ENV='qa'
      ```
    - **.env.staging**
      ```env
      # Variables in this file are injected by the following scripts:
      # - "build:s" Builds the App to `out/build/staging`
      # - "sbook:s" Builds Storybook to `out/storybook/staging`
      BUILD_PATH='./out/build/staging'
      REACT_APP_ENV='staging'
      ```
    - **.env.test**
      ```env
      # Variables in this file are injected by the following scripts:
      # - "test" Executes Unit Tests outputting to `out/coverage`
      BUILD_PATH='./out/build/test'
      REACT_APP_ENV='test'
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

    This template is intended to help you start a new `React SPA` project from scratch with a comprehensive folder structure, required dependencies, built-in configurations, example components and good practices for React Web Development. The project was bootstrapped with [Create React App](https://create-react-app.dev) following this [Tutorial](https://github.com/equisoide/react-mui-ts-steps). Below you will find some information on how to perform common tasks.

    ## Supported Language Features
       This project supports a superset of the latest **JavaScript** standard. In addition to [ES6](http://es6-features.org) syntax features, it also supports:
       - [Exponentiation Operator](https://github.com/tc39/proposal-exponentiation-operator) (ES2016)
       - [Async/await](https://github.com/tc39/proposal-async-await) (ES2017)
       - [Object Rest/Spread Properties](https://github.com/tc39/proposal-object-rest-spread) (ES2018)
       - [Dynamic import()](https://github.com/tc39/proposal-dynamic-import) (stage 4 proposal)
       - [Class Fields and Static Properties](https://github.com/tc39/proposal-class-public-fields) (part of stage 3 proposal)
       - [TSX](https://www.typescriptlang.org/docs/handbook/jsx.html) and [TypeScript](https://www.typescriptlang.org)

    ## Core Libraries
    - [React 18.2.0](https://reactjs.org) with `React Scripts 5.0.1`
    - [MUI 5.8.4](https://mui.com) with `Emotion` styling engine, `Roboto Fonts` and `Google Font Icons`
    - [TypeScript 4.7.3](https://www.typescriptlang.org) with [ES6](http://es6-features.org)
    - [I18next 21.8.9](https://react.i18next.com) for internationalization

    ## Documentation Tools
    - [Storybook 6.5.9](https://storybook.js.org) to document pages and components

    ## Code Quality & Performance
    - [ESLint 8.17.0](https://eslint.org) with `Airbnb`, `TypeScript`, `React`, `React Hooks` and `Jest` configuration
    - [Stylelint 14.9.1](https://stylelint.io) to analyse `CSS` files
    - [Jest 27.5.2](https://jestjs.io/docs/getting-started) to test `JavaScript`/`TypeScript` files
    - [React Testing Library 13.3.0](https://testing-library.com/docs/react-testing-library/intro) to test components
    - [Web Vitals 2.1.4](https://web.dev/vitals) to meassure performance

    ## Built-in Settings
    - [.editorconfig](https://editorconfig.org) settings to standardize charset, ending of lines and indentation
    - [.vscode](https://code.visualstudio.com/docs/getstarted/settings) settings with integrated `Chrome Debugger`, faster search results and auto-format on save
    - [Environment files](https://create-react-app.dev/docs/adding-custom-environment-variables) for `local`, `test`, `development`, `qa`, `staging` and `production`

    ## Environment Quick Setup

    1. Install [NodeJs](https://nodejs.org/es/download)
    2. Install [Git](https://git-scm.com/downloads)
    3. Install [VS Code](https://code.visualstudio.com/download)
    4. Install VS Code recomented extensions for this project:
       * [DotENV](https://marketplace.visualstudio.com/items?itemName=mikestead.dotenv)
       * [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
       * [EditorConfig](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig)
       * [Icons](https://marketplace.visualstudio.com/items?itemName=robertohuertasm.vscode-icons)
       * [MDX](https://marketplace.visualstudio.com/items?itemName=silvenon.mdx)
       * [NpmIntellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.npm-intellisense)
       * [SortLines](https://marketplace.visualstudio.com/items?itemName=Tyriar.sort-lines)
       * [Stylelint](https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint)
    5. Install [React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi) for Google Chrome

    ## Running & Debugging the application for the first time

    1. Clone repo:
       > `git clone https://github.com/equisoide/react-mui-ts-template.git`
    2. Install all required packages (It will perform a [Clean install](https://docs.npmjs.com/cli/v8/commands/npm-ci)):
       > `npm run init`
    3. Restart VS Code in order to refresh **TypeScript Intellisense**, otherwise you might see TypeScript errors in the editor
    4. Start the application:
       > `npm start`
    5. Start debugging in `VS Code` by pressing `F5` or by clicking on `Run and Debug` > `Green debug icon`
    6. You can now set breakpoints, debug and inspect the React component hierarchies into the [React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)

    ## Available Scripts
    | Command           | Description                                      | Evironment File  |
    | :---              | :---                                             | :---             |
    | `npm run init`    | Installs all dependencies for the first time     | N/A              |
    | `npm run lint`    | Analyses `JavaSript`/`TypeScript` code           | N/A              |
    | `npm run lint:f`  | Try to fix `JavaSript`/`TypeScript` errors       | N/A              |
    | `npm run lint:c`  | Analyses `CSS` files for potential errors        | N/A              |
    | `npm test`        | Executes Unit Tests outputting to `out/coverage` | .env.test        |
    | `npm start`       | Runs the App in http://localhost:3000            | .env.local       |
    | `npm run build`   | Builds the App to `out/build/production`         | .env.production  |
    | `npm run build:d` | Builds the App to `out/build/development`        | .env.development |
    | `npm run build:l` | Builds the App to `out/build/local`              | .env.local       |
    | `npm run build:q` | Builds the App to `out/build/qa`                 | .env.qa          |
    | `npm run build:s` | Builds the App to `out/build/staging`            | .env.staging     |
    | `npm run sbook`   | Runs Storybook in http://localhost:3001          | .env.local       |
    | `npm run sbook:d` | Builds Storybook to `out/storybook/development`  | .env.development |
    | `npm run sbook:l` | Builds Storybook to `out/storybook/local`        | .env.local       |
    | `npm run sbook:p` | Builds Storybook to `out/storybook/production`   | .env.production  |
    | `npm run sbook:q` | Builds Storybook to `out/storybook/qa`           | .env.qa          |
    | `npm run sbook:s` | Builds Storybook to `out/storybook/staging`      | .env.staging     |

    ## Working guidelines
    - Never delete and re-generate the `package-lock.json` file from scratch, it will break the App and Storybook! Let `npm` update that file every time you install a new dependency
    - Create reusable components inside `src/components` folder. Define each component in its own folder with the following structure:
      ```js
        + src/components/MyComponent  // Component name in PascalCase
          - index.stories.tsx         // Storybook documentation
          - index.test.tsx            // Jest testing file
          - index.tsx                 // Component definition
      ```
    - Prefer [Function Components](https://www.robinwieruch.de/react-function-component) over `Class components` they offer almost the same: `state` and `lifecycle methods`, with the plus they are more lightway, have a sophisticated `API` and require less code. With the introduction of `React Hooks` it's possible to write your entire application with just functions as `React components`:
        ```js
        import { Box, BoxProps } from '@mui/material';
        import { useTranslation } from 'react-i18next';

        export interface MyComponentProps {
          box?: BoxProps
        }

        function MyComponent({ box } : MyComponentProps) {
          const { t } = useTranslation();
          const boxProps = { ...MyComponent.defaultProps.box, ...box } as BoxProps;
          return (
            <Box {...boxProps}>
              {t('hello-world')}
            </Box>
          );
        }

        MyComponent.defaultProps = {
          box: {
            sx: { background: 'blue' },
          },
        };

        export default MyComponent;
        ```
    - In general use [Trailing Commas](https://blog.logrocket.com/best-practices-using-trailing-commas-javascript) (Except on `JSON` files), many coding styles now recommend using them all the time because they make it easier to add new parameters to your functions or copy/paste properties in arrays and objects and also helps with producing cleaner diff output
    - Add your own environment variables to the `.env-override/.env.local` file, this file should not be commited
    - Before running or building this application always run linters and unit tests
    - Linter is configured to accept valid ending of lines as `LF` (unix style), if you are on Windows, to avoid Git converting from `LF` to `CRLF`, run the following commands:
      ```shell
      git config --global core.autocrlf false
      git config --global core.eol lf
      ```

    ## Documentation & Training
    - [Official React Documentation](https://es.reactjs.org)
    - [React Function Components](https://www.robinwieruch.de/react-function-component)
    - [TypeScript](https://www.typescriptlang.org)
    - [ES6](http://es6-features.org/#Constants)
    - [MUI Crash Course](https://www.youtube.com/watch?v=o1chMISeTC0)
    - [MUI From Zero to Hero](https://www.youtube.com/playlist?list=PLDxCaNaYIuUlG5ZqoQzFE27CUOoQvOqnQ)
    - [MUI Components](https://mui.com/material-ui/react-autocomplete)
    - [MUI Templates](https://mui.com/material-ui/getting-started/templates)

    ## Creator

    **Juan Cuartas** https://twitter.com/juancuartas

    ## Copyright and license

    Code and documentation released under [the MIT license](https://github.com/equisoide/react-mui-ts-template/blob/master/LICENSE)
    ````
  - Save

## 14. Delete unnecessary root files
  - Go to **src** folder and delete the following files:
    - **App.css**
    - **App.test.tsx**
    - **App.tsx**
    - **index.css**
    - **logo.svg**

## 15. Customize [Web Vitals](https://web.dev/vitals)
  - Create **src/util** folder
  - Move **reportWebVitals.ts** file to that folder:
    > Update imports for 'reportWebVitals.ts'? > **Yes** (VS Code)
  - Rename **reportWebVitals.ts** to **report-web-vitals.ts**:
    > Update imports for 'reportWebVitals.ts'? > **Yes** (VS Code)
  - Add the following comments at the top of the file:
    ```js
    // Web Vitals is an initiative by Google to provide unified guidance
    // for quality signals that are essential to delivering a great user
    // experience on the web.
    // Learn more: https://web.dev/vitals
    ```
  - Refactor the file to fix linter issues:
    ```js
    import('web-vitals').then(({
      getCLS,
      getFID,
      getFCP,
      getLCP,
      getTTFB,
    }) => {
    ```
  - Save

## 16. Create and initialize styles folder
  - Create **src/styles** folder
  - In that folder create **site.css** file with the following styles:
    ```css
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family:
        -apple-system,
        BlinkMacSystemFont,
        "Segoe UI",
        Roboto,
        Oxygen,
        Ubuntu,
        Cantarell,
        "Fira Sans",
        "Droid Sans",
        "Helvetica Neue",
        sans-serif;
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
    }

    ```
  - Save

## 17. Add [Material Font Icons](https://developers.google.com/fonts/docs/material_icons)
  - Create **src/fonts** folder
  - In that folder copy file [material-icons-regular.ttf](https://github.com/equisoide/react-mui-ts-steps/raw/main/material-icons-regular.ttf)
  - Go to **src/styles** folder
  - In that folder create **material-icons.css** file with the following styles:
    ```css
    /**
     * Material icons to depict in simple and minimal forms the universal
     * concepts used commonly throughout a UI.
     * Learn more: https://developers.google.com/fonts/docs/material_icons
     */
    @font-face {
      font-family: "Material Icons";
      font-style: normal;
      font-weight: 400;
      src: url("../fonts/material-icons-regular.ttf") format("truetype");
    }

    .material-icons {
      font-family: "Material Icons";
      font-weight: normal;
      font-style: normal;
      font-size: 24px; /* Preferred icon size */
      display: inline-block;
      line-height: 1;
      text-transform: none;
      letter-spacing: normal;
      word-wrap: normal;
      white-space: nowrap;
      direction: ltr;

      /* Support for all WebKit browsers. */
      -webkit-font-smoothing: antialiased;

      /* Support for Safari and Chrome. */
      text-rendering: optimizelegibility;

      /* Support for Firefox. */
      -moz-osx-font-smoothing: grayscale;

      /* Support for IE. */
      font-feature-settings: "liga";
    }

    /* Rules for sizing the icon. */
    .material-icons.md-18 { font-size: 18px; }
    .material-icons.md-24 { font-size: 24px; }
    .material-icons.md-36 { font-size: 36px; }
    .material-icons.md-48 { font-size: 48px; }

    /* Rules for using icons as black on a light background. */
    .material-icons.md-dark { color: rgb(0 0 0 / 54%); }
    .material-icons.md-dark.md-inactive { color: rgb(0 0 0 / 26%); }

    /* Rules for using icons as white on a dark background. */
    .material-icons.md-light { color: rgb(255 255 255 / 100%); }
    .material-icons.md-light.md-inactive { color: rgb(255 255 255 / 30%); }
    ```
  - Save

## 18. Configure [i18ext](https://react.i18next.com)
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
    ```js
    // react-i18next is a powerful internationalization framework for
    // React / React Native which is based on i18next.
    // Learn more: https://react.i18next.com
    import LanguageDetector from 'i18next-browser-languagedetector';
    import i18n from 'i18next';
    import { initReactI18next } from 'react-i18next';
    
    import resourcesEn from './resources.en.json';
    import resourcesEs from './resources.es.json';

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

    export default initI18n;
    ```
  - Save

## 19. Configure [StoryBook](https://storybook.js.org)
  - Open **.storybook/main.js** file:
  - Add the following comments at the top of the file:
    ```js
    // This file controls the Storybook server's behavior.
    // You must restart Storybook’s process when you change it.
    // Learn more: https://storybook.js.org/docs/react/configure/overview
    ```
  - [Disable Telemetry](https://storybook.js.org/docs/react/configure/telemetry):
    ```js
    "core": {
      // By default StoryBook collects telemetry data.
      "disableTelemetry": true
    }
    ```
  - Add **webpackFinal** after **core**:
    ```js
    webpackFinal: async (config) => {
      // Manually inject environment variables.
      // Note that otherwise, only `STORYBOOK_*` prefix env vars are supported.
      // Ref: https://github.com/storybookjs/storybook/issues/12270
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

      return config;
    },
    ```
  - Save
  - Open **.storybook/preview.js** file:
  - Add the following code at the top of the file:
    ```js
    // Use preview.js for global code that applies to all stories.
    // Learn more: https://storybook.js.org/docs/react/configure/overview
    import initI18n from '../src/lang';

    import '@fontsource/roboto/300.css';
    import '@fontsource/roboto/400.css';
    import '@fontsource/roboto/500.css';
    import '@fontsource/roboto/700.css';

    import '../src/styles/site.css';
    import '../src/styles/material-icons.css';

    initI18n();
    ```
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
    // This file allows you to customize how Storybook’s app UI renders.
    // That is, everything outside of the Canvas (preview iframe).
    // Learn more: https://storybook.js.org/blog/declarative-storybook-configuration
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
    - Replace **# Welcome to Storybook** by the following:
      ```html
      <h1>{process.env.REACT_APP_PACKAGE_NAME}</h1>
      <h2>{process.env.REACT_APP_PACKAGE_VERSION}</h2>
      ```
    - Replace `stories/Introduction.stories.mdx` by `stories/introduction.stories.mdx`
  - Save

## 20. Configure [setupTests.ts](https://github.com/testing-library/jest-dom)
  - Open **src/setupTests.ts** file
  - Add the following initialization
    ```js
    import '@testing-library/jest-dom';
    import initI18n from './lang';

    initI18n();
    ```
  - Save

## 21. Update index.html Title
  - Go to **public/index.html** file
  - Replace the **title** by the following:
    ```html
    <title>%REACT_APP_PACKAGE_NAME%</title>
    ```
  - Save

## 22. Create HelloWorld component
  - Create **src/components/HelloWorld** folder
  - Inside **src/components/HelloWorld** folder, create **index.tsx** file with the following code:
    ```tsx
    import Alert from '@mui/material/Alert';
    import AlertTitle from '@mui/material/AlertTitle';
    import { AlertProps, Box, BoxProps } from '@mui/material';
    import { useTranslation } from 'react-i18next';

    export interface HelloWorldProps {
      alert?: AlertProps,
      box?: BoxProps
    }

    function HelloWorld({ alert, box } : HelloWorldProps) {
      const { t } = useTranslation();
      const boxProps = { ...HelloWorld.defaultProps.box, ...box } as BoxProps;
      const alertProps = { ...HelloWorld.defaultProps.alert, ...alert } as AlertProps;
      return (
        <Box {...boxProps}>
          <Alert {...alertProps}>
            <AlertTitle>{t('hello-world')}</AlertTitle>
            <div>{process.env.REACT_APP_PACKAGE_NAME}</div>
            <div>{process.env.REACT_APP_PACKAGE_VERSION}</div>
            <div>{process.env.REACT_APP_ENV}</div>
          </Alert>
        </Box>
      );
    }

    HelloWorld.defaultProps = {
      alert: {
        severity: 'success',
        sx: { width: 300 },
        variant: 'filled',
      },
      box: {},
    };

    export default HelloWorld;
    ```
  - Save
  - Inside **src/components/HelloWorld** folder, create **index.test.tsx** file with the following code:
    ```tsx
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
    import { ComponentMeta, ComponentStory } from '@storybook/react';
    import HelloWorld from '.';

    export default {
      title: 'Example/HelloWorld',
      component: HelloWorld,
    } as ComponentMeta<typeof HelloWorld>;

    const Template: ComponentStory<typeof HelloWorld> = (args) => <HelloWorld {...args} />;

    export const Green = Template.bind({});
    Green.args = {
    };

    export const Red = Template.bind({});
    Red.args = {
      alert: { severity: 'error' },
    };
    ```
  - Save

## 23. Update index.tsx file
  - Open **src/index.tsx** file and replace all code with the following:
    ```tsx
    import ReactDOM from 'react-dom/client';
    import { StrictMode } from 'react';

    import HelloWorld from './components/HelloWorld';
    import initI18n from './lang';
    import reportWebVitals from './util/report-web-vitals';

    import '@fontsource/roboto/300.css';
    import '@fontsource/roboto/400.css';
    import '@fontsource/roboto/500.css';
    import '@fontsource/roboto/700.css';

    import './styles/site.css';
    import './styles/material-icons.css';

    initI18n();

    const htmlRoot = document.getElementById('root') as HTMLElement;
    const reactRoot = ReactDOM.createRoot(htmlRoot);

    reactRoot.render(
      <StrictMode>
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
      </StrictMode>,
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

## 24. Test everything is working fine
   - Delete **node_modules** folder
   - Install all dependencies for the first time: `npm run init`
   - Restart VS Code in order to refresh **TypeScript Intellisense**
   - Analyse **JavaSript/TypeScript** code: `npm run lint`
   - Try to fix **JavaSript/TypeScript** errors: `npm run lint:f`
   - Analyse **CSS** files for potential errors: `npm run lint:c`
   - Execute Unit Tests outputting to **out/coverage**: `npm test`
   - Run the App in http://localhost:3000: `npm start`
   - Build the App to **out/build/production**: `npm run build`
   - Build the App to **out/build/development**: `npm run build:d`
   - Build the App to **out/build/local**: `npm run build:l`
   - Build the App to **out/build/staging**: `npm run build:s`
   - Run Storybook in http://localhost:3001: `npm run sbook`
   - Build Storybook to **out/storybook/development**: `npm run sbook:d`
   - Build Storybook to **out/storybook/local**: `npm run sbook:l`
   - Build Storybook to **out/storybook/production**: `npm run sbook:p`
   - Build Storybook to **out/storybook/qa**: `npm run sbook:q`
   - Build Storybook to **out/storybook/staging**: `npm run sbook:s`

## Creator

**Juan Cuartas** https://twitter.com/juancuartas

## Copyright and license

Code and documentation released under [the MIT license](https://github.com/equisoide/react-mui-ts-steps/blob/master/LICENSE)
