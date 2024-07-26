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
  },
  "vim_mode": true
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
Add the following entries into .zed/settings.json

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
##### C/C++ lsp and formatter settings
Add the following entries into .zed/settings.json
{
  "languages": {
    "C": {
      "enable_language_server": true,
      "use_autoclose": true,
      "extend_comment_on_newline": true,
      "remove_trailing_whitespace_on_save": true,
      "tab_size": 4,
      "indent_size": 4,
      "indent_style": "space",
      "code_actions_on_format": {
        "clangd": true
      },
      "always_treat_brackets_as_autoclosed": true,
      "ensure_final_newline_on_save": true,
      "format_on_save": "on"
    },
  }
}
Additionally you need to generate .clang-format file
$ clang-format -style=llvm -dump-config > .clang-format
