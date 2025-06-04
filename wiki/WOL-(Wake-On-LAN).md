## Overview
WOL (Wake On LAN) allows the waking of a suspended or shutdown system over LAN.

Note that not every system (especially laptops) supports WOL and or waking from shutdown.

A static DHCP lease (also known as a static Local IP) for your host in your router is recommended to improve reliability and is required for WOL over the Internet. See: https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide#static-dhcp-reservation

WOL over Wi-Fi is usually unstable. It is always recommended to have a wired connection for the host when possible.

WOL has to be enabled both in the UEFI/BIOS and OS in order to function.

## UEFI/BIOS Setup
*These steps may differ depending on your system*

First, enter the UEFI/BIOS. Pressing the __delete__ key during boot usually works, you can also try __F2__ or __F12__. Alternatively on Windows 8+ you can hold the __Shift key while Rebooting__ Then navigate to Troubleshooting>Boot to UEFI.

Look for a setting usually found in "Power" or "PCI sub system" called "Power On By PCI Device" or "Wake-on-LAN" or similar. These need to be enabled.

## Windows Setup
Open Device Manager, You can do this by right-clicking the Windows Icon. Then navigate to "Network Adapters", Right-click your Adapter, and go to its properties. Then go to the Advanced tab. In the list look for "Wake on Magic Packet" and enable it, it is usually towards the bottom. "Wake on Magic Packet from system shutdown" allows for Waking from shutdown. __Wake on pattern should remain Disabled!__ Having it Enabled can result in random system wakes from normal network scans and such.

![Wake on Magic Packet 1](https://github.com/moonlight-stream/moonlight-docs/assets/48956874/e4f331c9-5fc3-48ab-91d0-4b8aee09bac1)

If you do not see the options listed above then the NIC (Network Interface Card) either does not support WOL, or the drivers for the NIC are out of date or broken.

Also in the adapter properties under the "Power Management" tab enable "Allow this device to wake the computer" and its sub option.

![Wake on Magic Packet 2](https://github.com/moonlight-stream/moonlight-docs/assets/48956874/d5e5cfb5-9718-4564-a878-a5f418e17880)

## Linux Setup
In the Terminal run `ifconfig -a` and note the desired eth#.

Install "ethtool" if not already installed, run `sudo ethtool eth#` and replace eth# with noted. Check the output, if there is a "G" next to "Supports Wake-on" then the NIC supports WOL. Run `sudo ethtool -s eth# wol g` again replace eth# with noted.

## Internet WOL
WOL is not designed to work over WAN. (Wide Area Network, AKA Internet) But it can be done in a few ways, some safer than others. The list below is in the order of recommended methods. Most methods require some other device that is always online and connected you your __Host's__ local network.

DDNS or a static Public IP is a requirement for most options. see https://www.noip.com/ a DDNS service.

- Host a VPN server. You will need some other device that is always online and connected to the Host's network to act as a VPN server. You also need the ability to port forward on your router. The WOL packet can be sent from the Moonlight client to the sleeping host via a VPN tunnel. Also see the WOL Tailscale container in the next section. Such devices include but are not limited to;
    - Routers, many can run a VPN server and even have a baked-in utility for hosting a VPN.
    - A RPI (Raspberry PI) or other similar SBC.
    - A NAS. (Network Attached Storage) Basically a Server, a NAS can host a variety of servers including VPN servers. Many customer NAS devices have a baked-in VPN utility.
- Have another device wake the system. You will need some other device that is always online and connected to the Hosts network to act as in essence a WOL relay. Depending on the device used you may need to port forward. Such devices include but are not limited to;
    - Router WOL utility. Many routers offer a WOL utility either usable with just a router app or by port forwarding the router GUI. (If you do the latter be sure to have an EXTREMELY robust login for the router. Not recommended)
    - WOL Tailscale container. This option is great if you are behind a __CGNAT__ or are __unable to port forward__. https://github.com/andygrundman/tailscale-wakeonlan
    - A RPI. https://www.instructables.com/id/Raspberry-Pi-As-Wake-on-LAN-Server/
    - A remotely accessible system such as a NAS, or similar.
    - An Arduino with a network connection. https://github.com/TullyE/ArduinoWOL/
    - Use Home Assistant. https://www.home-assistant.io/integrations/wake_on_lan/
- Forward and allow through the router firewall port 9 to the Host. This will only work for ~2 hours due to the way IPs work. after such time you __Will__ need to use one of the other methods mentioned above.

## WOL Alternatives
If your system either does not have the ability to use WOL, or you can not use the Internet WOL methods mentioned above you may be able to use the following tactics to achieve a similar effect.
- Use a smart plug. You can set the system UEFI/BIOS to power on the system when power is lost and then restored. When you want to start the system you just turn the smart plug off and on.
- Use an in-system KVM/Remote management board to interact with the system and it's internal power switch header such as: https://geekworm.com/products/pikvm-a8?_pos=1&_sid=333b48621&_ss=r
- Set the UEFI/BIOS to wake the system at a certain time.

## Tips and Tricks
- WOL has a tendency to break when a system is asleep for a prolonged period of time usually due to a very small network hiccup (usually not even noticeable). This is particularly annoying when abroad. One way to get around this is to set the UEFI of the host to wake the system every day at say 1:00 AM, then have a scheduled task in Windows to sleep the system at say 1:05 AM. This will allow the system to re-establish a network connection at least once a day if it happened to break.