##### Vim extension for vscode

ext install vscodevim.vim

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

##### Install themes
One dark Theme 
```js
ext install mskelton.one-dark-theme
```
##### Install Icons

vscode icons -- This is a new one i am using
```js
ext install vscode-icons-team.vscode-icons
```

The extensions are stored in ~/.vscode/extensions

#### User settings
Copy keybindings.json and settings.json from dotfiles/.config/Code/User and paste it into ~/.config/Code/User folder

#### Just for reference
Open User settings using Ctrl+shift+p - `settings.json (~/.config/Code/User/settings.json)` and enter the following

```js
{
    "workbench.startupEditor": "none",
    "editor.fontFamily": "Cascadia Code NF",
    "editor.fontLigatures": false,
    "editor.fontWeight": "400",
    "editor.fontSize": 15,
    "editor.formatOnSave": true,
    "editor.codeActionsOnSave": {
        "source.organizeImports": "always"
    },
    "editor.inlayHints.enabled": "offUnlessPressed",
    "workbench.colorTheme": "Gruvbox Material Dark",
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

