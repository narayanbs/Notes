tmux is a terminal multiplexer.
By default, tmux looks for a configuration file in any of the following locations
* $XDG_CONFIG_HOME/tmux/tmux.conf
* ~/.config/tmux/tmux.conf
* /etc/tmux.conf

Tmux configuration can be divided into three main categories.
* server/session options
* user options
* window and pane options

The options can be set using the set command
ex:
        set-option ... or set ...

The command uses zero or more set of flags and arguments
-s is used to apply session options for ex: set-option -s or set -s
-w i used to apply window options  ex: set-option -w or set -w
-g sets a global option for all sessions and windows. ex: set-option -g or set -g
-a appends the value to existing options ex: set-option -a or set -a

Tmux is modal and has different operating modes like command mode, copy mode, view mode etc.

#### Installation & Configuration

```bash
$ sudo apt install tmux
```

Install the plugin manager by cloning the github repo as shown below.
```bash
$ git clone https://github.com/tmux-plugins/tmp ~/.config/tmux/plugins/tpm
``` 

create a folder `~/.config/tmux` and copy `tmux.conf` from https://github.com/narayanbs/dotfiles

Now finish the configuration 
```bash
$ tmux
$ <C-a>I to install the plugins (ctrl-a and caps I)
```

Note: press `<C-a>I` to install the plugins, and  press `<C-a>r` to reload the config.

#### Sessions

tmux uses a default prefix `<C-b>` for commands. We have changed this to `<C-a>`, by editing ``~/.tmux.conf`

**create session**
```bash
$ tmux
$ tmux new
$ tmux new-session
	or
$ :new
```
All of the above create a new session, with default names. 
To create a session with a particular name, we can use
```bash
$ tmux new -s <session-name>
```

**renaming an existing session**
```bash
$ tmux rename-session [-t session-name] [new-session-name]
```
Note: if `[-t session-name]` is not provided the last session used will be renamed.

**attach to existing session**
```bash
$ tmux attach -t [session-name]
```

**detach from session**
```bash
$ tmux detach
	or
$ <C-a>d
```

This would return you to the local terminal from tmux session. Everything would still be running in the background.

**exiting from a session** 
```bash
$ exit
```
Note: all information will be lost).

**kill  all sessions**
```bash
$ tmux kill-server
```

**kill specific session**
```bash
$ tmux kill-session -t [session-name]
```

**view session**
```bash
$ tmux ls 
$ tmux list-sessions 
```

If we are inside tmux terminal we can use
```bash
$ <C-a>s 
```

#### Window Management

**create and close window**
```bash
$ <C-a>c   to create window
$ <C-a>&   to kill the current window
```

**rename a window**
```bash
$ <C-a>, 
```

Each window (regardless of name) has a window id of 0,1,2...

**select window**
To select a window use `<C-a>id`  for ex: `<C-a>2` for the 2nd window

**moving b/w windows**
We can use `<C-a>n` and `<C-a>p` to move to the next and previous windows respectively

**to see all our windows**
To see all your windows press `<C-a>w`

##### Panes

```bash

<C-a>|    to split panes vertically
<C-a>-    to split panes horizontally
<C-a>x    to close the current pane

<C-a>m    toggle maximization

<C-a>{  and <C-a>}   to switch pane position

<C-j>, <C-k>, <C-h>, <C-l>  to navigate b/w panes

<C-a>q    to view the pane numbers
```

Copy - Mode
------------
<C-a>[ to swith to copy mode
v to make selection (j or k to move or down)
y to yank selection
<C-a>] to paste the selection
q to quit copy mode 

Tricks
--------
suppose we have 3 windows (0, 1, 2) and we wish to merge the second window into the first
as two panes (side by side).

1. Enter command mode  C-a :
2. Merge the windows join-pane -s 2 -t 1
3. Move the pane at the bottom to the side C-a Alt-1


