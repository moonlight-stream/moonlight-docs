NOTE: If you installed an earlier preview version of Moonlight Qt prior to v2.0.0, you must switch to the official repository to receive the update to v2.0.0 and future updates. To do so, run the the commands listed in the installation section and then those listed in the updates section.

Requirements:
- Raspberry Pi 4 or later (earlier Raspberry Pi models may not perform well)
- Raspberry Pi OS 12 (Bookworm) or later

[![Hosted By: Cloudsmith](https://img.shields.io/badge/OSS%20hosting%20by-cloudsmith-blue?logo=cloudsmith&style=for-the-badge)](https://cloudsmith.com)

## Installation
Run the following commands to install Moonlight Qt to your Raspberry Pi:
```
curl -1sLf 'https://dl.cloudsmith.io/public/moonlight-game-streaming/moonlight-qt/setup.deb.sh' | distro=raspbian codename=$(lsb_release -cs) sudo -E bash
sudo apt install moonlight-qt
```

You can then launch Moonlight from your Raspberry Pi's desktop or via the `moonlight-qt` command in the terminal.

For best performance, run Moonlight directly from a console/TTY. If you are currently in a desktop environment, you should be able to switch using Ctrl+Alt+(F1-F7). Usually your desktop will be at Ctrl+Alt+F1 or Ctrl+Alt+F7, so you can pick a different TTY that's not being used.

**NOTE**: If you run Moonlight from a desktop environment with the Raspberry Pi 4, we recommend keeping your Raspberry Pi's display resolution set to 1080p or below. Due to GPU performance limitations on the Pi 4, streaming performance decreases significantly when the Moonlight window is scaled larger than 1080p, even if the stream resolution is 1080p or below. These restrictions do not apply when streaming directly from a console/TTY using the steps above.

### Audio on Raspberry Pi OS Lite

Raspberry Pi OS Lite doesn't come with any audio daemon by default, so you should install PulseAudio otherwise audio over HDMI may not work.

Perform the following steps to install and configure PulseAudio:
1. `sudo apt install pulseaudio`
2. `sudo raspi-config`
3. Navigate to Advanced Settings -> Audio Config and select "PulseAudio"
4. Reboot your Pi (`sudo reboot`)
5. `sudo raspi-config`
6. Navigate to System Settings -> Audio and select the audio output you want to use

If you want to switch audio outputs, simply follow steps 5 and 6 again.

### Updates
To update Moonlight Qt after you've installed it, run:
```
sudo apt update
sudo apt upgrade
```

### OSMC

OSMC uses a different permission group for input devices than Raspberry Pi OS does. Input devices work, but you will not have any of the extended DS4/DS5 controller features by default.

To fix this, run the following command and reboot:
```
sudo usermod -a -G input $USER
```

## Common problems and solutions

### HDR option cannot be enabled or display doesn't switch to HDR mode

If the HDR option cannot be enabled, you are probably running Moonlight from within the desktop environment. Moonlight must be run directly from the console for HDR to be available.

If you can stream HDR but it doesn't switch your TV to HDR mode, you are probably not using the Full KMS driver (`vc4-kms-v3d`) that is required for HDR metadata to be sent to your TV. Ensure your `/boot/config.txt` is updated to use `vc4-kms-v3d` (not `vc4-fkms-v3d`) and try again.

### PS4/PS5 controller features aren't working

This is likely caused by Moonlight not having permission to open `/dev/hidraw` devices on your Pi. This is a common issue on OSMC, which doesn't use the `input` group in the same way that Raspberry Pi OS does.

To fix this, run the following command and reboot:
```
sudo usermod -a -G input $USER
```

### No audio output
If you are on _Raspberry Pi OS Lite_, make sure you've followed the steps [here](https://github.com/moonlight-stream/moonlight-docs/wiki/Installing-Moonlight-Qt-on-Raspberry-Pi-4/#audio-on-raspberry-pi-os-lite) first!

The most common issue is simply failing to configure the default audio device properly. Use the `raspi-config` tool, navigate to System Settings -> Audio, then select the audio device you want to use.

If you've set your audio device and Moonlight still cannot output audio, you can try an alternate SDL audio driver using the following commands:
- `SDL_AUDIODRIVER=alsa moonlight-qt`
- `SDL_AUDIODRIVER=pulseaudio moonlight-qt`

### Decoder Errors with a 4K 60 Hz Monitor
If your Raspberry Pi is configured for 4K 60 Hz output, you will need to increase the amount of GPU memory for the hardware video decoder to work.

Run the following commands:
```
echo "gpu_mem=128" | sudo tee -a /boot/config.txt
sudo reboot
```