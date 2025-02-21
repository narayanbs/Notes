#### Software

* Install build-essential `sudo apt install build-essential -y`
* Install git and configure it 
~~~bash
  $ sudo apt install git -y 
  
  $ git config -l
  $ git config --global user.name "Narayan"
  $ git config --global user.email "narayanbala@gmail.com"
  $ git config --global credential.helper cache
  $ git config --global color.ui auto
  $ git config --global init.defaultBranch main
~~~

* Checkout dotfiles repository from github
~~~bash
  $ git clone https://github.com/narayanbs/dotfiles
~~~

* Checkout Notes repository from github
~~~bash
  $ git clone https://github.com/narayanbs/Notes
~~~

* Install Fira Code Nerd Font and JetBrainsMono Nerd Font
~~~bash
  $ cp Notes/Nerd_Fonts/*.ttf ~/.local/share/fonts
  $ fc-cache -f -v
~~~
and reboot
**Optional**
* Install Fira Code font -- `sudo apt install fonts-firacode`

* For gedit, goto preferences/Fonts & Colors, Choose Fira Code Nerd Font 11 Medium
* Choose the theme gnome-text-editor-themes/catpuccin-frappe.xml by clicking the + button
* For gnome-text-editor `sudo cp gnome-text-editor-themes/catpuccin-frappe.xml /usr/share/gnome-text-editor/styles`

* Install curl, tree, htop `sudo apt install htop curl tree` -y
* Install neovim and add an alias in .bashrc (alias vim='nvim --clean')
~~~bash
  # visit https://github.com/neovim/neovim/releases
  # Download stable nvim-linux64.tar.gz and copy it into Devide
  $ mkdir ~/Devide && cp ~/Downloads/nvim-linux64.tar.gz
  $ tar -xzf nvim-linux64.tar.gz
  # Add bin folder to .bashrc
  export PATH=$PATH:~/Devide/nvim-linux64/bin
  $ source .bashrc

  # If you get an error about lack of fuse library, install it
  $ sudo apt install libfuse.so.2
~~~

* Install hugo (go to https://github.com/gohugoio/hugo/releases and download the appropriate version) and copy blogs folder
* Install and Configure [AC600 Nano Wifi Adapter](./tplinkadapter.md). 
* If you find two versions of gcc, then follow the fix in [Issues and fixes](./issues&fixes.md). 

* Install [terminal and tmux](./terminal.md)

* Install starship cross-shell prompt
~~~bash
  $ sh -c "$(curl -fsSL https://starship.rs/install.sh)"
  $ cp dotfiles/.config/starship.toml ~/.config
  # Add the following to the end of .bashrc
  $ eval "$(starship init bash)"
~~~

* Install Chrome
* Install extensions - ublock origin,privacy badger, save page WE, Print Edit WE, one-tab, bitwarden, debug css
 go to auto-fill in chrome settings and disable "offer to save passwords" and "auto-signing"

#### Languages

* Install [clang+llvm](./clang-llvm.md)
* Install [sdkman](./sdkman-java.md) and install java
* Install rust
~~~bash
  $ curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
  $ source $HOME/.cargo/env
  $ rustc --version
~~~

* Install golang
~~~bash
  $ rm -rf /usr/local/go
  $ sudo tar -C /usr/local -xzf go1.21.6.linux-amd64.tar.gz
  $ export PATH=$PATH:/usr/local/go/bin   # (in .bashrc)
  $ go version
~~~

* Install [python](./Python.md)
* Install [node](./node-npm.md)

* Install zig
* Download the zig binary from https://ziglang.org/download/
* Extract it to $HOME/lang
~~~bash
  $ curl -SLO https://ziglang.org/builds/zig-linux-x86_64-0.14.0-dev.3271+bd237bced.tar.xz
  $ tar -xvf zig-linux-x86_64-0.14.0-dev.3271+bd237bced.tar.xz -C ~/lang
  $ export PATH=$PATH:$HOME/zig # (in .bashrc)
~~~

#### Editors

* Install Lazyvim and configure it [neovim](./neovim-config.md)
* Install and configure [vscode](./vscode-config.md)
* Install and configure [zed](./zed-config.md)
* Install intellij

#### Others

* Install stylua (`cargo install stylua --features lua53`)
* Install ripgrep (`sudo apt install ripgrep`)
* Install fd-find (`sudo apt install fd-find and alias fd='fdfind' in .bashrc`)
* Install yt-dlp
~~~bash
  $ sudo curl -L https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -o /usr/local/bin/yt-dlp
  $ sudo chmod a+rx /usr/local/bin/yt-dlp
~~~

* Install Obsidian (Read how to add obsidian to favorites in [issues&fixes](./issues&fixes.md) )
* Install mpv player and copy configuration scripts. ([mpv Keybindings](../X04-Resources/mpv_player.md))
~~~bash
  $ sudo apt install mpv -y
  $ cp -r ~/dotfiles/.config/mpv/scripts ~/.config/mpv
~~~
* install audacious (`sudo apt install audacious`)
* Install Foliate e-book reader (`sudo snap install foliate`)
* Install Zoxide (curl -sSfL https://raw.githubusercontent.com/ajeetdsouza/zoxide/main/install.sh | sh)
* Install fzf (Download gz from https://github.com/junegunn/fzf/releases)
