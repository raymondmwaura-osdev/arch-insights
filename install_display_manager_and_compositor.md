```sh
# Install a display manager.
sudo pacman -S lightdm lightdm-gtk-greeter

# Install a compositor/window manager.
sudo pacman -S sway waybar

# Install GPU drivers.
sudo pacman -S mesa intel-media-driver
```

Configure for wayland by creating a `.desktop` file in `/usr/share/wayland-sessions`:

```ini
# sway.desktop

[Desktop Entry]
Name=Sway
Comment=Wayland compositor
Exec=sway
Type=Application
```

Set default greeter for lightdm in `/etc/lightdm/lightdm.conf`:

```ini
[Seat:*]
greeter-session=lightdm-gtk-greeter
```
