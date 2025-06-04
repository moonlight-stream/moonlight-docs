NOTE: If you installed an earlier preview version of Moonlight Qt prior to v2.0.0, you must switch to the official repository to receive the update to v2.0.0 and future updates. To do so, run the the commands listed in the installation section and then those listed in the updates section.

Requirements:
- Raspberry Pi 4 or later (earlier Raspberry Pi models may not perform well)
- Raspberry Pi OS Buster or later (**see special Bullseye instructions below**)

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

### HEVC and HDR support
Beginning with Moonlight Qt v3.1.2, the Raspberry Pi builds have support for streaming HEVC video using hardware decoding. If you're running Raspberry Pi OS Buster or Bullseye, you may need to perform the steps below to enable this functionality. These steps are not required on the Raspberry Pi 5, Raspberry Pi OS Bookworm, or later OS versions.

To enable HEVC support (only required on older Raspberry Pi OS versions):
- Add `dtoverlay=rpivid-v4l2` to your `/boot/config.txt` and reboot your Pi.
- You must run Moonlight directly from the console for HEVC support to be enabled. If you have your Pi set to boot to GUI, you can press Ctrl+Alt+F1 to switch to TTY 1 and run moonlight-qt from there.

If you would also like to stream HDR, perform these additional steps (only required on older Raspberry Pi OS versions):
- Open `/boot/config.txt`, change `dtoverlay=vc4-fkms-v3d` to `dtoverlay=vc4-kms-v3d`, then reboot your Pi

NOTE: Performing the HDR setup steps will prevent Moonlight from working normally when run within your Pi's desktop environment. You will need to launch Moonlight directly from the console for the video renderer to work properly.

### OSMC

OSMC uses a different permission group for input devices than Raspberry Pi OS does. Input devices work, but you will not have any of the extended DS4/DS5 controller features by default.

To fix this, run the following command and reboot:
```
sudo usermod -a -G input $USER
```

### Raspberry Pi OS Bullseye
Raspberry Pi OS Bullseye defaults to a display driver that doesn't support Moonlight's low-latency H.264 decoder. Unless you have incompatible software on your Pi (like Kodi v19) or need HDR support, we recommend enabling the alternate driver as detailed below.

**Do NOT perform these steps on the Raspberry Pi 5 or Raspberry Pi OS Bookworm! They are no longer required and may render your Pi unbootable!**

To fix this issue, you can edit the `/boot/config.txt` file:
1. Run `sudo nano /boot/config.txt`
2. Scroll down using the arrow keys until you see the line that says `dtoverlay=vc4-kms-v3d`
3. Change that line to `dtoverlay=vc4-fkms-v3d`
4. Press Ctrl+X, press Y, then press Enter
5. Reboot your Pi

**Workarounds for incompatible software (Kodi v19+)**

If you are using software that requires `vc4-kms-v3d` (such as Kodi v19 or later), you can force Moonlight to use the slower V4L2M2M decoder to enable it to function in this scenario. V4L2M2M adds between 1 and 2 frames of additional latency at 1080p compared to the optimal solution above (using `vc4-fkms-v3d`). This workaround is no longer required on Raspberry Pi 5 or Raspberry Pi OS Bookworm and later.

To enable the V4L2M2M decoder, launch Moonlight with the following command:
```
H264_DECODER_HINT=h264_v4l2m2m DRM_FORCE_DIRECT=1 moonlight-qt
```

It is _highly_ recommended that you enable the HEVC decoder (see "HEVC support" above) to avoid the performance cost of V4L2M2M for host PCs that support HEVC encoding (GTX 900 series and newer).

## Common problems and solutions

### Video decoder error dialog when starting Moonlight or black screen when streaming
This is most likely because you're running Raspberry Pi OS Bullseye or another Linux distro that enables the Full KMS display driver by default.

To fix this, you can follow the steps above in the Raspberry Pi OS Bullseye section.

### HDR option cannot be enabled or display doesn't switch to HDR mode

This is most likely because you have not correctly followed all the steps in the [HEVC and HDR support](https://github.com/moonlight-stream/moonlight-docs/wiki/Installing-Moonlight-Qt-on-Raspberry-Pi-4#hevc-and-hdr-support) section.

If the HDR option cannot be enabled, you have either not enabled the HEVC decoder properly or are running Moonlight from within the desktop environment. Moonlight must be run directly from the console for HDR to be available.

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