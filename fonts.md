# Font Setup

This file documents how to install the Jetbrains Nerd font and setting it as the default for applications on arch linux.

+ Install the font.
  ```
  sudo pacman -S ttf-jetbrains-mono-nerd
  ```
+ Refresh the font cache.
  ```
  fc-cache
  ```
+ Make it the default for applications.
  - Create `~/.config/fontconfig/fonts.conf` and write this.

  ```
  <?xml version="1.0"?>
  <!DOCTYPE fontconfig SYSTEM "fonts.dtd">
  <fontconfig>
    <alias>
      <family>monospace</family>
      <prefer>
        <family>JetBrainsMono Nerd Font Mono</family>
      </prefer>
    </alias>
  </fontconfig>
  ```

---
