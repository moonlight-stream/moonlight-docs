Beginning with Moonlight Qt v5.0.0, we are now publishing experimental Debian Sid packages for use on single-board computers or other embedded devices. This packages are designed for devices that have standards-compliant V4L2 H.264 and/or HEVC decoders and working DRI drivers.

SBCs often have notoriously bad video and graphics drivers (sometimes requiring special patches to work), so your experience may vary depending on your hardware and which distro you choose.

These packages are designed to be used directly from the console (not inside a desktop environment) for best performance.

Requirements:
- RISC-V board
- Debian/Armbian Sid
- Working V4L2 H.264 or HEVC decoder (stateful or stateless)
- Linux kernel v5.8 or later

Tested working devices:
- VisionFive 2 (JH7110) using the [Debian image provided by StarFive](https://rvspace.org/en/project/VisionFive2_Debian_User_Guide)

Tested non-working devices:
- TH1520-based devices such as the LicheePi 4a (due to lack of V4L2 drivers for the VPU)

[![Hosted By: Cloudsmith](https://img.shields.io/badge/OSS%20hosting%20by-cloudsmith-blue?logo=cloudsmith&style=for-the-badge)](https://cloudsmith.com)

## Installation
Run the following commands to install Moonlight Qt to your device:
```
curl -1sLf 'https://dl.cloudsmith.io/public/moonlight-game-streaming/moonlight-qt/setup.deb.sh' | codename=sid sudo -E bash
sudo apt install moonlight-qt
```

### Updates
To update Moonlight Qt after you've installed it, run:
```
sudo apt update
sudo apt upgrade
```

### Running Moonlight

First, make sure to **complete any relevant device-specific steps in the section below**, then start Moonlight by running the `moonlight-qt` command.

For best performance, run Moonlight directly from a console/TTY. If you are currently in a desktop environment, you should be able to switch using Ctrl+Alt+(F1-F7). Usually your desktop will be at Ctrl+Alt+F1 or Ctrl+Alt+F7, so you can pick a different TTY that's not being used.

## Device-Specific Steps

### VisionFive 2


**Recommendations**

When using the [Debian image provided by StarFive](https://rvspace.org/en/project/VisionFive2_Debian_User_Guide), don't install their patched Qt package because it has a broken TLS implementation. Instead, you can simply use the Qt packages already provided by the existing APT repo from upstream Debian.

**Initial Setup**

First, you will need to add your local user account to the `video` and `input` groups in order for Moonlight to be able to directly open video devices and read input devices, then logoff or reboot for the changes to take effect. You can do so using the following commands
```
sudo usermod -a -G video $USER
sudo usermod -a -G input $USER
sudo reboot
```

Note: Since `video` and `input` groups are used to enforce multi-user separation, adding unprivileged users to these groups is not recommended.

**Setup Required After Reboots**

The current Debian image for the VisionFive 2 board from StarFive defaults to OMX-based video decoding drivers rather than V4L2. This Moonlight build only supports V4L2 decoding, so leaving the OMX drivers loaded will lead to a video decoding warning in Moonlight.

You can switch to the V4L2 driver using the following commands:
```
sudo modprobe -r vdec
sudo modprobe wave5
```

You will need to reactivate the Wave5 driver using these commands each time you restart your VisionFive board.

**Launching Moonlight**

Finally, to launch Moonlight, you should use the `-platform linuxfb` option since EGLFS UI performance is poor anyway due to non-functional OpenGL ES support on current Debian images. 

In short, to launch Moonlight on the VisionFive board _after following the above steps_, switch to a different TTY with Ctrl+Alt+F2 then run:
```
moonlight-qt -platform linuxfb
```

If everything worked, you should get a GUI and no video decoder warning dialogs.

Note: Due to the use of the LinuxFB Qt backend, you may see minor to moderate UI rendering issues. These will not impact the stream itself.

**Other Notes**

The default kernel used in the StarFive Debian images lacks the built-in drivers for most gamepads. You may have more success using a HID-compliant game controller, such as PS4/5 controllers (though extended features like motion sensors, LED control, and touchpad support will not be available due to the lack of the `hid-playstation` driver in the StarFive kernel.

## Support

For the most part, these packages are provided without official support. We can fix bugs in Moonlight itself, but if it doesn't start or stream at all, odds are that it's related to your hardware or OS and won't be fixable by us.

### GUI doesn't start

This most likely means your device lacks either a working DRI driver (check if a `/dev/dri/card*` device exists) or an OpenGL ES 2.0 driver (even a software one) or that your user account lacks permission to open /dev/dri devices.

The error message from Qt may give you a hint as to what the problem is. You may try adding `-platform linuxfb` to the end of the `moonlight-qt` command (which will somewhat break the UI, but may allow you to get far enough to stream).

If you see an error like `Could not open DRM device /dev/dri/card0 (Permission denied)`, it's probably because your account is not a member of the `video` group. To fix this, run `sudo usermod -a -G video $USER` and reboot.

### Input devices aren't working

This is probably because you're not a member of the `input` group, so Moonlight lacks permission to open input devices to receive input.

To fix this, run `sudo usermod -a -G input $USER` and reboot.

### GUI is very slow/unresponsive

This is usually because your device or distro lacks an hardware accelerated OpenGL ES driver and is using software rendering instead. Unfortunately, this is quite common on many devices due to the lack of open-source drivers. You may try to find a distro that contains proper OpenGL ES drivers, or you can try adding `-platform linuxfb` to the `moonlight-qt` command (which will cause some UI issues, but should make it slightly faster).

Note: Only Moonlight's UI is actually using OpenGL, so the slowness of the GUI will not impact performance while streaming.

### Video decoder error dialog when starting Moonlight

First, make sure you've followed any steps under the "Device-Specific Steps" section above.

If that doesn't work, This means your device or distro doesn't have working V4L2 decoders for H.264 or HEVC. Generally this is a show-stopper for Moonlight Qt on your device, but you may also try [Moonlight Embedded](https://github.com/moonlight-stream/moonlight-embedded) which supports some vendor-specific decoding APIs.

You may try searching the Internet for any special distro builds, newer kernels, or patches that might enable V4L2 decoding on your device's SoC.

### Display doesn't switch to HDR mode or HDR content is not displayed correctly

This usually means that your hardware is probably not exposing the standard properties used for HDR (`COLOR_ENCODING`, `HDR_OUTPUT_METADATA`, and `Colorspace`). You may see an error message from Moonlight referring to one or more of those properties.

If so, there is probably nothing you (or we) can do. You may be able to find a distro or kernel for your device that properly implements HDR modesetting support if you search around.