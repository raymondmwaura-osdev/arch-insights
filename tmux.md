# `tmux`

## Reload Config

To reload tmux config without restarting the session use the `source-file` command:

```tmux
tmux source-file ~/.config/tmux/tmux.conf
```

Or bind it to a key:

```tmux
bind r source-file ~/.config/tmux/tmux.conf
```

---

## Key Bindings

All these keybindings are prefixed by `C-b` (the default prefix).

**Note:** `M-key` means `Meta + key`. Meta is the Alt key. That keybinding means you press `key` while holding down the meta key (alt).

+ `M-Up, M-Down, M-Left, M-Right`: Resize the current pane in steps of five cells.
+ `C-Up, C-Down, C-Left, C-Right`: Resize the current pane in steps of one cells.

---
