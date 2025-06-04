## Information on NVIDIA's GameStream End of Service Notification

See the dedicated [GameStream End of Service Notification FAQ](https://github.com/moonlight-stream/moonlight-docs/wiki/NVIDIA-GameStream-End-Of-Service-Announcement-FAQ) page.

We recommend switching to [Sunshine](https://app.lizardbyte.dev/Sunshine/) for hosting, particularly if you experience issues with stream reliability from GeForce Experience. Unlike GeForce Experience, Sunshine is still receiving new features and bugfixes.

## What is Moonlight?

Moonlight is an unofficial third-party open-source client for the NVIDIA SHIELD streaming software that comes included with GeForce Experience. GeForce Experience uses the NVENC hardware on NVIDIA GPUs and custom tuned software to provide low-latency high-quality PC streaming.

## What do I need for my host PC?

The recommended hosting software [Sunshine](https://app.lizardbyte.dev/Sunshine/), which is fully open-source, supports more platforms and GPUs, and has more features, and lacks most of the annoying bugs in the older GeForce Experience hosting software.

If you want to use GeForce Experience to host instead of Sunshine, your host needs:
- Windows 10 or later
- NVIDIA GeForce GTX/RTX GPU 600-series or later
- NVIDIA GeForce Experience

## What devices can I run Moonlight on?

We have official clients for [Windows, macOS, Linux, Raspberry Pi 4, Steam Link hardware](https://github.com/moonlight-stream/moonlight-qt/releases/), [Android](https://play.google.com/store/apps/details?id=com.limelight), [Amazon Fire tablets and TVs](https://www.amazon.com/gp/product/B00JK4MFN2), [iOS, Apple TV](https://apps.apple.com/us/app/moonlight-game-streaming/id1000551566), [and ChromeOS devices](https://chrome.google.com/webstore/detail/moonlight-game-streaming/gemamigbbenahjlfnmlfdjhdnkpbkfjj).

The community has created unofficial ports for [PS Vita](https://github.com/xyzz/vita-moonlight/releases/), [Xbox consoles](https://apps.microsoft.com/detail/9MW1BS08ZBTH), [LG webOS TVs](https://github.com/mariotaku/moonlight-tv), and many [embedded Linux devices](https://github.com/irtimmer/moonlight-embedded/wiki/Packages).

## Is there a Moonlight web client?

No, while there is a ChromeOS app that runs on Chromebooks, there is not a pure web-based Moonlight client. The GameStream protocol requires us to use raw TCP and UDP sockets which is not currently supported in web browsers. Fortunately, there is a proposed [Direct Sockets web standard](https://github.com/WICG/raw-sockets/blob/master/docs/explainer.md) in development that could make it possible to implement a web-based Moonlight client in the future.

While we would like to offer a web-based client as an option, we believe that native apps currently provide the most feature-rich and performant clients. Optimizations like changing the display refresh rate to match the stream frame rate, communicating with gamepads that aren't natively supported by the OS or browser, and using full-screen exclusive mode for lower latency are not currently available to web apps. Web browsers are also often forced to make tradeoffs to cater to the most common use-cases at the expense of others. For example, a design tradeoff for better battery life for video playback or smoother web animations might result in an increase to rendering latency.

## Can I stream from my PC while outside my house?

Yes, for many ISPs, it's as simple as [installing the Moonlight Internet Hosting Tool on your PC](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide#automatic-configuration-recommended-for-most-users).

If your ISP doesn't provide dedicated public IP addresses, you can still [stream using ZeroTier](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide#zerotier) but the setup is slightly more complicated.

When you are streaming outside your home, we recommend that you choose a bitrate in Moonlight that is at least 1 Mbps lower than your Internet connection's upload speed. This will leave room for other upload traffic from your network to avoid disturbing your Moonlight streaming performance.

## Can I wake up my PC for streaming if it's asleep?

If you're connected to the same network as your host, it is usually possible to wake your PC with Moonlight. If it's not working, check your NIC driver and BIOS settings to ensure Wake-on-LAN is enabled.

If you're streaming from outside your home network, it is not always possible to wake your PC. Certain routers may support it, but many don't. We recommend that you leave your computer awake if you want to stream outside your home.

## Can I stream my entire desktop with Moonlight?

Yes, many Moonlight users use it as a high performance remote desktop client.

If you're using Sunshine on your host PC, you should see a "Desktop" option included out of the box. If you're using GeForce Experience, you can add an option to stream your full desktop [using these steps](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide#using-moonlight-to-stream-your-entire-desktop).

If you're using the PC client, you can also enable remote desktop mouse mode in the Moonlight settings for a seamless mouse experience when using other apps along with Moonlight.

## Can I use special input hardware like flight sticks, steering wheels, gyros, etc?

Yes, but not with Moonlight itself. GameStream only supports passing gamepad input via virtual Xbox 360 controllers to the host PC. This means special input devices connected to the Moonlight client like flight sticks, steering wheels, etc. cannot be directly passed through to the host PC.

To pass through those special devices to your host PC, we recommend [VirtualHere](https://virtualhere.com/) which can pass through 1 USB device for free, or more with the paid version.

## Is Moonlight secure?

NVIDIA GameStream uses a secure pairing process to establish trust between clients and hosts. Each Moonlight client generates a unique key which is exchanged directly with the host PC during the pairing process. This process authorizes the Moonlight client to launch games, view installed apps, etc.

Moonlight client keys are generated and stored locally on each client. We never receive your unique client keys, so there is no online account system that could possibly be compromised to gain access to your PC.

Keyboard, mouse, and gamepad data is sent back to the host PC over an encrypted connection to prevent the possibility of this data being intercepted when travelling over an insecure network. For even more security, you can use Moonlight over a VPN connection [like ZeroTier](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide#zerotier) which encrypts all traffic.

Beginning in Sunshine v0.22, full end-to-end encryption is supported. This includes all video, audio, control, and connection setup traffic. By default, full encryption is enabled for capable devices when streaming over the Internet. Encryption can be disabled or made mandatory for LAN and WAN connections independently in the Sunshine configuration.

## Where can I get help with streaming issues?

[Our Discord server](https://moonlight-stream.org/discord) is the best place to find help from Moonlight developers and the community.

## Where can I make suggestions for improvements to Moonlight?

You can [suggest improvements here](https://ideas.moonlight-stream.org). Please upvote suggestions to show your support. Only comment if you have something to add to the conversation.

Some new features will require the use of [Sunshine](https://github.com/LizardByte/Sunshine) for hosting, instead of GeForce Experience, since the latter is out of support from NVIDIA and is not receiving new feature work.

## Where can I find the Moonlight source code?

The Moonlight source code is on our [GitHub page](https://github.com/moonlight-stream).

We welcome pull requests. If you'd like to port Moonlight to a new platform, please [join our Discord server](https://moonlight-stream.org/discord). We would be happy to share our knowledge with you to help you bring Moonlight to a new platform.

## Why doesn't my audio work after I stop streaming?

This is almost always because you haven't truly ended your streaming session; you've just disconnected from it.

When you just exit the stream or close Moonlight, the session remains running on your host PC to ensure you don't lose progress in the game or application that you're streaming. This behavior also allows you to seamlessly pick up your streaming session from a totally different device without having to restart your game.

If you select your PC in Moonlight, you will see that the app you were streaming still has the Play button icon on it, which indicates the session for that app is still active.

To end your streaming session, select the running game and choose Quit App. Keep in mind that this will forcefully terminate the app on your host PC, so ensure you've saved your progress first!

## Why does my host PC resolution change to 720p when I start streaming?

GeForce Experience only officially supports 720p, 1080p, and 4K streaming resolutions. Moonlight allows users to pick resolutions to stream that aren't on that officially supported list, but these will cause GeForce Experience to set the host PC resolution to 720p when streaming starts.

This is usually not a problem, since you can configure your resolution in game to whatever you want and that will kick in when the game launches. If changing resolution in game isn't working, make sure your game is configured to use full-screen exclusive mode instead of borderless windowed mode.

You can also [stream your full desktop](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide#using-moonlight-to-stream-your-entire-desktop) which will not adjust your host PC resolution at all.

Note: This issue doesn't affect hosts using [Sunshine](https://github.com/LizardByte/Sunshine) instead of GeForce Experience.

## Why doesn't Moonlight show all of my games?

NVIDIA GeForce Experience only reports games that NVIDIA has manually validated to work correctly with GameStream, even if they otherwise appear in GeForce Experience's game list.

You can add any game manually [using these steps](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide#adding-custom-programs-that-are-not-automatically-found). 

## Why doesn't Steam show up on my Apple TV or iOS device?

To comply with [Apple App Store Review Guideline 4.2.7d](https://developer.apple.com/app-store/review/guidelines/#minimum-functionality), we cannot show the Steam app out of the box, because it features a third-party store for purchasing games.

You can manually add Steam if you would like [using these steps](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide#adding-custom-programs-that-are-not-automatically-found).

## Why can't I add a PC that isn't on my local network on my Apple TV or iOS device?

To comply with [Apple App Store Review Guideline 4.2.7a](https://developer.apple.com/app-store/review/guidelines/#minimum-functionality), we cannot allow computers to be added that aren't connected to your local network. You must add them while connected to the same network.

## Why doesn't my mouse work properly in FPS games on Android 7.1 or earlier?

Android 8.0 is the first version of Android that contains support for mouse pointer capture. Without this, mouse support is limited to games that don't utilize relative mouse motion, like RTS or simulation games.

If your device is rooted, you may try the APK named 'app-root-release.apk' on the [Moonlight Android releases page](https://github.com/moonlight-stream/moonlight-android/releases). This version of Moonlight uses root access to capture the mouse pointer on older Android devices.

## Why does my mouse move very fast on Android?

Android's mouse capture API does not allow apps to opt-out of mouse acceleration. The result is that your mouse may be accelerated twice, once by Android and once by Windows, leading to difficulty controlling the mouse.

If possible, you can disable mouse acceleration in your game as a workaround.

NVIDIA has implemented a custom method for disabling mouse acceleration on their own SHIELD Android devices. Moonlight uses this support to provide proper non-accelerated mouse support on NVIDIA Shield Android devices. Unfortunately, there is no generic solution for other Android devices.

## Why does my host's mouse acceleration change while streaming?

When GeForce Experience starts a GameStream session, it adjusts the Windows mouse acceleration and pointer speed options to some predefined settings. We don't know exactly why NVIDIA's software does this, but there is nothing Moonlight can do to opt out of it.

The adjusted mouse acceleration is not generally a problem in games, because most games disable Windows' mouse acceleration or implement their own custom mouse acceleration internally. If your mouse is misbehaving in game, look for an option to enable "raw input", disable "mouse acceleration", or similar options.

For remote desktop usage, Moonlight has a remote desktop optimized mouse mode that can be enabled in the Moonlight's input settings. In remote desktop mouse mode, your host's mouse cursor will directly track at the same position as your client's cursor. Not only does this avoid host mouse acceleration problems, but it also allows your cursor to seamlessly enter and exit the Moonlight window without having to bind and unbind your mouse. In this configuration, Moonlight behaves very similarly to Microsoft Remote Desktop or Chrome Remote Desktop.

Note: This issue doesn't affect hosts using [Sunshine](https://github.com/LizardByte/Sunshine) instead of GeForce Experience.

## Why do I see periodic stutters on macOS when streaming over WiFi?

macOS performs periodic background WiFi scans for Location and AirDrop. While the WiFi radio is scanning, it cannot send or receive traffic. The result is that video and audio data is delayed or dropped during these scans. The result is perceived as stuttering video and audio.

To minimize background scans that lead to stuttering, try disabling AirDrop and Location Services.

Other video applications like Netflix or YouTube keep a buffer of some data which smooths over these small glitches. Real-time streaming apps like Moonlight can't buffer data because it would introduce significant latency. As a result, Moonlight and other game streaming apps are much more sensitive to small glitches in your network performance.

## Why is my frame rate low when streaming my desktop on a laptop with NVIDIA Optimus?

There is extra overhead to stream the desktop when Optimus is enabled, because each frame must be copied back from the iGPU to the NVIDIA GPU for NVENC to encode it. This extra copying overhead usually results in frame rates between 25 and 40 FPS while streaming the desktop.

Once you start a full-screen game, the streaming performance should go back to normal. If it doesn't, make sure your game is set to run on the NVIDIA GPU and that your game is set to use full-screen exclusive mode instead of borderless windowed mode.

Note: This issue doesn't affect hosts using [Sunshine](https://github.com/LizardByte/Sunshine) instead of GeForce Experience.

## Why is my frame rate low when streaming static content from Sunshine?

Unlike GeForce Experience which produces a fixed frame rate encode, Sunshine uses variable frame rate encoding to match the rate of content updates on the host. That means you'll see a low frame rate (typically around 10 FPS) when streaming static content. When content on the screen starts changing, the frame rate will increase to match the frame rate of the content displayed on the host PC, up to the maximum FPS set in Moonlight.

Note: On some Android devices, this may cause the reported decoding latency numbers to be higher when content is static than it will be when actually gaming.

## Why doesn't the bitrate slider go beyond 150 Mbps?

There are a few hardware and software limitations at play.

The hardware video decoder on the client must have the capability to actually handle the video bitrate you specify. Since almost no content is produced at a bitrate above 100 Mbps, it's unlikely that the hardware decoder and driver could handle a 1 Gbps video stream even if you have a 1 Gbps network connection.

Encoders also have limitations regarding the amount of data they can encode from the source video. NVIDIA's GameStream tuning for NVENC is optimized for very fast encode times to ensure low latency. While this ensures frames are delivered to the client as fast as possible, it also limits the encoding hardware in terms of how much encoding it can do in the time window.

Finally, GeForce Experience itself also caps the bitrate that it will use for encoding, regardless of what Moonlight asks for. This is likely due to the encoding limitations above.

## How can I see on-screen statistics about my streaming performance?

On the PC client, you can press Ctrl+Alt+Shift+S to enable the stats overlay while streaming. Raspberry Pi and Steam Link do not current have overlay support, but you can see the same stats in the log file after you end your stream.

On Android and iOS, you can enable the on-screen overlay in the Moonlight settings.

## What do the numbers mean in the on-screen connection statistics?

Notes about these numbers:
- Due to limitations of the various decoding APIs available on each platform, not all latency and frame drop numbers will be available on all Moonlight clients.
- Client performance can vary significantly depending on the selected frame rate, resolution, client hardware, etc. You can tweak these settings to improve your performance.
- These numbers can't be used to compare to other non-Moonlight clients, since each value may not be measuring the same thing, despite potentially having the same name.
- There is additional system latency that can't be measured by apps (compositor latency, display latency, input device latency, etc). For the most accurate results, you should always measure using external testing hardware.

### Latency numbers
- Network latency
    - This is your "ping" time to your host - the time it takes for one packet to be sent from client -> host -> client.
    - In more concrete terms, this is the amount of network delay for user input (like a key press) to reach the host, then for the resulting video and audio from the host to reach the client.
    - Network latency usually increases as the geographic distance from your host increases.
    - Network latency can also increase if your bitrate is set higher than your connection can handle well.
    - Many cellular networks (3G, 4G/LTE, 5G) tend to have higher network latency than traditional Internet connections.
- Network latency variance
    - This measures the amount of variance between the network latency of each packet (also known as: jitter).
    - Latency variance/jitter depends on how well the connection to your host is handling the network load from streaming.
    - If this value is very high or jumps around a lot, try lowering the bitrate in Moonlight or streaming from a more stable connection.
- Decode latency
    - This is the average amount of time it takes for a frame to be decoded and ready for rendering.
    - This number varies widely depending on your client hardware, bitrate, stream frame rate, and stream resolution.
    - Increasing the frame rate to 90 or 120 FPS may decrease decode latency on some devices.
- Frame queue latency
    - This is the average amount of time that frames wait to be rendered after decoding. The wait is usually because the previous frame is still being rendered or waiting for V-Sync.
    - It should usually stay under a frame interval (16 ms for 60 FPS), but in rare cases, driver issues can cause it to rise significantly if rendering is not progressing at the normal rate.
- Render latency
    - This is the average amount of time it takes for a decoded frame to be rendered to the display.
    - If you have V-Sync enabled, this will typically include a V-sync period (16 ms for a 60 Hz display) in addition to the actual render latency. This is because Moonlight must wait for V-Sync to render.

### Frame drop numbers
- Frames dropped by network connection
    - This indicates the percentage of frames that are sent from the host and don't successfully reach the client. It should stay very close to 0% most of the time.
    - High values indicate an unreliable network connection (like 2.4 GHz WiFi or powerline networking) or that your connection is not capable of streaming at the bitrate settings you've chosen.
- Frames dropped due to network jitter
    - This indicates the percentage of frames dropped because they are too early or too late to render.
    - Rather than coming at a smooth 16ms-16ms-16ms-16ms... for each frame, network variance may cause patterns like 20ms-12ms-18ms-14ms... which forces Moonlight to skip or drop frames to stay in sync with the client display.
    - It is typically caused by high network jitter but it can also be caused by hardware limitations or software issues (especially if very high).

## What do the frame pacing options on the Android client mean?

- Prefer lowest latency
    - Renders a frame immediately after it has been decoded (dropping the last frame if it hasn't been displayed yet)
    - Keeps the display refresh rate as high as possible
- Balanced (recommended)
    - Uses a [Choreographer frame callback](https://developer.android.com/reference/android/view/Choreographer.FrameCallback) to render when the next frame is due
    - Up to 1 frame is buffered to smooth over network jitter and v-sync drift between host and client
- Balanced with FPS limit
    - Limits the FPS value to the display refresh rate - 1 and never drops frames
    - If FPS > display refresh rate, it will behave like Balanced
    - Devices with variable refresh rate displays may have issues with this pacing method due to fluctuations in display refresh rate
    - This was the default frame pacing behavior before v10.0
- Prefer smoothest video
    - Never drops frames, even if the frame rate is equal or higher than the display
    - Frames queue up until they hit an OS-defined limit, potentially leading to very high latency