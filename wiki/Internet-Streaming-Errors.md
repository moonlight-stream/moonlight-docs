<a href="https://moonlight-stream.org/discord"><img src="https://moonlight-stream.org/images/discord.png" height="70" alt="Join our Discord"></a>

# Multiple connections error
If you get this warning, your host PC is probably connected to your home network via both WiFi and Ethernet. This can cause connection issues with NVIDIA GameStream. Disconnect one of the connections (preferably the WiFi connection), then try again.

# Connected through another router error
If you get this error, it usually means you have two routers plugged into each other. This is usually caused by having your own wireless router plugged into a router already provided by your ISP. This setup prevents many applications from working optimally, like hosting games, P2P applications, etc.

You can fix this by switching one of your two routers into bridged or Access Point mode. The steps to do this vary by router, but you should be able to find them by Googling around a bit.

If you're sure that you don't have more than one router running on your network, try restarting your router. If that doesn't work, the error may be caused by a Carrier-Grade NAT running on the ISP's network. You can try the steps in the section below to resolve that.

If you can't fix this, you can try using the [ZeroTier setup steps](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide#zerotier) instead.

# Carrier-Grade NAT error
If you get this error, your ISP hasn't given you a public IP address which allows you to host services like Moonlight on the Internet. In many cases, your ISP will be happy to give one to you for free if you just ask.

If your ISP won't give you a public IP address, you can try using the [ZeroTier setup steps](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide#zerotier) instead.

# Limited connectivity for hosting error
If you get this error, your ISP hasn't given you a public IP address which allows you to host services like Moonlight on the Internet. In many cases, your ISP will be happy to give one to you for free if you just ask.

Despite the lack of a public IP address, your connection does offer IPv6 support which will work for hosting over the Internet but streaming will only work natively from networks that also support IPv6. You can check a network's IPv6 support by [running this test](http://test-ipv6.com/) while connected to the network you want to test. If it scores a 10/10, it should be good to go. If not, you may try the [Cloudflare 1.1.1.1 app for iOS and Android](https://1.1.1.1/) with the free 'WARP' feature to gain IPv6 connectivity on networks that don't natively support it.

If your ISP won't give you a public IP address, you can try using the [ZeroTier setup steps](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide#zerotier) instead.

# Internet GameStream connectivity check error
This error usually means your router doesn't have UPnP enabled. Some routers have bugs where UPnP doesn't work properly, so you may check your router manufacturer's website for a firmware update for your router that could fix it. You can also try restarting your router.

This error may also be caused by a firewall product on your host PC blocking the Internet Hosting Tool from talking to your router. Try disabling your host PC's firewall temporarily to see if that's the cause.

If you can't fix this error, you can try using the [ZeroTier setup steps](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide#zerotier) instead or you can [forward the ports manually](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide#manual-port-forwarding-advanced) if you feel comfortable making changes to your router settings.

# Display locked error
This error means that your PC is currently sitting at the lock screen. This may seem counter-intuitive since you've obviously managed to run the tester, but you are probably doing that over Microsoft Remote Desktop.

In order for GameStream to work, your PC's "console session" (physical monitor, keyboard, and mouse) must be logged in. Microsoft Remote Desktop locks the console session until you sign in again, making GameStream unavailable.

You can use a GameStream-compatible remote desktop solution like Chrome Remote Desktop, TeamViewer, or VNC to connect to your PC's console session and sign in again. You will need to use one of these compatible remote desktop apps if you want to use GameStream.

# Local network access blocked error
This error means that something on your PC is blocking access to other devices on your local network. Without access to devices on your network, the Internet Hosting Tool cannot configure your router to allow streaming over the Internet. Depending on how the blocking is implemented, you may not be able to stream at all, even on your home network.

This is most commonly caused by VPN software which contains a feature to disable access to the local network. You will need to disable this in order to stream successfully. Check the documentation for the VPN software if you are unsure of how to disable local network blocking.

Here are links to instructions on unblocking the local network for some commonly used VPN software:
* [Private Internet Access (PIA)](https://www.privateinternetaccess.com/helpdesk/kb/articles/i-cannot-access-devices-on-my-local-network) - enable "Allow LAN traffic"
* [NordVPN](https://support.nordvpn.com/FAQ/Setup-tutorials/1047409642/Installing-and-using-NordVPN-on-Windows-7-and-later-versions.htm#Advanced%20settings) - disable "Invisibility on LAN" and "Internet Killswitch" options
* [ExpressVPN](https://www.expressvpn.com/support/troubleshooting/restore-lan-access/) - enable "Allow access to local network devices such as network shares or printers"

# Sleep mode enabled warning
This warning means your PC is configured to go to sleep after a period of inactivity. This will almost always make the PC unusable for streaming over the Internet until it is manually woken up.

In most cases, you should disable sleep in the Power Settings on your host PC to address this warning. You can leave the monitor power-off option enabled if you wish.

If you have configured a Wake-on-LAN relay device on your network, you can safely ignore this warning. If you don't know what this is, you probably don't have one :)

# Hibernation enabled warning
This warning means your PC is configured to hibernate after a period of inactivity. This will almost always make the PC unusable for streaming over the Internet until it is manually powered back on.

In most cases, you should disable hibernation in the Advanced Power Options on your host PC to address this warning.

If you have configured a Wake-on-LAN relay device on your network and your PC can wake from hibernation via Wake-on-LAN, you can safely ignore this warning. If you don't know what this is, you probably don't have one :)