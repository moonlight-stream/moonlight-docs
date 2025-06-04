_These troubleshooting checklists contain various suggestions to solve each potential issue. They are generally meant to be done in the order the steps are listed, however the list doesn't need to be fully completed if issue goes away during the process of troubleshooting._

You can chat with Moonlight developers and other users to help you resolve streaming issues on our Discord server.

<a href="https://moonlight-stream.org/discord"><img src="https://moonlight-stream.org/images/discord.png" height="70" alt="Join our Discord"></a>

Look at the troubleshooting steps for each of the following issues: 

* [Unable to stream at all on the same network as the PC](https://github.com/moonlight-stream/moonlight-docs/wiki/Troubleshooting#unable-to-stream-at-all-on-the-same-network-as-the-pc)
* [Unable to stream at all over the Internet](https://github.com/moonlight-stream/moonlight-docs/wiki/Troubleshooting#unable-to-stream-at-all-over-the-internet)
* [Video is choppy or laggy](https://github.com/moonlight-stream/moonlight-docs/wiki/Troubleshooting#video-is-choppy-or-laggy)
* [No video (black screen)](https://github.com/moonlight-stream/moonlight-docs/wiki/Troubleshooting#no-video-black-screen)
* [Missing mouse cursor](https://github.com/moonlight-stream/moonlight-docs/wiki/Troubleshooting#missing-mouse-cursor)
* [Video only displays in the top left corner of the stream](https://github.com/moonlight-stream/moonlight-docs/wiki/Troubleshooting#video-only-displays-in-the-top-left-corner-of-the-stream)
* [Known application compatibility issues](https://github.com/moonlight-stream/moonlight-docs/wiki/Troubleshooting#known-application-compatibility-issues)
* [Pairing dialog won't show up on PC](https://github.com/moonlight-stream/moonlight-docs/wiki/Troubleshooting#pairing-dialog-wont-show-up-on-pc)
* [SHIELD tab is missing in GeForce Experience](https://github.com/moonlight-stream/moonlight-docs/wiki/Troubleshooting#shield-tab-is-missing-in-geforce-experience)
* [Games are missing from Moonlight](https://github.com/moonlight-stream/moonlight-docs/wiki/Troubleshooting#games-are-missing-from-moonlight)
* [Controller input doesn't work when streaming](https://github.com/moonlight-stream/moonlight-docs/wiki/Troubleshooting#controller-input-doesnt-work-when-streaming)
* [Bluetooth-related streaming issues](https://github.com/moonlight-stream/moonlight-docs/wiki/Troubleshooting#bluetooth-related-streaming-issues)

### Known bugs in GeForce Experience that _don't_ affect hosts using [Sunshine](https://app.lizardbyte.dev/Sunshine/)
* [Streamed picture is stuck in the top-left corner](https://github.com/moonlight-stream/nvidia-gamestream-issues/issues/48)
* [Pairing may fail if there are non-ASCII characters in your user name](https://github.com/moonlight-stream/nvidia-gamestream-issues/issues/30)
* [Video freezes with hardware-accelerated GPU scheduling on the host](https://github.com/moonlight-stream/nvidia-gamestream-issues/issues/27)
* [Host mouse cursor is invisible when a UAC dialog is displayed on Win10+](https://github.com/moonlight-stream/nvidia-gamestream-issues/issues/2)
* [Windows OS HDR state is not properly identified when starting a stream](https://github.com/moonlight-stream/nvidia-gamestream-issues/issues/29)
* [Rumble stops working until host PC reboot if nvstreamer.exe terminates unexpectedly](https://github.com/moonlight-stream/nvidia-gamestream-issues/issues/28)

### Unable to stream at all on the same network as the PC
* Ensure you've enabled GameStream in GeForce Experience per the [setup guide](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide)
* Reboot your PC and client device.
* If your gaming PC is connected to your home network via multiple connections (like both Ethernet and WiFi), disconnect all connections except for the fastest one (usually Ethernet).
* Check the list of [known application compatibility issues](https://github.com/moonlight-stream/moonlight-docs/wiki/Troubleshooting#known-application-compatibility-issues). Try uninstalling any programs on that list one to see if one of them is interfering.
* Make sure your primary monitor is connected to your NVIDIA GPU and turned on, and you are logged in.
* If you use a VPN for Internet access on your gaming PC, disable it to ensure your local network is accessible. You may also need to [disable the setting to block local network access](https://github.com/moonlight-stream/moonlight-docs/wiki/Internet-Streaming-Errors#local-network-access-blocked-error).
* Disable your PC's firewall and anti-virus, and reboot again. If this works, you can create a firewall exception using [the steps here](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide#firewall-setup).
* Uninstall GeForce Experience, reboot, clean install GeForce Experience, and reboot again.
* In an administrator command prompt, run `netsh winsock reset` and reboot your computer.
* If your PC is running Windows Server, install the qWave service and ensure the Windows Audio service is enabled and running.
* If you had used Microsoft Remote Desktop you will need to follow the instructions in the [Known Compatibility Issues](https://github.com/moonlight-stream/moonlight-docs/wiki/Troubleshooting#known-application-compatibility-issues) in order to stream again.
* Ask for help on our [Discord server](https://moonlight-stream.org/discord)

### Unable to stream at all over the Internet
* First, ensure you can stream successfully from your home network to ensure it's an issue specific to streaming over the Internet. If you can't, follow the instructions in the section above for general streaming issues.
* Make sure your gaming PC is running the [Moonlight Internet Hosting Tool](https://github.com/moonlight-stream/Internet-Hosting-Tool/releases) to automatically manage your port forwarding rules.
* Ensure UPnP is enabled in your router settings and delete any older Moonlight port forwarding entries.
* If you use a VPN for Internet access on your gaming PC, disable it to ensure your local network is accessible. You may also need to [disable the setting to block local network access](https://github.com/moonlight-stream/moonlight-docs/wiki/Internet-Streaming-Errors#local-network-access-blocked-error).
* Run the "Moonlight Internet Streaming Tester" found in the [Moonlight Internet Hosting Tool](https://github.com/moonlight-stream/Internet-Hosting-Tool/releases) and ask for help on our [Discord server](https://moonlight-stream.org/discord). Be sure to have the tester log handy.
* If the Moonlight Internet Streaming Tester says your ISP is running a [Carrier-grade NAT](https://en.wikipedia.org/wiki/Carrier-grade_NAT) that blocks hosting services like Moonlight, try these steps:
    * Ask your ISP for a public IP address. Many users have reported that their ISP is happy to provide one free of charge upon request.
    * Many users have reported good streaming performance using the [ZeroTier](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide#zerotier) setup steps.
    * You can try using the [IPv6 setup steps](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide#ipv6-certain-isps-only) if your home ISP and client network both support IPv6. You can check this by seeing if you score a 10/10 on [this web IPv6 test](http://test-ipv6.com/).
* Ask for help on our [Discord server](https://moonlight-stream.org/discord)

### Video is choppy or laggy
* If you have issues with the video getting stuck while streaming, disable hardware-accelerated GPU scheduling on your host PC.
* Try streaming with Bluetooth disabled to see if your device has the Bluetooth issue detailed below.
* Make sure your client device is connected on 5 GHz WiFi or Ethernet, and your PC is wired to your router if possible.
* If you're streaming to a Mac over WiFi, try [disabling Location Services and AirDrop](https://github.com/moonlight-stream/moonlight-qt/issues/159#issuecomment-452675992).
* If you're streaming to a Windows PC with an Intel WiFi adapter, try setting "Global BG scan blocking" to "On Good RSSI" in the Device Manager Properties for the WiFi adapter. If "On Good RSSI" does not show up, try using "Always" instead.
* Ensure your Nvidia GPU is not being underclocked (which can impact NVENC performance). You may also try a modest overclock or raising the GPU power limit if you are comfortable with that.
* Lower the bitrate slider to determine if it's a bandwidth issue.
* Try using 720p30 which has the lowest requirements.
* Ask for help on our [Discord server](https://moonlight-stream.org/discord)

### No video (black screen)
* Ensure your monitor is powered on and connected to your NVIDIA GPU
* If you want to stream without a monitor connected, you can buy a cheap headless HDMI dongle like [this one](https://www.amazon.com/fit-Headless-GS-resolution-emulator-game-streaming/dp/B01EK05WTY)
* Try a different game or stream Steam to see if it's game-specific. You may be able to work around the game-specific issues by [streaming your whole desktop](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide#using-moonlight-to-stream-your-entire-desktop) and starting the game from there.
* Ask for help on our [Discord server](https://moonlight-stream.org/discord)

### Missing mouse cursor
* Ensure a mouse is connected to your host gaming PC
* If unable to physically connect a mouse, enable Mouse Keys on the host gaming PC to force Windows to display a mouse cursor.
    * If you just type "Mouse key" into the Start Menu search dialog, it should take you to the correct settings page.
* Ask for help on our [Discord server](https://moonlight-stream.org/discord)

### Video only displays in the top left corner of the stream
* Use the NVIDIA Control Panel to set your desired display resolution, not Windows Display Settings
   * If your resolution is already set to the desired value, change it to something else and back again using NVIDIA Control Panel.

### Known application compatibility issues
Some installed applications and security products can interfere with GeForce Experience or GameStream. Depending on the configuration of these incompatible applications, you may or may not experience issues streaming.

Special-case issues:
* Parsec/Rainway/Steam In-Home Streaming
    * Disconnect your stream before using Moonlight to avoid encoder conflicts with other streaming apps
* NordVPN, TunnelBear, PIA, and other VPNs
    * Disable the VPN if Moonlight cannot discover your gaming PC or stream over the Internet
    * You may also need to [disable the setting to block local network access](https://github.com/moonlight-stream/moonlight-docs/wiki/Internet-Streaming-Errors#local-network-access-blocked-error).
* Safing Portmaster
    * Streaming may not work until the program is fully uninstalled
* Microsoft Remote Desktop
  * When using RDP, your computer is technically locked, causing streaming issues even after disconnecting. This lock prevents starting programs with Moonlight.
  * Sunshine Hosts
    * Log back into the computer via the "Desktop" app in Moonlight, then you can end and start another stream with the application you wanted originally.

  * Geforce Experience Hosts
      * Log into the computer physically or you may use the following script commands in a PowerShell terminal while in an RDP session:

      ```powershell
      $session = (query session | Select-String $env:USERNAME) -split " " | Where-Object { $_ } | Select-Object -Index 2
      & tscon $session /dest:console
      ```
      This will terminate your RDP session but leave it unlocked, allowing you to stream again.

   * Chrome Remote Desktop, TeamViewer, or VNC can be used for remote access without breaking Moonlight
* Teamspeak Gamepad Plugin
    * The gamepad plugin may cause [extra gamepads to appear in Device Manager](https://github.com/moonlight-stream/moonlight-qt/issues/304), but streaming works normally
* Password managers (KeePass, iCloud Keychain, and potentially others)
    * In order to improve security, some password managers report themselves as protected content (like DRM) to Windows. This can interfere with streaming.
    * If you have trouble streaming while a password manager is running, check the password manager's settings to see if it's possible to turn this protection off.
* Valorant (The kernel level DRM. A full Windows reinstall may be required to allow Gamestream to function.)

If you have one of the following, try disabling or uninstalling it:
* 3rd-party Firewalls and Anti-virus
    * Kaspersky in particular may only [stop breaking Moonlight when it is fully uninstalled](https://www.reddit.com/r/theNvidiaShield/comments/4g5fft/gamestreaming_vs_kaspersky_resolved/).
    * Malwarebytes (specifically the Web Protection module)
* DisplayLink dock/display software
* Razer Synapse
* Razer Kraken software (APO Helper)
* ASUS Sonic Studio
* ASUS SonicRadar
* ASUS KeyBot
* ASUS GameFirst
* NVIDIA RTX Voice
* Lenovo Vantage

### Pairing dialog won't show up on PC
* Check the list of known application compatibility issues above. Uninstall any programs on that list, and reboot.
* Reboot your PC
* Delete the following registry value (if present): HKEY_LOCAL_MACHINE\SOFTWARE\NVIDIA Corporation\NvTray\ShowInSedona
* Open the NVIDIA Control Panel, select the "Desktop" menu at the top, and check "Show Notification Tray Icon".
* Uninstall GeForce Experience, reboot, clean install GeForce Experience, and reboot again.
* Ask for help on our [Discord server](https://moonlight-stream.org/discord)

### SHIELD tab is missing in GeForce Experience
* Check the list of known application compatibility issues above. Uninstall any programs on that list, and reboot.
* Reboot your PC
* Install the latest GPU driver from NVIDIA's website
* Uninstall and reinstall GeForce Experience

### Games are missing from Moonlight
* Make sure the folder where your games are installed is listed in GeForce Experience.
    * You can add a games folder by opening GeForce Experience, clicking on the Settings button, then clicking the + button and navigating to the correct folder.
* You can add games manually that aren't detected as streamable by GeForce Experience [using this guide](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide#adding-custom-programs-that-are-not-automatically-found)

### Controller input doesn't work when streaming
* Ensure you're running GeForce Experience 3.15.0 or later
* In Steam Big Picture, go to Settings > Controller Settings, then uncheck all gamepad "Configuration Support" checkboxes
* Check if input works in Steam Big Picture to see if it's a game-specific compatibility issue
* If your host is running Windows Server 2016/2019, you may need to install the [Xbox 360 drivers for Windows 7 64-bit](https://www.microsoft.com/accessories/en-gb/d/xbox-360-controller-for-windows)
* Ask for help on our [Discord server](https://moonlight-stream.org/discord)

### Bluetooth-related streaming issues
Depending on your streaming device, you may have a bad experience if Bluetooth is active while streaming. This is a hardware limitation due to the antenna wiring. If you experience this and are streaming from within your home, you can try connecting the gamepad directly to your PC using a wireless adapter or Bluetooth.

Still having issues? Ask for help on our [Discord server](https://moonlight-stream.org/discord)