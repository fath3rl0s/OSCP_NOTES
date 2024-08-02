
**Pimp My Kali:**
https://github.com/Dewalt-arch/pimpmykali

**TMUX:**
terminal multi-plexer
https://github.com/tmux/tmux/wiki/Getting-Started
- Create `.tmux.conf`

```
# Set prefix to Ctrl-a
set -g prefix C-a
bind C-a send-prefix
unbind C-b

# Set history limit and disable automatic renaming of windows
set -g history-limit 100000
set -g allow-rename off

# Plugins and status bar settings
set -g @plugin 'tmux-plugins/tmux-logging'
set -g status-bg colour27
set -g status-fg white

# Bind keys for joining and sending panes
bind-key j command-prompt -p "Join pane from:" "join-pane -s '%%'"
bind-key s command-prompt -p "Send pane to:" "join-pane -t '%%'"

# Enable vi mode
set-window-option -g mode-keys vi

# Run tmux logging plugin
run-shell /opt/tmux-logging/logging.tmux

# Mouse support
set -g mouse on

# Use system clipboard
# Install xclip first: sudo apt-get install xclip
set-option -g set-clipboard on

# Bindings for copying to system clipboard
bind-key -T copy-mode MouseDragEnd1Pane send-keys -X copy-pipe-and-cancel 'xclip -in -selection clipboard'
bind-key -T copy-mode-vi MouseDragEnd1Pane send-keys -X copy-pipe-no-clear 'xclip -in -selection clipboard'
bind-key -T copy-mode-vi y send-keys -X copy-pipe-and-cancel 'xclip -in -selection clipboard'

# Optional: bind key for copying entire buffer to system clipboard
bind C-c run "tmux save-buffer - | xclip -i -selection clipboard"


```

![[Pasted image 20240619162858.png]]

- Enter new session
`tmux new -s Test`
`tmux source-file ~/.tmux.conf`

![[Pasted image 20240619164006.png]]

Press
`Ctrl + a`
Followed by `i` to commit changes

***
**LOGGING**

Enter new Tmux Session:
![[Pasted image 20240619170252.png]]

To start Logging:
`Ctrl + a`
`Shift + p`

![[Pasted image 20240619170347.png]]

Run some commands and view the logs!

![[Pasted image 20240619170728.png]]

***
**TMUX Commands**


Create TMUX Session
`tmux new -s [anything]`


Rename Tabs
`Ctrl + a` `,`
![[Pasted image 20240619180658.png]]
![[Pasted image 20240619180718.png]]
The `0` tells us we are in the first tab


Create New Tab
`Ctrl + a` `c`


Toggle Tabs
`Ctrl  a` `[tab number]`

***
**Split/Resize Pane**

Vertical
`Ctrl + a` `Shift + 5` (% or Grapes)
Horizontal
`Ctrl +a` `"`

Kill Pane
`Ctrl + a` `x` or `exit`


Resize Pane
`Ctrl + a` Hold `Ctrl + [arrows]`
or 
`Ctrl + a` `:`
`resize-pane -[UDLR] [Number]`
![[Pasted image 20240619182256.png]]

Move Panes:
`Ctrl + a` `[arrow]`


Toggle Full Screen Window:
`Ctrl + a` `z`


Copy/Paste
`Ctrl + a` `[`
Navigate to where you want to start copying and press `space` and use arrows to highlight portion
Press `enter` to save to clipboard

`Ctrl + a` `]` to paste

***
You can close tmux windows and continue where you left off by using:

List any current tmux sessions
`tmux ls`

`tmux attach`

***
***

**OBSIDIAN**

Use Kali-Tweaks to install Virtualization packages
https://www.kali.org/docs/virtualization/install-vmware-guest-tools/
`mount-shared-folders`

![[Pasted image 20240620122938.png]]

Install App Image:
https://obsidian.md/download

- Make executable and run

![[Pasted image 20240620123355.png]]

Make alias in `~/.bash_aliases`

`alias obsidian=/[path]/[to]/Obsidian-1.6.3.AppImage`

***
***

