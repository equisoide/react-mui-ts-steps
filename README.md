# Creating a React-MUI-TypeScript Template

The purpose of this tutorial is to document the step by step on how to create a [React-MUI-TypeScript Template](https://github.com/equisoide/react-mui-ts-template), so that it will serve as a reference guide for myself and other users.

## 1. Install required libraries
  - [React App with TypeScript template](https://github.com/facebook/create-react-app/tree/main/packages/cra-template-typescript):
    - `npx create-react-app react-mui-ts-template --template typescript`
    - `cd react-mui-ts-template`
  - [MUI (Material UI)](https://mui.com/material-ui/getting-started/installation):
    - `npm i @mui/material @emotion/react @emotion/styled`
    - `npm i @fontsource/roboto`
    - `npm i @mui/icons-material`
  - [react-i18next](https://react.i18next.com/guides/quick-start):
    - `npm i i18next react-i18next`
    - `npm i i18next-browser-languagedetector`
  - [env-cmd](https://github.com/toddbluhm/env-cmd):
    - `npm i env-cmd`
  - [Stylelint](https://stylelint.io/user-guide/get-started):
    - `npm i stylelint stylelint-config-standard`
  - [ESLint](https://eslint.org/docs/user-guide/getting-started):
    - `npm i eslint`
    - `npm init @eslint/config`
      - To check syntax, find problems, and enforce code style
      - JavaScript modules (import/export)
      - React
      - Does your project use TypeScript? › `Yes`
      - Where does your code run? › `Browser`
      - Use a popular style guide › `Airbnb`
      - What format do you want your config file to be in? › `JavaScript`
      - Would you like to install them now? › `Yes`
      - Which package manager do you want to use? › `npm`
  - [Storybook](https://storybook.js.org/docs/react/get-started/install):
    - `npx storybook init`
      - Need to install the following packages: storybook, Ok to proceed? › `y` 
      - Do you want to run the eslintPlugin migration on your project? › `y`

## 2. Install VS Code useful extensions
  - [DotENV](https://marketplace.visualstudio.com/items?itemName=mikestead.dotenv)
  - [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
  - [EditorConfig](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig)
  - [Icons](https://marketplace.visualstudio.com/items?itemName=robertohuertasm.vscode-icons)
  - [MDX](https://marketplace.visualstudio.com/items?itemName=silvenon.mdx)
  - [NpmIntellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.npm-intellisense)
  - [SortLines](https://marketplace.visualstudio.com/items?itemName=Tyriar.sort-lines)
  - [Stylelint](https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint)

## 3. Add [.editorconfig](https://editorconfig.org/)
  - Create `.editorconfig` file at the app's root level
  - Add the following configuration:
    ```
    root = true

    [*]
    charset = utf-8
    end_of_line = lf
    indent_size = 2
    indent_style = space
    insert_final_newline = true
    trim_trailing_whitespace = true
    ```
  - Save twice (the 2nd save is to apply coding style to the `.editorconfig` file)

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
  - Move `devDependencies` after `dependencies`
  - Replace `scripts` section with the following:
    ```json
    "scripts": {
      "build": "env-cmd -f ./.env/.env.production react-scripts build",
      "build:b": "build-storybook -s public",
      "build:d": "env-cmd -f ./.env/.env.development react-scripts build",
      "build:l": "env-cmd -f ./.env/.env.local react-scripts build",
      "build:q": "env-cmd -f ./.env/.env.qa react-scripts build",
      "build:s": "env-cmd -f ./.env/.env.staging react-scripts build",
      "eject": "react-scripts eject",
      "init": "npm ci --loglevel=error --no-audit --no-fund",
      "lint": "eslint --ext .js,.jsx,.ts,.tsx src/",
      "lint:f": "eslint --fix --ext .js,.jsx,.ts,.tsx src/",
      "lint:s": "./node_modules/.bin/stylelint \"src/**/*.css\"",
      "sbook": "start-storybook -p 3001 -s public",
      "start": "env-cmd -f ./.env/.env.local react-scripts start",
      "test": "env-cmd -f ./.env/.env.test react-scripts test --env=jsdom --coverage --watchAll=false"
    },
    ```
  - Remove `eslintConfig` section
  - Add [jest](https://jestjs.io/docs/configuration) section after `scripts`:
    ```json
    "jest": {
      "collectCoverageFrom": [
        "src/**/*.ts",
        "src/**/*.tsx",
        "!src/**/*.stories.tsx",
        "!src/app.tsx",
        "!src/index.tsx",
        "!src/util/report-web-vitals.ts"
      ]
    },
    ```
  - Save

## 5. Configure [tsconfig.json](https://www.typescriptlang.org/tsconfig)
  - Enable [ES6](http://es6-features.org) features:
    > `"target": "es6",`
  - Disable **TypeScript** [incremental](https://www.typescriptlang.org/tsconfig#incremental) compilation (I had experienced cache issues with it):
    > `"incremental": false,`
  - Put **lib** section on a single line:
    > `"lib": ["dom", "dom.iterable", "esnext"],`
  - Sort `compilerOptions` items by selecting all of them and pressing `F9` (SortLines plugin)
  - Remove trailing comma from the last item of `compilerOptions`
  - Save

## 6. Configure [.eslintrc](https://eslint.org/docs/user-guide/configuring/)
  - Rename `.eslintrc.js` to `.eslintrc`
  - Remove `module.exports = ` (The file is now a **JSON** document)
  - Remove semicolon at the end of the file
  - Replace all `single quotes` by `double quotes`
  - Enclose all property names in `double quotes`
  - Add `"jest": true` to the `"env"` object
  - Replace `extends` array with the following:
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
  - Replace `plugins` array with the following:
    ```json
    "plugins": [
      "react",
      "react-hooks",
      "@typescript-eslint"
    ],
    ```
  - Replace `rules` section with the following:
    ```json
    "rules": {
      "@typescript-eslint/no-empty-function": "off",
      "comma-dangle": ["error", "never"],
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
  - Add `settings` section after `rules`:
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
  - Create `.eslintignore` file at the app's root level
  - Add the following configuration:
    ```
    build/
    coverage/
    node_modules/
    storybook-static/
    ```
  - Save

## 8. Add [.stylelintrc](https://stylelint.io/user-guide/configure)
  - Create `.stylelintrc` file at the app's root level
  - Add the following configuration:
    ```json
    {
        "extends": "stylelint-config-standard",
        "rules": {
            "declaration-block-trailing-semicolon": "always",
            "declaration-no-important": true,
            "indentation": 2
        }
    }
    ```
  - Save

## 9. Add [VS Code Settings](https://code.visualstudio.com/docs/getstarted/settings)
  - Create `.vscode` folder at the app's root level
  - Inside `.vscode` folder, create `launch.json` file with the following configuration:
    ```json
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
  - Inside `.vscode` folder, create `settings.json` file with the following configuration:
    ```json
    {
      // Use IntelliSense to learn about possible attributes.
      // Hover to view descriptions of existing attributes.
      // Learn more: https://code.visualstudio.com/docs/getstarted/settings
      "explorer.sortOrder": "type",
      "files.eol": "\n",
      "search.exclude": {
        "**/build": true,
        "**/coverage": true,
        "**/node_modules": true,
        "**/storybook-static": true,
        "package-lock.json": true
      },
      "editor.codeActionsOnSave": {
        "source.fixAll": true
      }
    }
    ```
  - Save

## 10. Configure [.gitignore](https://git-scm.com/docs/gitignore)
   - Remove `.env.local`
   - Remove `.env.development.local`
   - Remove `.env.test.local`
   - Remove `.env.production.local`
   - Add `/storybook-static` after `/build`
   - Add `# log` comment before `npm-debug.log*`
   - Save

## 11. Add [Environment Files](https://create-react-app.dev/docs/adding-custom-environment-variables/#adding-development-environment-variables-in-env)
  - Create `.env` folder at the app's root level
  - Inside `.env` folder, create the following files:
    - `.env.development`
      - Initialize file with `REACT_APP_ENV=development`
    - `.env.local`
      - Initialize file with `REACT_APP_ENV=local`
    - `.env.production`
      - Initialize file with `REACT_APP_ENV=production`
    - `.env.qa`
      - Initialize file with `REACT_APP_ENV=qa`
    - `.env.staging`
      - Initialize file with `REACT_APP_ENV=staging`
    - `.env.test`
      - Initialize file with `REACT_APP_ENV=test`

## 12. Add [LICENSE](https://docs.github.com/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository)
  - Create `LICENSE` file at the app's root level
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
  - Replace `README.md` with the following content:
    ````markdown
    # React, MUI and TypeScript template

    This template is intended to help you start a new `React SPA` project from scratch with a comprehensive folder structure, required dependencies, built-in configurations, example components and good practices for React Web Development. The project was bootstrapped with [Create React App](https://create-react-app.dev). Below you will find some information on how to perform common tasks.

    ## Core Libraries
    - [React 18.1.0](https://reactjs.org) with `React Scripts 5.0.1`
    - [MUI 5.8.2](https://mui.com) with `Emotion` styling engine, `Roboto Fonts` and `Font Icons`
    - [TypeScript 4.7.2](https://www.typescriptlang.org) with [ES6](http://es6-features.org)
    - [I18next 21.8.5](https://react.i18next.com) for internationalization

    ## Documentation Tools
    - [Storybook 6.5.6](https://storybook.js.org) to document pages and components

    ## Code Quality & Performance
    - [ESLint 8.16.0](https://eslint.org) with `Airbnb`, `TypeScript`, `React`, `React Hooks` and `Jest` configuration
    - [Stylelint 14.8.5](https://stylelint.io) to analyse `CSS` files
    - [Jest 27.5.2](https://jestjs.io/docs/getting-started) to test `JavaScript`/`TypeScript` files
    - [React Testing Library 13.3.0](https://testing-library.com/docs/react-testing-library/intro) to test components
    - [Web Vitals 2.1.4](https://web.dev/vitals) to meassure performance

    ## Built-in Settings
    - [.editorconfig](https://editorconfig.org) settings to standardize charset, ending of lines and indentation
    - [.vscode](https://code.visualstudio.com/docs/getstarted/settings) settings with integrated `Chrome Debugger`, faster search results and auto-format on save
    - [Environment files](https://create-react-app.dev/docs/adding-custom-environment-variables) for `local`, `test`, `development`, `qa`, `staging` and `production`

    ## Environment Quick Setup

    1. Install [NodeJs](https://nodejs.org/es/download/)
    2. Install [Git](https://git-scm.com/downloads)
    3. Install [VS Code](https://code.visualstudio.com/download)
    4. Install VS Code useful extensions:
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
    3. Start the application:
       > `npm start`
    4. Start debugging in `VS Code` by pressing `F5` or by clicking on `Run and Debug` > `Green debug icon`
    5. You can now set breakpoints, debug and inspect the React component hierarchies into the [React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)

    ## Available Scripts
    | Command           | Description                                                 | Evironment      |
    | :---              | :---                                                        | :---            |
    | `npm run init`    | Installs all packages for the 1st time (`Clean Install`)    | N/A             |
    | `npm run lint`    | Analyses `JavaSript`/`TypeScript` code for potential errors | N/A             |
    | `npm run lint:f`  | Try to fix `JavaSript`/`TypeScript` errors                  | N/A             |
    | `npm run lint:s`  | Analyses `CSS` files for potential errors                   | N/A             |
    | `npm test`        | Launches the test runner                                    | env.test        |
    | `npm run build`   | Builds the app for `production` to the `build` folder       | env.production  |
    | `npm run build:b` | Builds `Storybook` as a Static Web Application              | N/A             |
    | `npm run build:d` | Builds the app for `development` to the `build` folder      | env.development |
    | `npm run build:l` | Builds the app for `local` to the `build` folder            | env.local       |
    | `npm run build:q` | Builds the app for `qa` to the `build` folder               | env.qa          |
    | `npm run build:s` | Builds the app for `staging` to the `build` folder          | env.staging     |
    | `npm start`       | Runs the app in http://localhost:3000                       | env.local       |
    | `npm run sbook`   | Runs `Storybook` in http://localhost:3001                   | N/A             |

    ## Working guidelines
    - Never delete and re-generate `package-lock.json` file from scratch, it will break the App and Storybook! Let `npm` update that file every time you install a new dependency
    - Create reusable components inside `src/components` folder. Define each component in its own folder with the following structure:
      ```js
        + src/components/MyComponent  // Component name in PascalCase
          - index.stories.tsx         // Storybook documentation
          - index.test.tsx            // Jest testing file
          - index.tsx                 // Component definition
          - styles.css                // Component styles
      ```
    - Prefer [Function Components](https://www.robinwieruch.de/react-function-component/) over `Class components` they offer almost the same: `state` and `lifecycle methods`, with the plus they are more lightway, have a sophisticated `API` and require less code. With the introduction of `React Hooks` it's possible to write your entire application with just functions as `React components`:
        ```js
        import 'styles.css';

        function MyComponent() {
          return (
            <b>{t('hello_world')}</b> // Use i18n for text rendering
          );
        }

        export default MyComponent;   // Prefer default export
        ```
    - Add your own environment variables to the `env/.env.local` file, this file should not be commited
    - Before running or building this application always run linters and unit tests
    - Linter is configured to accept valid ending of lines as `LF` (unix style), if you are on Windows, to avoid Git converting from `LF` to `CRLF`, run the following commands:
      ```shell
      git config --global core.autocrlf false
      git config --global core.eol lf
      ```

    ## Documentation & Training
    - [MUI Crash Course](https://www.youtube.com/watch?v=o1chMISeTC0/)
    - [MUI From zero to hero](https://www.youtube.com/playlist?list=PLDxCaNaYIuUlG5ZqoQzFE27CUOoQvOqnQ)
    - [MUI Components](https://mui.com/material-ui/react-autocomplete/)
    - [MUI Templates](https://mui.com/material-ui/getting-started/templates/)

    ## Creator

    **Juan Cuartas** https://twitter.com/juancuartas

    ## Copyright and license

    Code and documentation released under [the MIT license](https://github.com/equisoide/react-mui-ts-template/blob/master/LICENSE)
    ````
  - Save

## 14. Organize src folder
  - Go to `src` folder and delete the following files:
    - `App.css`
    - `App.test.tsx`
    - `App.tsx`
    - `index.css`
    - `logo.svg`

## 15. Organize src/stories folder
  - Go to `src/stories` folder and delete the following files:
    - *button.css*, *Button.stories.tsx*, *Button.tsx*
    - *header.css*, *Header.stories.tsx*, *Header.tsx*
    - *page.css*, *Page.stories.tsx*, *Page.tsx*
  - Rename `Introduction.stories.mdx` to `introduction.stories.mdx`
  - Open file `introduction.stories.mdx` and replace `stories/Introduction.stories.mdx` by `stories/introduction.stories.mdx`

## 16. Other

  


  - Rename `App.tsx` to `app.tsx`
    ```js
    function App() {
      return (
        <div>Hello World!</div>
      );
    }

    export default App;
    ```
  - Rename `reportWebVitals.ts` to `util/report-web-vitals.ts`
  - Create `styles/site.css`
    ```css
    body {
      margin: 0;
    }
    ```
  
2. Install MUI
  - <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons" />

