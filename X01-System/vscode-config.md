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

##### Vim extension for vscode

```js
ext install vscodevim.vim
```

##### Install Icons

vscode icons -- This is a new one i am using
```js
ext install vscode-icons-team.vscode-icons
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

The extensions are stored in ~/.vscode/extensions

#### User settings
Copy keybindings.json and settings.json from dotfiles/.config/Code/User and paste it into ~/.config/Code/User folder


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

