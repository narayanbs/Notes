tmux is a terminal multiplexer. When you open tmux, you get a session associated with a window and a pane.
Each session can have multiple windows and each window can have multiple panes. The session can be named and we can 
detach/re-attach to a session using the name.

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


**navigate between sessions**
To navigate between the sessions we can use `j and k` like in vim and press enter.
use `<Esc>` or `q` to exit

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

```

#### Others

**to enable and disable mouse**
$ :set -g mouse on 
$ :set -g mouse off 

**to copy and paste in Tmux between tmux and host**
`<C-a>[`  to enter into copy mode vim like . select text and then yank using `y`. You can paste from clipboard using `<Ctrl+Shift+V>`
`q` to exit copy mode and return to normal mode.

or

`<Ctrl-Shift+C>` to copy to X clipboard and `<Ctrl+shift+V>` to paste from X clipboard

#### Using Tmux Resurrect  to restore sessions

**tmux-resurrect keyboard shortcuts:**

```bash
<C-a><C-s> for saving sessions
<C-a><C-r> for restoring sessions
```

the sessions are stored in ~/.local/share/tmux/resurrect folder.


