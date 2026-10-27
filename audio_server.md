# Audio Server

An audio server (or sound server) in Linux is a background software program that sits between your applications and the low-level kernel sound driver (ALSA) to manage, mix, and route sound streams. Because raw ALSA drivers traditionally allow only a single application to access a sound card at a time, an audio server acts as a middleman or proxy.

**What an Audio Server Does:**

+ **Software Mixing (Multiplexing)**: Combines audio streams from multiple apps (such as a browser playing a video while a music player runs) into a single unified output stream.
+ **Per-Application Volume Control**: Allows you to adjust or mute the volume independently for each open program.
+ **Device Switching & Management**: Lets you hot-swap audio devices (like plugging in Bluetooth headphones or switching to an HDMI monitor) on the fly.
+ **Resampling**: Converts different audio sample rates (e.g., 44.1 kHz from a CD versus 48 kHz from a video) into a common frequency the hardware supports.
+ **Network Audio**: Can stream audio over a local network to another computer or speaker setup.

**Common Linux Audio Servers:**

+ **PulseAudio**: The long-time standard sound server for general desktop Linux distributions. It offers plug-and-play ease of use and per-app controls, though it introduces moderate latency.
+ **JACK (JACK Audio Connection Kit)**: A professional-grade audio server built for low-latency, real-time audio production, digital audio workstations (DAWs), and complex signal routing among musicians.
+ **PipeWire**: The modern, unified multimedia server replacing both PulseAudio and JACK on most contemporary Linux distributions (such as Fedora and modern Ubuntu releases). It handles low-latency professional audio, video graphs, and full backward compatibility with older PulseAudio and JACK applications.

## Check which audio server is running

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

Install audio utilities:

```sh
sudo pacman -S alsa-utils pavucontrol helvum
```

+ `alsa-utils`: Low-level audio tools (alsamixer, speaker-test)
+ `pavucontrol`: GUI mixer for pipewire/pulseaudio layer
+ `helvum`: Pipewire patchbay (graphical routing tool)

**Enable and start pipewire service.** Note that pipewire runs as a user service, not system-wide:

```sh
systemctl --user enable --now pipewire pipewire-pulse wireplumber
```

---
