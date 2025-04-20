Beginning with Moonlight Qt v2.0.0, support for L4T devices such as the [Nintendo Switch](https://wiki.switchroot.org/en/Linux/Ubuntu-Install-Guide) and NVIDIA Jetson development boards is in beta. As is typical with beta releases, the usual caveats apply: this may not perform well for you; it may crash/hang or just not work at all. Please [report bugs](https://github.com/moonlight-stream/moonlight-qt/issues) if you encounter issues.

NOTE: If you installed an earlier preview version of Moonlight Qt prior to v2.0.0, you must switch to the official repository to receive the update to v2.0.0 and future updates. To do so, you must first run `sudo apt remove moonlight` then run the commands listed in the installation section to install the new `moonlight-qt` package.

[![Hosted By: Cloudsmith](https://img.shields.io/badge/OSS%20hosting%20by-cloudsmith-blue?logo=cloudsmith&style=for-the-badge)](https://cloudsmith.com)

Requirements:
* Linux4Tegra OS based on Ubuntu 18.04, Ubuntu 22.04, or Ubuntu 24.04

### Installation
Run the following commands to install Moonlight Qt to your L4T device:
```
curl -1sLf 'https://dl.cloudsmith.io/public/moonlight-game-streaming/moonlight-l4t/setup.deb.sh' | sudo -E bash
sudo apt install moonlight-qt
```

You can then launch Moonlight from your desktop or via the `moonlight-qt` command in the terminal.

### Updates
To update Moonlight Qt after you've installed it, run:
```
sudo apt update
sudo apt upgrade
```