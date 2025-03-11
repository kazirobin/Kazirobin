# User Settings

VS Code provides several different scopes for settings. When you open a workspace, you will see at least the following two scopes: User Settings - Settings that apply globally to any instance of VS Code you open. Workspace Settings - Settings are stored inside your workspace and only apply when the workspace is opened.

---

- JavaScript User Settings JSON
    
    To open the Settings editor, navigate to `File > Preferences > Settings`. You can also open the Settings editor from the Command Palette `(Ctrl+Shift+P)` with Preferences: Open Settings or use the keyboard shortcut `(Ctrl+,)`.
    
    You can also open the user settings.json file just go to the command palette `(Ctrl+Shift+P)` and type `"open setting"` and you are presented with a few options, choose **Open User Settings (JSON)**
    
    ```json
    {
      /*
      JavaScript User Settings JSON
      Version: 1.0.0
      */
    
      //Auto File Save Config Here
      "files.autoSave": "afterDelay",
    
      //Text Editor Config Here
      "editor.fontSize": 17,
      "editor.lineHeight": 1.5,
      "editor.wordWrap": "on",
      "editor.fontLigatures": true,
      "editor.fontFamily": "Operator Mono Lig, Fira Code",
      "editor.accessibilitySupport": "off",
      "editor.renderWhitespace": "all",
      "editor.minimap.enabled": false,
      "workbench.editor.enablePreviewFromQuickOpen": false,
      "editor.pasteAs.preferences": [
        "text.updateImports.jsts",
        "html.updateImports.jsts"
      ],
    
      // Editor String Quick Suggestion Config Here
      "editor.quickSuggestions": {
        "strings": "on"
      },
    
      //Auto Close Tag Config Here
      "auto-close-tag.activationOnLanguage": ["*"],
    
      // Code Formatting Config Here
      "editor.formatOnSave": true,
      "editor.defaultFormatter": "esbenp.prettier-vscode",
      "[prisma]": {
        "editor.defaultFormatter": "Prisma.prisma"
      },
    
      //Terminal Config Here
      "terminal.integrated.fontSize": 13,
      "terminal.integrated.fontFamily": "JetBrainsMono Nerd Font",
      "terminal.integrated.cursorStyle": "line",
      "terminal.integrated.env.windows": {},
      "terminal.integrated.fontLigatures.enabled": true,
      "terminal.integrated.cursorBlinking": true,
    
      // Cursor Config Here
      "editor.hover.delay": 800,
      "editor.cursorWidth": 3,
      "editor.cursorBlinking": "expand",
      "editor.cursorSmoothCaretAnimation": "on",
    
      // Bracket Color Config Here
      "editor.bracketPairColorization.enabled": true,
      "editor.bracketPairColorization.independentColorPoolPerBracketType": true,
      "editor.guides.bracketPairs": true,
    
      //Explorer File Delete Confirm Config Here
      "explorer.confirmDelete": false,
    
      //Opening and Closing Tags Auto Rename Config Here
      "editor.linkedEditing": true,
    
      // Workspace Trust security Config Here
      "security.workspace.trust.untrustedFiles": "open",
    
      // Workspace Whitespace And New Line Config Here
      "files.trimTrailingWhitespace": true,
      "files.insertFinalNewline": true,
      "files.trimFinalNewlines": true,
    
      //Explorer Drag And Drop Config Here
      "explorer.confirmDragAndDrop": true,
    
      // Workspace Color Theme Config Here
      "workbench.colorTheme": "Bearded Theme Black & Diamond",
    
      // Window Zoom Level Config Here
      "window.zoomLevel": 1.3,
    
      // Error Lens Config Here
      "errorLens.enabled": true,
      "errorLens.enabledDiagnosticLevels": ["error", "warning", "info"],
      "errorLens.exclude": ["markdown", "plaintext"],
    
      // Powermode Config Here
      "powermode.enabled": true,
      "powermode.presets": "particles",
      "powermode.shake.enabled": false,
      "powermode.combo.counterEnabled": "hide",
      "powermode.combo.counterSize": 0,
    
      // Workspace Icon Theme Config Here
      "workbench.iconTheme": "material-icon-theme",
      "material-icon-theme.activeIconPack": "react_redux",
    
      // Github Copilot Config Here
      "github.copilot.enable": {
        "*": true,
        "plaintext": false,
        "markdown": true,
        "scminput": false
      },
    
      // Spell Config Here
      "cSpell.language": "en,en-GB,en-US,lorem",
      "cSpell.userWords": [],
    
      // SVG Preview Config Here
      "svg.preview.mode": "svg"
    }
    
    ```
    
- User Keybinding JSON
    
    To open the Keyboard Binding, navigate to `File > Preferences > Keyboard Shortcut`
    
    And you need to open **`keybindings.json`**
    
    ```json
    
    ```
    
- VScode Intellisense Setup
    
    IntelliSense is a general term for various code editing features including: code completion, parameter info, quick info, and member lists. IntelliSense features are sometimes called by other names such as `code completion`, `content assist`, and `code hinting`
    
    For jQuery Project create  **`jsconfig.json` in your project root directory**
    
    ```json
    {
      "typeAcquisition": {
        "include": ["jquery"]
      }
    }
    ```
    
    For React JS Project create **`jsconfig.json` in your project root directory**
    
    ```json
    {
      "include": ["**/*"],
      "exclude": ["node_modules", "**/node_modules", "dist", "build"],
      "compilerOptions": {
        "allowJs": true,
        "target": "es6",
        "module": "esnext",
        "moduleResolution": "node"
      }
    }
    
    ```
    
    For Next JS Project create  **`jsconfig.json` in your project root directory**
    
    ```json
    {
      "include": ["**/*"],
      "exclude": ["node_modules", "**/node_modules", "dist", "build", ".next"],
      "compilerOptions": {
        "paths": {
          "@/*": ["./*"]
        },
        "allowJs": true,
        "target": "es6",
        "module": "esnext",
        "moduleResolution": "node"
      }
    ```