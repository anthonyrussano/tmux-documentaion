# tmux-documentaion

### Starting, Detaching, and Attaching Sessions
- **Start new session**: `tmux`
- **Start named session**: `tmux new -s [session-name]`
- **List sessions**: `tmux ls`
- **Attach to last session**: `tmux attach`
- **Attach to named session**: `tmux attach-session -t [session-name]`
- **Detach from session**: `Ctrl-b d`

### Managing Windows
- **Create new window**: `Ctrl-b c`
- **Switch to window**: `Ctrl-b [window-number]`
- **Rename current window**: `Ctrl-b ,`
- **List windows**: `Ctrl-b w`
- **Close current window**: `exit` or `Ctrl-d`

### Managing Panes
- **Split pane horizontally**: `Ctrl-b %`
- **Split pane vertically**: `Ctrl-b "`
- **Navigate between panes**: `Ctrl-b [arrow key]`
- **Resize pane**: `Ctrl-b [arrow key]` (after pressing `Ctrl-b :` and typing `resize-pane`)
- **Close current pane**: `exit` or `Ctrl-d`

### Miscellaneous
- **Enter command mode**: `Ctrl-b :`
- **Scrolling**: `Ctrl-b [` then use arrow keys (exit scrolling mode with `q`)
- **Reload tmux configuration**: `Ctrl-b :` then type `source-file ~/.tmux.conf`
- **Show all key bindings**: `Ctrl-b ?`

### Customizing tmux
- **Edit `.tmux.conf` file**: Customize settings in `~/.tmux.conf`

#### Example `tmux.conf` file

```
# Improve colors
set -g default-terminal "screen-256color"

# Set history limit
set -g history-limit 5000

# Set default window and pane base index to 1 (instead of 0)
set -g base-index 1
setw -g pane-base-index 1

# Remap prefix from 'Ctrl-b' to 'Ctrl-a'
unbind C-b
set-option -g prefix C-a
bind-key C-a send-prefix

# Split panes using | and -
bind | split-window -h
bind - split-window -v

# Reload the config file with Ctrl-a r
bind r source-file ~/.tmux.conf \; display "Config reloaded!"

# Navigate panes with Alt-arrow without prefix
bind -n M-Left select-pane -L
bind -n M-Right select-pane -R
bind -n M-Up select-pane -U
bind -n M-Down select-pane -D

# Resize panes with Shift-arrow
bind -n S-Left resize-pane -L 2
bind -n S-Right resize-pane -R 2
bind -n S-Up resize-pane -U 2
bind -n S-Down resize-pane -D 2

# Enable mouse mode (tmux 2.1 and above)
set -g mouse on

# Set aggressive resize option
setw -g aggressive-resize on

# Activity monitoring
setw -g monitor-activity on
set -g visual-activity on

# Enable vi mode for copy-paste
setw -g mode-keys vi
bind-key -T copy-mode-vi 'v' send -X begin-selection
bind-key -T copy-mode-vi 'y' send -X copy-selection-and-cancel

# Set the status line's color and format
set -g status-bg black
set -g status-fg white
set -g status-interval 60
set -g status-left-length 30
set -g status-left '#[fg=green]Session: #S#[fg=white]'
set -g status-right 'Date: %Y-%m-%d Time: %H:%M'
```
