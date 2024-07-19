#### Installing
curl -f https://zed.dev/install.sh | sh

#### Uninstalling Zed
rm -rf ~/.config/zed
rm -rf $HOME/.local/zed.app
rm -rf $HOME/.local/bin/zed
rm -rf $HOME/.local/share/zed
rm -rf $HOME/.local/share/applications/dev.zed.Zed.desktop

#### Global Configuration
vim ~/.config/zed/settings.json

{
  "ui_font_size": 16,
  "buffer_font_size": 13,
  "buffer_font_family": "JetBrainsMono Nerd Font",
  "theme": {
    "mode": "system",
    "light": "One Light",
    "dark": "One Dark"
  }
}

#### Project Configuration
Create a folder .zed in the project root and add the file settings.json inside it. 

##### Virtual environment path for python projects
Add the following to pyproject.toml

[tool.pyright]
venvPath = "."
venv = "myenv"

[tool.isort]
profile = "black"

##### black formatter to python project
Add the following entries into settings.json

{
  "languages": {
    "Python": {
      "formatter": {
        "external": {
          "command": "myenv/bin/black",
          "arguments": ["-"]
        }
      },
      "format_on_save": "on"
    }
  }
}

