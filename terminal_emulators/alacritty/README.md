# Alacritty

## What Is Alacritty?

Alacritty is a free, open-source, cross-platform terminal emulator written in **Rust** that leverages **OpenGL** for rendering.
Its primary design goals are **speed**, **simplicity**, and **low latency**.
Unlike some other terminal emulators, Alacritty intentionally avoids features such as built-in tabs or split panes, advocating instead that users integrate it with terminal multiplexers (e.g., tmux) or window managers.

---

## Key Features

Some of the most notable features of Alacritty are:

* **GPU-accelerated rendering**, which contributes to its high performance.
* **Cross-platform support**: it runs on Linux, BSD, macOS, and Windows.
* **Live configuration reload**: when you modify its config file, many changes apply without restarting.
* **Vi mode**: allows for vi-like keybindings to navigate the scrollback buffer and make selections.
* **Search functionality**: you can search within the scrollback buffer.
* **Regex hints**: Alacritty can highlight text (like URLs) based on regular expressions, making it interactive.
* **True color (24-bit)** support, giving you rich color schemes.

---

## Installation

### Install via Distribution Package Manager (Fastest Path)

#### Ubuntu / Debian

```bash
sudo apt update
sudo apt install alacritty
```

If unavailable in your repo, install from a PPA:

```bash
sudo add-apt-repository ppa:mmstick76/alacritty
sudo apt update
sudo apt install alacritty
```

#### Fedora

```bash
sudo dnf install alacritty
```

#### Arch / Manjaro

```bash
sudo pacman -S alacritty
```

#### openSUSE

```bash
sudo zypper install alacritty
```

#### Validate Installation

```bash
alacritty --version
```

---

## Configuration

### Configuration File

Alacritty uses a configuration file written in **TOML**.
It does *not* generate a config file by default; you need to create one yourself.
The program searches for the configuration in these locations (on UNIX-like systems):

1. `$XDG_CONFIG_HOME/alacritty/alacritty.toml`
2. `$XDG_CONFIG_HOME/alacritty.toml`
3. `$HOME/.config/alacritty/alacritty.toml`
4. `$HOME/.alacritty.toml`

On Windows, the config file is looked for under `%APPDATA%\alacritty\alacritty.toml`.

### Important Configuration Sections

Here are some common sections you will likely modify in `alacritty.toml`:

* **[general]**: Global settings, such as whether to reload config on changes (`live_config_reload`), or IPC.
* **[window]**: Window settings, like padding, dimensions, or using a custom box-drawing font.
* **[font]**: Specify the font family, style (italic, bold), size, and offsets.
* **[colors]**: Define color palettes, cursor color, vi-mode cursor, blinking behavior, etc.
* **[terminal]**: Terminal-specific behavior, like shell program, OSC-52 clipboard behavior, etc.
* **[mouse]**: Mouse behavior, e.g., hiding cursor while typing, double-click timing.
* **[keyboard]**: Custom keybindings and shortcuts.
* **[debug]**: Settings for logging, rendering timers, or verbose output.

---

## Common Challenges and Tips

1. **No config file by default**: Since Alacritty doesn’t ship with a template config, you may need to copy a sample from the GitHub repo or other users’ dotfiles and tailor it.
2. **Migrating from YAML to TOML**: Earlier versions of Alacritty used YAML config (`alacritty.yml`). If you're upgrading, run `alacritty migrate` to convert to TOML.
3. **No tab support**: As noted, Alacritty intentionally avoids built-in tabs; use tmux or your window manager to manage multiple sessions.
4. **Setting default terminal in desktop environments**: On some Linux distributions (e.g., GNOME), making Alacritty the default terminal requires setting alternatives or desktop-application defaults.
5. **Ligature support**: Alacritty does *not* support font ligatures.

---
