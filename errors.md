# Display Environment Variables

```
# Raised by firefox.
Error: No DISPLAY environment variable specified
```

```
# Raised by alacritty.
Error: Os(OsError { line: 765, file: "/build/.cargo/registry/src/index.crates.io-1949cf8c6b5b557f/winit-0.30.12/src/platform_impl/linux/mod.rs", error: Misc("neither WAYLAND_DISPLAY nor WAYLAND_SOCKET nor DISPLAY is set.") })
```

The errors above are raised when you try to run a graphical application when not in a graphical session context (from a tty).

This can also happen if you run the application from a tmux session, and tmux was started from a tty. Since tmux was run from a tty, it won't have the `WAYLAND_DISPLAY` or `DISPLAY` environment variables set.
