<a href="https://moonlight-stream.org/discord"><img src="https://moonlight-stream.org/images/discord.png" height="70" alt="Join our Discord"></a>

# Windows
Moonlight uses either DXVA2 or D3D11VA for hardware acceleration on Windows, depending on hardware support and OS version. All modern GPUs from AMD, NVIDIA, and Intel should support hardware decoding of H.264 via DXVA2 or D3D11VA with the proper drivers installed.

If you have issues with hardware decoding:
* Ensure your client PC GPU drivers are properly installed and up-to-date from the GPU manufacturer or PC vendor's website.
* If your client PC supports NVIDIA Optimus, try switching Moonlight to run on the integrated Intel GPU.
* Ensure you're not using Remote Desktop to access your PC. This can prevent your GPU from being usable for rendering.

# Mac
Moonlight uses VideoToolbox for hardware acceleration on macOS. All Macs capable of running the latest release of macOS should support hardware H.264 decoding without any work required.

If you are using Hackintosh machine, you'll need to find a GPU driver (if available) that correctly implements VideoToolbox decoding for H.264 video.

# Linux
Moonlight uses VAAPI, VDPAU, and NVDEC for hardware acceleration on Linux. One of those APIs should be compatible with any modern desktop GPU. The most common issue preventing it from working properly is a missing driver package for your GPU or if your distro doesn't include H.264 and HEVC decoding support in their Mesa package for AMD GPUs (openSUSE and Fedora don't).

* Hardware acceleration support may differ between included libraries within the Flatpak, Snap, and AppImage packages. If you have hardware acceleration issues, trying a different Moonlight package may resolve the issue.

* If you are running Moonlight via AppImage, you will need to ensure the appropriate video acceleration drivers are installed on your system. On Debian-based distros like Ubuntu, run `apt-get install va-driver-all vdpau-driver-all`. On newer Intel hardware, you may need to also run `apt install intel-media-va-driver-non-free`.

* If you installed Moonlight via Flatpak, you may need extra packages to utilize hardware video decoding in Flatpak applications.
    * For AMD GPUs, run `flatpak install flathub org.freedesktop.Platform.GL.default//22.08-extra` to install the required Mesa video codecs.
    * For Intel and Nvidia GPUs, run `flatpak update` to ensure the appropriate packages are installed and up-to-date.

* If you are running Wayland on GNOME, you may need to launch Moonlight with the `-platform wayland` option to ensure hardware acceleration works.
    * If you installed Moonlight via Snap, run `moonlight -platform wayland`.
    * If you installed Moonlight via Flatpak, it runs under Wayland by default.
    * Decoding performance under Wayland may not be as good as X11, so try X11 if you experience performance issues.

* For AMD GPU users on Fedora 37 or later, you will need to configure [RPM Fusion Free repositories](https://rpmfusion.org/Configuration) and follow the setup instructions in the "Hardware codecs with AMD" section in [this documentation](https://rpmfusion.org/Howto/Multimedia) to install drivers capable of hardware H.264 and HEVC decoding.

# Steam Deck
The current Steam OS Preview v3.4 disables H.264 and HEVC hardware decoding functionality. This affects both Moonlight and native Steam Link streaming.

See https://github.com/ValveSoftware/SteamOS/issues/903 for details.

If you are willing to risk modifying your OS, you can try the workaround in https://steamcommunity.com/app/1675200/discussions/0/3541546590709961979/

# Raspberry Pi
Moonlight uses the Raspberry Pi's H.264 hardware decoder using the MMAL decoder library. It can also use the HEVC decoder in the Raspberry Pi 4 and later hardware, as long as you've [followed the steps to enable it](https://github.com/moonlight-stream/moonlight-docs/wiki/Installing-Moonlight-Qt-on-Raspberry-Pi-4#hevc-support) and you're running Moonlight outside of the desktop environment.

**First, ensure you have [followed the instructions here](https://github.com/moonlight-stream/moonlight-docs/wiki/Installing-Moonlight-Qt-on-Raspberry-Pi-4#raspbian-bullseye) to ensure you're using the correct display driver for streaming.** Without this step, the H.264 decoder will not work!

If the H.264 decoder still fails to initialize after following the above steps, this usually means that the amount of reserved GPU memory is insufficient.

To increase the reserved GPU memory, run the following commands:
```
echo "gpu_mem=128" | sudo tee -a /boot/config.txt
sudo reboot
```