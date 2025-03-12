# Global Settings

To configure project settings, **select WebStorm | Settings on macOS or File | Settings on Windows and Linux from the main menu**. Alternatively, you can press Ctrl Alt 0S to show the IDE settings. icon. Other settings are global and apply to all existing projects.

---

- Editor & Terminal Font Config
    
    Add WebStorm editor font, navigate to `File > Settings > Editor > Font`
    
    ```
    Font Name - Operator Mono Lig
    Font Size - 18
    Line Height - 1.3
    ```
    
    Add WebStorm terminal font, navigate to `File > Settings > Editor > Color Scheme > Console Font`
    
    ```
    Font Name - JetBrains Mono
    Font Size - 13
    Line Height - 1.3
    ```
    
- Custom WebStorm Properties
    
    To add custom WebStorm properties, navigate to `Menu > Help > Edit Custom Properties`
    
    ```xml
    # Hide the project directory path
    project.tree.structure.show.url=false
    ide.tree.horizontal.default.autoscrolling=false
    ```
    
- Soft Wrap on Editor
    
    To add Soft Wrap, navigate to `File > Settings > Editor > General > **Soft-wrap these files`** make sure to use a semicolon as the separator!
    
    ```
    *.md; *.mdx; *.txt; *.rst; *.adoc; *.svg; *.ts; *.tsx; *.js; *.jsx; *.html; *.cjs; *.cts; *.mjs; *.mts; *.vue; *.astro
    ```
    
- Highlight Match HTML/XML Tag
    
    To add Highlight match tag, navigate to `File > Settings > Editor > General > Appearance` `Enable HTML/XML tag tree Highlighting` and set `Level to highlighting = 1` and `opacity = 0.1` and also disable `Usages of element at caret` from `File > Settings > Editor > Code Edting`
    
    ```xml
    Level to highlighting = 1
    opacity = 0.1
    ```
    
- JSX Attributes
    
    To Add for JSX attributes, navigate to `File > Settings > Editor > Code Style > HTML > Other` and set `Quotes` or `Based on type` for **Add for JSX attributes** field.
    
    ```
    **Add for JSX attributes = Quotes or Based on type**
    ```
    
- User Interface Theme
    
    The interface theme defines the appearance of windows, dialogs, buttons, and all visual elements of the user interface.
    
    To Add a theme, navigate to `File > Settings > Plugins > Marketplace`
    
    ```xml
    Darucla Solid Theme
    ```
    
- Prettier Glob Pattern
    
    Glob pattern use in `webstorm` for config prettier.
    
    ```
    {**/*,*}.{js,ts,jsx,tsx,cjs,cts,mjs,mts,md,mdx,vue,astro,html,json,css,scss}
    ```