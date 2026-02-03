# Audio Server

Check which audio server is running:

```sh
pactl info | grep "Server Name"
```

Possible results:

```
Server Name: PulseAudio (on PipeWire)
```

The above means pipewire is running and emulating pulseaudio.

```
Server Name: pulseaudio
```

The above means pulseaudio is running.

```
Connection failure: Connection refused
```

The above means nothing is running.

---

## Pipewire Setup

Components:

+ `pipewire`: Core audio/video engine.
+ `pipewire-alsa`: ALSA compatibility layer.
+ `pipewire-pulse`: PulseAudio replacement.
+ `pipewire-jack`: JACK replacement.
+ `wireplumber`: Session manager (mandatory).

Installation:

```sh
sudo pacman -S pipewire pipewire-alsa pipewire-pulse pipewire-jack wireplumber
```

If you have conflicting sound servers like pulseaudio installed, remove them.

Enable and start pipewire service. Note that pipewire runs as a user service, not system-wide:

```sh
systemctl --user enable --now pipewire pipewire-pulse wireplumber
```

Install audio utilities:

```sh
sudo pacman -S alsa-utils pavucontrol helvum
```

+ `alsa-utils`: Low-level audio tools (alsamixer, speaker-test)
+ `pavucontrol`: GUI mixer for pipewire/pulseaudio layer
+ `helvum`: Pipewire patchbay (graphical routing tool)

---
