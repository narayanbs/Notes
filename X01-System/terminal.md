
* Install alacritty with tmux or kitty or ghostty or wezterm terminal 

##### Alacritty with tmux

* Install alacritty terminal. 
~~~bash
  $ sudo add-apt-repository ppa:aslatter/ppa -y
  $ sudo apt install alacritty
  $ cp -r dotfiles/.config/alacritty ~/.config
  $ sudo update-alternatives --config x-terminal-emulator  (and choose alacritty in the options)
~~~
* Install tmux. (After installation launch tmux and press `<C-a>I` to install the plugins)
~~~bash
  $ sudo apt install tmux -y
  # Install the plugin manager
  $ git clone https://github.com/tmux-plugins/tpm ~/.config/tmux/plugins/tpm
  $ cp -r dotfiles/.config/tmux ~/.config
~~~

##### Kitty
* Install kitty terminal
~~~bash
  $ curl -L https://sw.kovidgoyal.net/kitty/installer.sh | sh /dev/stdin
~~~
or 

* Download releases from https://github.com/kovidgoyal/kitty/releases/
* Extract and install
~~~bash
  $ mkdir ~/.local/kitty.app && cd ~/.local/kitty.app/
  $ curl -SLO https://github.com/kovidgoyal/kitty/releases/download/v0.39.0/kitty-0.39.0-x86_64.txz
  $ tar -xvf kitty-0.39.0-x86_64.txz
~~~
* Make kitty the default terminal
~~~bash
  $ sudo update-alternatives --install /usr/bin/x-terminal-emulator x-terminal-emulator /home/narayan/.local/kitty.app/bin/kitty 100
  # Confirm terminal config
  $ sudo update-alternatives --list x-terminal-emulator 
~~~


#### Ghostty
* Install ghostty terminal
* Download ghostty deb package
~~~bash
  $ https://github.com/mkasberg/ghostty-ubuntu/releases
~~~
* Install it
~~~bash
  $ sudo dpkg -i ghostty_1.0.1-0.ppa4_amd64_22.04.deb
~~~

#### Wezterm

* Install wezterm terminal.
~~~bash
  $ curl -fsSL https://apt.fury.io/wez/gpg.key | sudo gpg --yes --dearmor -o /usr/share/keyrings/wezterm-fury.gpg
  $ echo 'deb [signed-by=/usr/share/keyrings/wezterm-fury.gpg] https://apt.fury.io/wez/ * *' | sudo tee /etc/apt/sources.list.d/wezterm.list
  $ sudo apt update
  $ sudo apt install wezterm
  $ cp -r dotfiles/.config/wezterm ~/.config
  $ sudo update-alternatives --config x-terminal-emulator  (and choose wezterm in the options)
~~~


