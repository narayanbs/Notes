
##### Install Python extension and Black Formatter

Launch VS Code Quick Open (ctrl+p), paste the following and enter

```js
ext install ms-python.python
ext install ms-python.black-formatter
```

##### Install Golang extension

```js
ext install golang.Go
```

##### Install clangd C/C++ extension

```js
ext install llvm-vs-code-extensions.vscode-clangd
```

##### Install Live Server extension

```js
ext install ritwickdey.LiveServer
```

##### Install ES7 React/Redux/GraphQL/React-Native snippets

```js
ext install dsznajder.es7-react-js-snippets
```

##### Install prettier extension

```js
ext install esbenp.prettier-vscode
```

##### Install ESLint extension

```js
ext install dbaeumer.vscode-eslint
```

##### Install Path intellisense extension

```js
ext install christian-kohler.path-intellisense
```

##### Install EditorConfig extension

```js
ext install EditorConfig.EditorConfig
```

##### Install themes

Material theme

```js
ext install Equinusocio.vsc-material-theme
```

Kanagawa

```js
ext install qufiwefefwoyn.kanagawa
```

Gruvbox

```js
ext install jdinhlife.gruvbox
```

Tokyo Night

```js
ext install enkia.tokyo-night
```

Nord Theme

```js
ext install arcticicestudio.nord-visual-studio-code
```

##### Install Icons

Material icon theme -- (ctrl+shift+p --> Material icons: change folder color, change folder theme etc)

```js
ext install PKief.material-icon-theme
```

vscode icons -- This is a new one i am using
```js
ext install vscode-icons-team.vscode-icons
```

The extensions are stored in ~/.vscode/extensions

#### User settings

Open User settings using Ctrl+shift+p - `settings.json (~/.config/Code/User/settings.json)` and enter the following

```js
{
    "workbench.startupEditor": "none",
    "editor.fontFamily": "JetBrainsMono Nerd Font",
    "editor.fontLigatures": true,
    "editor.fontWeight": "500",
    "editor.fontSize": 14,
    "editor.formatOnSave": true,
    "editor.codeActionsOnSave": {
        "source.organizeImports": "always"
    },
    "editor.inlayHints.enabled": "offUnlessPressed",
    "workbench.colorTheme": "Everforest Dark",
    "workbench.iconTheme": "vscode-icons",
    "editor.minimap.enabled": false,
    "emmet.includeLanguages": {
        "javascript": "javascriptreact"
    },
    "gopls": {
        "ui.semanticTokens": true
    },
    "[python]": {
        "editor.defaultFormatter": "ms-python.black-formatter"
    },
    "[html]": {
        "editor.defaultFormatter": "vscode.html-language-features"
    },
    "[javascript][javascriptreact][typescript]": {
        "editor.defaultFormatter": "vscode.typescript-language-features"
    },
    "[json][jsonc]": {
        "editor.defaultFormatter": "vscode.json-language-features"
    },
    "[css][scss][less]": {
        "editor.defaultFormatter": "vscode.css-language-features"
    },
    "explorer.confirmDelete": false,
    "files.exclude": {
        "**/.vscode": true,
        "**/.venv": true,
        "**/db.sqlite3": true,
        "**/node_modules": true
    },
    "breadcrumbs.enabled": false,
    "telemetry.telemetryLevel": "off",
    "liveServer.settings.donotShowInfoMsg": true,
    "vsicons.dontShowNewVersionMessage": true,
}

````

### Duplicate Line keyboard Shortcut

- Go to File/Preferences/Keyboard Shortcuts
- Find Copy Line Down Command and click to the left to edit it
- use shift+alt+/ for the shortcut
- use ctrl+shift+alt+/ for the Copy Line Up shortcut

### Uninstalling and clearing configuration folders
```bash
$ sudo apt remove --purge code
$ sudo rm -r ~/.config/Code
$ sudo rm -r ~/.vscode
```

