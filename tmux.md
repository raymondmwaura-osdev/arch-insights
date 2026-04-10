# `tmux`

To reload tmux config without restarting the session use the `source-file` command:

```tmux
tmux source-file ~/.config/tmux/tmux.conf
```

Or bind it to a key:

```tmux
bind r source-file ~/.config/tmux/tmux.conf
```

---
