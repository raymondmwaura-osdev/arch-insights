# Synthesizers

A synthesizer is a device (hardware or software) that plays audio of different instruments. Instead of playing back a recording, a synthesizer creates sounds electronically from scratch. For example, you tell a synthesizer to play note 60 (middle C) on instrument 0 (piano) at velocity 127 (loud). The synthesizer generates the audio waveform and plays it. I used this to play midi files using Python.

`timidity` is a synthesizer for Linux.

```sh
# Install timidity
sudo pacman -S timidity++ soundfont-fluid

# Start timidity as an ALSA sequencer
timidity -iA

# (optional) Enable it as a systemd service.
sudo systemctl enable --now timidity
```

`fluidsynth` is a more modern synthesizer.

```sh
# Install fluidsynth and a soundfont
sudo pacman -S fluidsynth soundfont-fluid

# Start fluidsynth
fluidsynth -a alsa -m alsa_seq /usr/share/soundfonts/FluidR3_GM.sf2

# Or run it as a systemd service
systemctl --user enable --now fluidsynth
```

To test, run this python script:

```python
import pygame.midi

pygame.midi.init()

# List devices to verify
for i in range(pygame.midi.get_count()):
    info = pygame.midi.get_device_info(i)
    print(f"Device {i}: {info[1].decode()}")

pygame.midi.quit()
```

"TimiMidity port 0" or "FLUID Synth" should be listed in the output. If they are missing, you might need:

```sh
sudo pacman -S alsa-utils alsa-lib
```

---
