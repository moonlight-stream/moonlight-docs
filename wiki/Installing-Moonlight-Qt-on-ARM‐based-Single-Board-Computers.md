Beginning with Moonlight Qt v5.0.0, we are now publishing generic armhf and aarch64 Debian packages for use on single-board computers or other embedded devices. This packages are designed for devices that have standards-compliant V4L2 H.264 and/or HEVC decoders and working DRI drivers. Devices that use non-standard video decoding interfaces should use [Moonlight Embedded](https://github.com/moonlight-stream/moonlight-embedded) instead.

ARM SBCs often have notoriously bad video and graphics drivers (sometimes requiring special patches to work), so your experience may vary depending on your hardware and which distro you choose.

These packages are designed to be used directly from the console (not inside a desktop environment) for best performance. Newer devices with more powerful GPUs may perform fine within a desktop environment, though certain features like HDR will not work.

Supported distros:
- Debian/Armbian Bullseye
- Debian/Armbian Bookworm
- Ubuntu 22.04 (Jammy)
- Ubuntu 24.04 (Noble)

Other requirements:
- 32-bit ARMv7 or 64-bit ARMv8 (armhf or aarch64)
- Working V4L2 H.264 or HEVC decoder (stateful or stateless)
- Linux kernel v5.8 or later

Tested working devices:
- Asus Tinkerboard (RK3388) - Armbian Bookworm 
- Orange Pi 4 LTS (RK3399) - Armbian Bookworm

Tested non-working devices:
- **Raspberry Pi - [Use this build instead](https://github.com/moonlight-stream/moonlight-docs/wiki/Installing-Moonlight-Qt-on-Raspberry-Pi-4)**
- NanoPi R6S (RK3588 currently lacks V4L2 drivers)

[![Hosted By: Cloudsmith](https://img.shields.io/badge/OSS%20hosting%20by-cloudsmith-blue?logo=cloudsmith&style=for-the-badge)](https://cloudsmith.com)

## Installation
Run the following commands to install Moonlight Qt to your device:
```
curl -1sLf 'https://dl.cloudsmith.io/public/moonlight-game-streaming/moonlight-qt/setup.deb.sh' | sudo -E bash
sudo apt install moonlight-qt
```

### Updates
To update Moonlight Qt after you've installed it, run:
```
sudo apt update
sudo apt upgrade
```

### Running Moonlight

Start Moonlight by running the `moonlight-qt` command.

For best performance, run Moonlight directly from a console/TTY. If you are currently in a desktop environment, you should be able to switch using Ctrl+Alt+(F1-F7). Usually your desktop will be at Ctrl+Alt+F1 or Ctrl+Alt+F7, so you can pick a different TTY that's not being used.

## Support

For the most part, these packages are provided without official support. We can fix bugs in Moonlight itself, but if it doesn't start or stream at all, odds are that it's related to your hardware or OS and won't be fixable by us.

### GUI doesn't start

This most likely means your device lacks either a working DRI driver (check if a `/dev/dri/card*` device exists) or an OpenGL ES 2.0 driver (even a software one) or that your user account lacks permission to open /dev/dri devices.

The error message from Qt may give you a hint as to what the problem is. You may try adding `-platform linuxfb` to the end of the `moonlight-qt` command (which will somewhat break the UI, but may allow you to get far enough to stream) or try creating a EGLFS configuration json file [as detailed here](https://doc.qt.io/qt-5/embedded-linux.html#eglfs-with-the-eglfs-kms-backend).

If you see an error like `Could not open DRM device /dev/dri/card0 (Permission denied)`, it's probably your account is not a member of the `video` group. To fix this, run `sudo usermod -a -G video $USER` and reboot.

### Input devices aren't working

This is probably because you're not a member of the `input` group, so Moonlight lacks permission to open input devices to receive input.

To fix this, run `sudo usermod -a -G input $USER` and reboot.

### GUI is very slow/unresponsive

This is usually because your device or distro lacks an hardware accelerated OpenGL ES driver and is using software rendering instead. Unfortunately, this is quite common on many ARM devices due to the lack of open-source drivers. You may try to find a distro that contains proper OpenGL ES drivers, or you can try adding `-platform linuxfb` to the `moonlight-qt` command (which will cause some UI issues, but should make it slightly faster).

Note: Only Moonlight's UI is actually using OpenGL, so the slowness of the GUI will not impact performance while streaming.

### Video decoder error dialog when starting Moonlight

This means your device or distro doesn't have working V4L2 decoders for H.264 or HEVC. Generally this is a show-stopper for Moonlight Qt
on your device, but you may also try [Moonlight Embedded](https://github.com/moonlight-stream/moonlight-embedded) which supports some vendor-specific decoding APIs.

You may try searching the Internet for any special distro builds, newer kernels, or patches that might enable V4L2 decoding on your device's SoC.

### Display doesn't switch to HDR mode or HDR content is not displayed correctly

This usually means that your hardware is probably not exposing the standard properties used for HDR (`COLOR_ENCODING`, `HDR_OUTPUT_METADATA`, and `Colorspace`). You may see an error message from Moonlight referring to one or more of those properties.

If so, there is probably nothing you (or we) can do. You may be able to find a distro or kernel for your device that properly implements HDR modesetting support if you search around.