# Workspace Settings

VS Code provides several different scopes for settings. When you open a workspace, you will see at least the following two scopes: User Settings - Settings that apply globally to any instance of VS Code you open. Workspace Settings - Settings are stored inside your workspace and only apply when the workspace is opened.

---

- JavaScript Workspace Settings JSON
    
    Typically, a VS Code `“workspace”` is just your project root folder. You don’t have to do anything for a folder to become a VS Code workspace other than open the folder with VS Code.
    
    You can modify settings for the project and they are stored locally in `<<project folder>>/.vscode/settings.json`
    
    1. Use this `settings.json` if control formatting with `Eslint Formatter`.
    
    ```json
    {
      // Code Formating Config Here
      "eslint.format.enable": true,
      "editor.defaultFormatter": "dbaeumer.vscode-eslint",
      "[javascript]": {
        "editor.defaultFormatter": "dbaeumer.vscode-eslint"
      },
      "[javascriptreact]": {
        "editor.defaultFormatter": "dbaeumer.vscode-eslint"
      },
      "[typescript]": {
        "editor.defaultFormatter": "dbaeumer.vscode-eslint"
      },
      "[typescriptreact]": {
        "editor.defaultFormatter": "dbaeumer.vscode-eslint"
      },
    
      // VSCode Default Validation Config Here
      "typescript.validate.enable": false,
      "javascript.validate.enable": false,
    
      // Auto Close Tag Config Here
      "javascript.autoClosingTags": false,
      "typescript.autoClosingTags": false,
    
      // Code Action On Save Config Here
      "editor.codeActionsOnSave": {
        "source.fixAll.eslint": "explicit",
        "source.fixAll.tslint": "explicit",
        "source.organizeImports": "explicit"
      },
    
      // Eslint Validation Config Here
      "eslint.validate": [
        "javascript",
        "javascriptreact",
        "typescript",
        "typescriptreact"
      ],
    
      // Eslint Emmet Config Here
      "emmet.triggerExpansionOnTab": true,
      
      // VSCode Emmet Including Language Config Here
      "emmet.includeLanguages": {
        "javascript": "javascriptreact",
        "typescript": "typescriptreact"
      }
    }
    ```
    
    1. Use this `settings.json` if control formatting with `Prettier Formatter`.
    
    ```json
    {
      // Code Formating Config Here
      "[javascript]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
      },
      "[javascriptreact]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
      },
      "[typescript]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
      },
      "[typescriptreact]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
      },
    
      // VSCode Default Validation Config Here
      "typescript.validate.enable": false,
      "javascript.validate.enable": false,
    
      // Auto Close Tag Config Here
      "javascript.autoClosingTags": false,
      "typescript.autoClosingTags": false,
    
      // Code Action On Save Config Here
      "editor.codeActionsOnSave": {
        "source.fixAll.eslint": "explicit",
        "source.fixAll.tslint": "explicit",
        "source.organizeImports": "explicit"
      },
      
      // VSCode Emmet Including Language Config Here
      "emmet.includeLanguages": {
        "javascript": "javascriptreact",
        "typescript": "typescriptreact"
      }
    }
    ```