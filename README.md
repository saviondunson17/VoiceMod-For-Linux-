# VoiceMod-For-Linux-
VoiceMod for Ubuntu
# Reggie Voice Changer

A community-built, VoiceMod-inspired real-time microphone effects app for Linux.
This is an **early starter build**, not an official VoiceMod product.

## Current starter features
- PySide6 desktop interface
- Microphone and output-device selection
- Live clean, robot, echo, and radio-style effects
- PipeWire/PulseAudio virtual-sink helper scripts
- Debian package build script

## Requirements
Designed for Ubuntu with PipeWire and its PulseAudio compatibility layer.

Install system dependencies:

```bash
sudo apt update
sudo apt install -y python3 python3-pip python3-venv python3-dev \
  build-essential dpkg-dev pipewire pipewire-pulse pulseaudio-utils \
  libportaudio2
```

Create a virtual environment and install Python dependencies:

```bash
cd Reggie-Voice-Changer
python3 -m venv .venv
. .venv/bin/activate
python -m pip install --upgrade pip
pip install -r requirements.txt
python -m reggie_voice_changer
```

If your terminal says `No module named reggie_voice_changer`, run the app from
the project root with:

```bash
PYTHONPATH=src .venv/bin/python -m reggie_voice_changer
```

## Set up the virtual microphone

In another terminal:

```bash
bash scripts/create-virtual-mic.sh
```

In Reggie Voice Changer, choose your physical microphone as the input and
the `Reggie Voice` / `ReggieVoice` output as the output device if it appears.
Then open VRChat's microphone settings and choose **Monitor of Reggie Voice**
(or `ReggieVoice.monitor`) as the input.

To remove the virtual sink:

```bash
bash scripts/remove-virtual-mic.sh
```

If the output device does not appear in the app, check `pavucontrol` or
`pactl list short sinks` and select the matching device. Audio-device
availability depends on the Ubuntu audio stack and PortAudio build.

## Build a .deb

On an Ubuntu build machine, from the project root:

```bash
bash build-deb.sh
```

The package will be written to `dist/reggie-voice-changer_0.1.0_all.deb`.
The .deb declares Ubuntu system Python audio/GUI packages as dependencies.
Package names can differ by Ubuntu release; if `dpkg-deb` builds successfully
but apt cannot resolve a dependency, adjust `debian/control` for that release.

Install:

```bash
sudo apt install ./dist/reggie-voice-changer_0.1.0_all.deb
```

## Important
- This is an MVP starter, not yet a polished or fully tested release.
- Use headphones to reduce microphone feedback.
- Do a local audio test before joining a public VRChat instance.
- Do not use the app to impersonate, harass, or disrupt other people.
- No VoiceMod code, assets, or branding are included.
