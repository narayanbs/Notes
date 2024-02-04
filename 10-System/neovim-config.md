

Clone github repository

```bash
$ git clone https://github.com/narayanbs/dotfiles
```

I am currently using LazyVim  setup 

```bash
# required
rm -rf ~/.config/nvim
rm ~/.local/share/nvim
rm  ~/.local/state/nvim
rm ~/.cache/nvim

# clone the starter
git clone https://github.com/LazyVim/starter ~/.config/nvim

# remove the .git folder 
rm -rf ~/.config/nvim/.git
```

Place my configuration inside ~/.config

```bash
$ cp -r dotfiles/.config/nvim/lua ~/.config/nvim
```

In case of any error, remove the following folders and try the above steps again

```bash
$ rm -r ~/.config/nvim/
$ sudo rm -r ~/.local/share/nvim
$ sudo rm -r ~/.local/state/nvim
$ sudo rm -r ~/.cache/nvim
```

