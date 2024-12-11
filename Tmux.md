`tmux` (Terminal Multiplexer) is a powerful command-line tool that allows you to manage multiple terminal sessions from a single window. It's especially useful for developers, system administrators, and anyone who works extensively in the command line.

---

### Common Use Cases

#### 1. **Session Management**

- Start a session: `tmux new -s mysession`
- Detach from a session: `Ctrl-b d`
- List active sessions: `tmux ls`
- Reattach to a session: `tmux attach -t mysession`

#### 2. **Splitting Panes**

- Split horizontally: `Ctrl-b %`
- Split vertically: `Ctrl-b "`
- Navigate between panes: `Ctrl-b [arrow key]`
- Resize panes: `Ctrl-b` then hold an arrow key.

#### 3. **Window Management**

- Create a new window: `Ctrl-b c`
- Switch between windows: `Ctrl-b [0-9]`
- Rename a window: `Ctrl-b ,`
- Close a window: `exit` (or close the program running in the window).

#### 4. **Session Sharing**

- Allow others to connect to your session: `tmux attach -t mysession`
- Useful for pair programming or debugging sessions.

#### 5. **Scripting and Automation**

- Automate workflows by creating scripts that start tmux sessions with predefined layouts and commands.

---

### Basic tmux Commands

Here’s a quick cheat sheet for essential tmux commands:

|Command|Description|
|---|---|
|`tmux new -s name`|Create a new session|
|`tmux ls`|List active sessions|
|`tmux attach -t name`|Attach to an existing session|
|`Ctrl-b d`|Detach from the current session|
|`Ctrl-b "`|Split pane horizontally|
|`Ctrl-b %`|Split pane vertically|
|`Ctrl-b o`|Toggle between panes|
|`Ctrl-b c`|Create a new window|
|`Ctrl-b n`|Move to the next window|
|`Ctrl-b p`|Move to the previous window|
|`Ctrl-b x`|Close the current pane|

---

### Customization

You can customize tmux by editing the `~/.tmux.conf` file. Example:

```bash
# Remap prefix key from Ctrl-b to Ctrl-a
set-option -g prefix C-a
unbind-key C-b
bind-key C-a send-prefix

# Enable mouse support
set-option -g mouse on

# Set pane splitting shortcuts
bind-key | split-window -h
bind-key - split-window -v
```

---

### Reference

- https://github.com/tmux/tmux/wiki