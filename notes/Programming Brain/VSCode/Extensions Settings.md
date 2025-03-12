# Extensions Settings

VS Code extensions let you add languages, debuggers, and tools to your installation to support your development workflow. VS Code's rich extensibility model lets extension authors plug directly into the VS Code UI and contribute functionality through the same APIs used by VS Code.

---

- Eslint Global Setup
    
    Initialize Eslint to your app with the following command
    
    ```bash
    npm init @eslint/config
    ```
    
    After that, this configuration starts asking some questions you let us answer together.
    
    ![1_WyYkJi-C-NTM-3Gs6qhHCA.webp](Extensions%20Settings%201b2aeacbb29981d3b6ffcdfc59f724fe/1_WyYkJi-C-NTM-3Gs6qhHCA.webp)
    
    Select `“To check syntax and find problems”`. When you select this option next it will ask for (react use import and exports that is why use Javascript modules (import /export):
    
    ![1__3YgdiOcvT9rN0L8cGbK8w.webp](Extensions%20Settings%201b2aeacbb29981d3b6ffcdfc59f724fe/1__3YgdiOcvT9rN0L8cGbK8w.webp)
    
    The next question is about the framework. We select React because we use React now).
    
    ![1_qgzyREGfyJKdSzcB82m7Jw.webp](Extensions%20Settings%201b2aeacbb29981d3b6ffcdfc59f724fe/1_qgzyREGfyJKdSzcB82m7Jw.webp)
    
    And if you use react with typescript you can choose `“Yes”` and it automatically creates and downloads plugins for linting typescript.
    
    ![1_r1-1PF7g-Tw5ioSlCP0qOg.webp](Extensions%20Settings%201b2aeacbb29981d3b6ffcdfc59f724fe/1_r1-1PF7g-Tw5ioSlCP0qOg.webp)
    
    We run our code in Browser which is why we should select browser.
    
    ![1_FfdnrSl44LIukUCNfQBvuw.webp](Extensions%20Settings%201b2aeacbb29981d3b6ffcdfc59f724fe/1_FfdnrSl44LIukUCNfQBvuw.webp)
    
    And we can choose we want which format for our Eslint file `(eslint.json or esling.js)`. I prefer `JSON`.
    
    ![1_BFmoDE7rv6toQVbrdoCWpg.webp](Extensions%20Settings%201b2aeacbb29981d3b6ffcdfc59f724fe/1_BFmoDE7rv6toQVbrdoCWpg.webp)
    
    The last step Eslint init asks us to download Eslint plugins for now and with which package manager.
    
    ![1_kG9MQRbj3lbPmSGgdrfkBA.webp](Extensions%20Settings%201b2aeacbb29981d3b6ffcdfc59f724fe/1_kG9MQRbj3lbPmSGgdrfkBA.webp)
    
    ![1_iZ3v5mwwtKUIRaQw6JIATQ.webp](Extensions%20Settings%201b2aeacbb29981d3b6ffcdfc59f724fe/1_iZ3v5mwwtKUIRaQw6JIATQ.webp)
    
    After downloading the packages `Eslint` configuration is ready for our template and we have a new file.
    
    ![1_GeRoYpoW_qVVL4FRrYQZlA.webp](Extensions%20Settings%201b2aeacbb29981d3b6ffcdfc59f724fe/1_GeRoYpoW_qVVL4FRrYQZlA.webp)
    
    ### Let us add prettier for out template with Eslint.
    
    You can use these two options depending on your package manager.
    
    ```bash
    npm install --save-dev prettier eslint-config-prettier
    ```
    
    After installing go to the `.eslintrc.JSON` file and inside `“extends”` add the `“prettier”` plugin.
    
    ![1_FRq97rSmnWA_o58iXSnljA.webp](Extensions%20Settings%201b2aeacbb29981d3b6ffcdfc59f724fe/1_FRq97rSmnWA_o58iXSnljA.webp)
    
- Prettier Global Setup
    
    First, install Prettier locally in your project as `devDependencies`
    
    ```bash
    npm install --save-dev prettier
    ```
    
    Create a `.prettierrc` file and place it in the root of your project.
    
    ```json
    {
      "semi": true,
      "tabWidth": 2,
      "printWidth": 80,
      "trailingComma": "none",
      "bracketSpacing": true,
      "jsxBracketSameLine": false
    }
    ```
    
    Add this following line to `package.json` for check format and fix the issue
    
    ```json
    "scripts": {
    	 "format:check": "prettier . --check",
    	 "format:fix": "prettier . --write",
    }
    ```
    
    Open the user settings JSON file by entering the keyboard shortcut `CMD + Shift + P` on Mac or `Ctrl + Shift + P` on Windows, then type in user settings, and select `Preferences: Open User Settings (JSON)`
    
    Then add the following lines to the `settings.json` file and save it.
    
    ```json
    {
      "editor.formatOnSave": true,
      "editor.defaultFormatter": "esbenp.prettier-vscode"
    }
    ```
    
- Prettier Config Options
    
    This configuration sets up Prettier to enforce consistent and readable code formatting, especially for JavaScript, TypeScript, and JSX.
    
    - **`printWidth`**
        - Specifies the maximum line length before wrapping.
        - Default: `80` (characters per line).
        
    - **`tabWidth`**
        - Defines the number of spaces per indentation level.
        - Default: `2`.
        
    - **`useTabs`**
        - Determines whether to use tabs for indentation.
        - `false`: Uses spaces instead of tabs.
        - `true`: Uses tabs.
        
    - **`semi`**
        - Controls whether semicolons (`;`) are added at the end of statements.
        - `true`: Adds semicolons.
        - `false`: Omits semicolons.
        
    - **`singleQuote`**
        - Specifies whether to use single (`'`) or double (`"`) quotes.
        - `false`: Uses double quotes (`"`).
        - `true`: Uses single quotes (`'`).
        
    - **`quoteProps`**
        - Controls when to quote object property names.
        - `"as-needed"`: Only adds quotes when necessary.
        - `"consistent"`: Quotes all properties if one requires quotes.
        - `"preserve"`: Keeps quotes as written in the original code.
        
    - **`jsxSingleQuote`**
        - Determines whether to use single quotes in JSX.
        - `false`: Uses double quotes (`"`).
        - `true`: Uses single quotes (`'`).
        
    - **`trailingComma`**
        - Specifies whether to add trailing commas in objects, arrays, functions, etc.
        - `"none"`: No trailing commas.
        - `"es5"`: Adds trailing commas where valid in ES5 (objects, arrays).
        - `"all"`: Adds trailing commas everywhere, including function parameters.
        
    - **`bracketSpacing`**
        - Controls spacing inside `{}` for objects.
        - `true`: `{ key: value }` (adds spaces).
        - `false`: `{key:value}` (no spaces).
        
    - **`arrowParens`**
        - Determines whether to include parentheses for single-argument arrow functions.
        - `"avoid"`: Omits parentheses when possible (`x => x`).
        - `"always"`: Always includes parentheses (`(x) => x`).
        
    - **`requirePragma`**
        - Controls whether Prettier should only format files with a special comment (`@prettier` or `@format`).
        - `false`: Formats all files.
        - `true`: Formats only files with the pragma comment.
        
    - **`insertPragma`**
        - Determines whether Prettier should insert a special `@prettier` pragma comment at the top of formatted files.
        - `false`: Does not insert the pragma.
        - `true`: Inserts the pragma.
        
    - **`proseWrap`**
        - Controls how Prettier wraps markdown text.
        - `"always"`: Wraps text at `printWidth`.
        - `"never"`: Does not wrap text.
        - `"preserve"`: Keeps the original formatting.
        
    - **`htmlWhitespaceSensitivity`**
        - Defines how Prettier treats whitespace in HTML.
        - `"css"`: Follows CSS display rules.
        - `"strict"`: Preserves all spaces.
        - `"ignore"`: Ignores whitespace completely.
    
    - `endOfLine`
        - Specifies line ending style.
        - `"lf"` → Unix/Linux (default)
        - `"crlf"` → Windows
        - `"cr"` → Classic Mac
        - `"auto"` → Based on existing file
    
    Complete Example Configuration (`.prettierrc`)
    
    ```json
    {
      "printWidth": 80,
      "tabWidth": 2,
      "useTabs": false,
      "semi": true,
      "singleQuote": false,
      "quoteProps": "as-needed",
      "jsxSingleQuote": false,
      "trailingComma": "none",
      "bracketSpacing": true,
      "arrowParens": "avoid",
      "requirePragma": false,
      "insertPragma": false,
      "proseWrap": "preserve",
      "htmlWhitespaceSensitivity": "css",
      "endOfLine": "lf"
    }
    ```
    
- Eslint Setup on TypeScript Project
    
    **First, install the following dependencies to your `devDependencies`**
    
    ```bash
    npm install --save-dev eslint @eslint/js typescript typescript-eslint
    ```
    
    Next, create an `eslint.config.mjs` config file in the root of your project, and populate it with the following
    
    ```jsx
    import eslint from "@eslint/js";
    import tseslint from "typescript-eslint";
    
    export default tseslint.config({
      languageOptions: {
        parserOptions: {
          project: true,
          tsconfigRootDir: import.meta.dirname,
        },
      },
      extends: [eslint.configs.recommended, ...tseslint.configs.recommended],
      rules: {
        "no-console": "warn",
      },
    });
    ```
    
    Add this following line to `package.json` for check lint and fix the issue
    
    ```json
    "scripts": {
    	  "lint": "eslint",
        "lint:fix": "eslint --fix",
    }
    ```
    
    Integrating `Prettier` with `eslint` Run the following command in the terminal
    
    ```bash
    npm install --save-dev prettier eslint-config-prettier eslint-plugin-prettier
    ```
    
    Then update the `eslint.config.mjs`
    
    ```jsx
    import eslint from '@eslint/js';
    import eslintConfigPrettier from 'eslint-config-prettier';
    import eslintPluginPrettier from 'eslint-plugin-prettier';
    import tseslint from 'typescript-eslint';
    
    export default tseslint.config({
      languageOptions: {
        parserOptions: {
          project: true,
          tsconfigRootDir: import.meta.dirname
        }
      },
      plugins: {
        prettier: eslintPluginPrettier
      },
      extends: [
        eslint.configs.recommended,
        ...tseslint.configs.recommended,
        eslintConfigPrettier
      ],
      rules: {
    	  "no-console": "warn",
        'prettier/prettier': ['error', { endOfLine: 'auto' }]
      }
    });
    ```
    
- Eslint Setup on JavaScript Project
    
    **First, install the following dependencies to your `devDependencies`**
    
    ```bash
    npm install --save-dev eslint @eslint/js
    ```
    
    Next, create an `eslint.config.mjs` config file in the root of your project, and populate it with the following
    
    ```jsx
    import globals from "globals";
    import pluginJs from "@eslint/js";
    
    /** @type {import('eslint').Linter.Config[]} */
    export default [
      { languageOptions: { globals: globals.browser } },
      pluginJs.configs.recommended,
      { rules: { "no-console": "warn" } },
    ];
    ```
    
    Add this following line to `package.json` for check lint and fix the issue
    
    ```json
    "scripts": {
    	  "lint": "eslint",
        "lint:fix": "eslint --fix",
    }
    ```
    
    Integrating Prettier with eslint Run the following command in the terminal
    
    ```bash
    npm install --save-dev prettier eslint-config-prettier eslint-plugin-prettier
    ```
    
    Then update the `eslint.config.mjs`
    
    ```jsx
    import globals from 'globals';
    import pluginJs from '@eslint/js';
    import eslintConfigPrettier from 'eslint-config-prettier';
    import eslintPluginPrettier from 'eslint-plugin-prettier';
    
    /** @type {import('eslint').Linter.Config[]} */
    export default [
      {
        languageOptions: {
          globals: globals.browser
        }
      },
      pluginJs.configs.recommended,
      eslintConfigPrettier,
      {
        plugins: {
          prettier: eslintPluginPrettier
        },
        rules: {
          'no-console': 'warn',
          'prettier/prettier': 'error'
        }
      }
    ];
    ```
    
- Eslint Setup on NextJS  Project
    
    To get started with ESLint in a Next.js project, we first need to install the necessary dependencies.
    
    ```bash
    npm install eslint eslint-config-next --save-dev
    ```
    
    Create a `.eslintrc.json` file and place it in the root of your project.
    
    ```json
    {
      "env": {
        "browser": true,
        "es6": true
      },
      "extends": ["next/core-web-vitals", "next/typescript", "eslint:recommended", "next"]
    }
    ```
    
    Integrating `Prettier` with `eslint` Run the following command in the terminal:
    
    ```bash
    npm install --save-dev prettier eslint-config-prettier eslint-plugin-prettier
    ```
    
    And update `.eslintrc.json`
    
    ```json
    {
    	"extends": [
    		"prettier",
        "plugin:prettier/recommended"
      ]
      "plugins": [
        "prettier"
      ],
      "rules": {
        "prettier/prettier": ["error", { "endOfLine": "auto" }]
      }
    }
    ```
    
    Integrating `TailwindCSS ClassName` Checking with `eslint` Run the following command in the terminal:
    
    ```bash
    npm install --save-dev eslint-config-standard eslint-plugin-tailwindcss
    ```
    
    And update `.eslintrc.json`
    
    ```json
    {
      "extends": ["standard", "plugin:tailwindcss/recommended"]
    }
    ```
    
    Add this following line to `package.json` to check lint and fix the issue
    
    ```json
    "scripts": {
    	  "lint": "next lint",
        "lint:fix": "next lint --fix"
    }
    ```
    
- Console Ninja Setup
    
    Console Ninja is a VS Code extension that displays `console.log` output and **runtime errors** directly in your editor from your running browser or node application. It's like your browser dev tools console tab or terminal output from your node app, but instead of having to context switch, values are connected to your code and displayed ergonomically in your editor.
    
    ```json
    // Console Ninja Config Here
      "console-ninja.toolsToEnableSupportAutomaticallyFor": {
        "live-server-extension": true,
        "live-preview-extension": true
      },
      "console-ninja.allowedHosts": ["127.0.0.1", "localhost"],
      "console-ninja.featureSet": "Community",
    ```
    
- Power Mode Extension Setup
    
    Your code is powerful, unleash it! The extension made popular by Code in the Dark has finally made its way to VS Code.
    
    ```json
      // Powermode Config Here
      "powermode.enabled": true,
      "powermode.presets": "particles",
      "powermode.shake.enabled": false,
      "powermode.combo.counterEnabled": "hide",
      "powermode.combo.counterSize": 0,
    ```
    
- Live Sass Compiler Extension Setup
    
    Inside your Project Create a `.vscode` directory. In the `.vscode` folder create a json file named `settings.json`. Inside of the `settings.json`, type the following json code.
    
    ```jsx
    {
      // Live Sass Compiler Config Here
      "liveSassCompile.settings.formats": [
        {
          "format": "expanded",
          "extensionName": ".css",
          "savePath": "/css"
        },
        {
          "format": "compressed",
          "extensionName": ".min.css",
          "savePath": "/css"
        }
      ],
      "liveSassCompile.settings.generateMap": true
    }
    ```
    
- TailwindCSS IntelliSense Extension Setup
    
    An alternative to VS Code's built-in CSS language mode which maintains full CSS IntelliSense support even when using Tailwind-specific at-rules. Syntax definitions are also provided so that Tailwind-specific syntax is highlighted correctly in all CSS contexts.
    
    Inside your Project Create a `.vscode` directory. In the `.vscode` folder create a json file named `settings.json`. Inside of the `settings.json`, type the following json code.
    
    ```json
    // TailwindCSS Config Here
      "css.validate": false,
      "tailwindCSS.emmetCompletions": true,
      "files.associations": {
      "*.css": "tailwindcss"
    }
    ```
    
    ### Automatic Class Sorting with Prettier
    
    This plugin scans your templates for class attributes containing Tailwind CSS classes, and then sorts those classes automatically following our **recommended class order**.
    
    To get started, install **`prettier-plugin-tailwindcss`** as a dev-dependency:
    
    ```bash
    npm install -D prettier-plugin-tailwindcss prettier
    ```
    
    Then add the plugin to your `.prettierrc` configuration file.
    
    ```json
    {
      "plugins": ["prettier-plugin-tailwindcss"]
    }
    ```
    
    ### TailwindCSS Class Error Eslint Setup
    
    First, install Eslint Config and Tailwindcss locally in your project as `devDependencies`
    
    ```bash
    npm install --save-dev eslint eslint-config-standard eslint-plugin-tailwindcss
    ```
    
    ### For `.eslintrc.json` / `.eslintrc`
    
    Create a `.eslintrc.json` file and place it in the root of your project.
    
    ```json
    {
      "extends": ["standard", "plugin:tailwindcss/recommended"]
    }
    ```
    
    ### For `eslint.config.js`
    
    Create an `eslint.config.js` file and place it in the root of your project.
    
    ```jsx
    import tailwind from "eslint-plugin-tailwindcss";
    
    export default [
    	...tailwind.configs["flat/recommended"],
    	
    	// ... Other code here
    ]
    ```
    
    ### For `eslint.config.js` TypeScript Project
    
    Create an `eslint.config.js` file and place it in the root of your project.
    
    ```jsx
    import tseslint from "typescript-eslint";
    import js from "@eslint/js";
    import tailwind from "eslint-plugin-tailwindcss";
    
    export default tseslint.config(
      ...tailwind.configs["flat/recommended"],
      {
        extends: [
          js.configs.recommended,
          ...tseslint.configs.recommended,
        ],
        files: ["**/*.{ts,tsx}"]
      }
      
      // ... Other code here
    );
    
    ```
    
- Error Lens Extension Setup
    
    Improve highlighting of errors, warnings and other language diagnostics.
    
    ```json
      // Error Lens Config Here
      "errorLens.enabled": true,
      "errorLens.enabledDiagnosticLevels": ["error", "warning", "info"],
      "errorLens.exclude": ["markdown", "plaintext"]
    ```
    
- Code Runner Extension Setup
    
    Run code file of current active Text Editor
    
    ```json
      // Code Runner Config Here
      "code-runner.clearPreviousOutput": true,
      "code-runner.runInTerminal": true,
    ```