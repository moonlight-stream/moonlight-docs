This FAQ page covers frequently asked questions about [NVIDIA's GameStream End of Service Notification](https://nvidia.custhelp.com/app/answers/detail/a_id/5436).

# What is happening?
In late 2022, NVIDIA announced that they have chosen to discontinue their NVIDIA GameStream technology.

You can read NVIDIA's official announcement [here](https://nvidia.custhelp.com/app/answers/detail/a_id/5436).

# Why does NVIDIA's announcement impact Moonlight?

The Moonlight project implements unofficial open-source clients for NVIDIA GameStream. The host software that Moonlight connects to is part of NVIDIA GeForce Experience, so it is under NVIDIA's control and depends on their ongoing effort to fix bugs and implement new host-side features.

While NVIDIA's announcement is primarily centered around the removal of GameStream support from their official NVIDIA Games client, it's highly unlikely that they would continue to invest maintenance resources in the host software when no official clients exist.

**2024 Update:** NVIDIA has announced that GeForce Experience itself will be discontinued in favor of their new [NVIDIA app](https://www.nvidia.com/en-us/software/nvidia-app/) which is currently in beta. This new NVIDIA app does not support GameStream and installing it will remove GeForce Experience. 

# What does this mean for Moonlight?

In the short term, nothing. Moonlight will continue to be usable with host PCs running the latest version of GeForce Experience until at least mid-Feburary 2023, according to NVIDIA's announcement.

Inline with our long-term goal of providing an excellent open-source game streaming solution, we have increased our efforts to improve [the Sunshine project](https://github.com/LizardByte/Sunshine), which acts as an a free open-source host for Moonlight. 

Sunshine now supports many features that were never possible with GeForce Experience, including:
- Support for AMD, Intel, and NVIDIA GPUs
- Full DualShock controller emulation, including motion sensors, touchpad, and light bar control
- AV1 encoding for higher quality than HEVC or H.264 codecs
- Built-in support for hosting on the Internet without requiring [a separate tool](https://github.com/moonlight-stream/Internet-Hosting-Tool)
- Built-in support for IPv6 without requiring [a separate tool](https://github.com/moonlight-stream/GS-IPv6-Forwarder)
- Host capture/encoding latency reporting that appears in Moonlight's on-screen performance overlay

By investing our time in making Sunshine a top-tier game streaming host, we can ensure that the whims of a single company cannot unilaterally impact the game streaming community again.

# What will happen to Moonlight in mid-February?

Past mid-February 2023, the status of the hosting GeForce Experience is unclear. It's likely that the GameStream functionality will be present in GeForce Experience for a little longer, since major GeForce Experience updates don't arrive very often.

Even when the functionality is removed in GeForce Experience, it is likely that GameStream can still be used by running older versions of GeForce Experience (and blocking the automatic update mechanism). This might also require older GPU drivers, but historically older GeForce Experience versions and GameStream have been compatible with newer drivers without issue.

Because GeForce Experience contains a list of GameStream-supported GPUs, it is likely that GPUs launched after mid-February will not be usable for GameStream, even running older versions of GeForce Experience.

**2024 Update:** NVIDIA has announced that GeForce Experience will be discontinued in favor of their new [NVIDIA app](https://www.nvidia.com/en-us/software/nvidia-app/) which is currently in beta. This new NVIDIA app does not support GameStream and installing it will remove GeForce Experience. 

# How will Moonlight change after GameStream support is removed from GeForce Experience?

That will depend on how the removal works in practice and what our users want.

While the performance and capabilities of GameStream in GeForce Experience was excellent, it did limit our capabilities in some ways. For example, microphone support was implemented for GeForce Now but never for GameStream. Similarly, major features like PS4 or Xbox One controller emulation, trigger rumble support, client-side cursor rendering, and AV1 encoding support were not possible due to host and GameStream protocol limitations. Now that we no longer have to worry about introducing compatibility issues with future versions of GameStream, we can implement features like these in Sunshine.

In any case, it is unlikely that we will remove support for streaming from GeForce Experience for the foreseeable future.

# Was the Moonlight team given advance notice of this?

No, we found out when the public announcement was made.

While it would have been nice to know in advance, it's completely understandable that NVIDIA did not do so. We have no official relationship or agreement with NVIDIA, so there is no NDA in place or anything that would provide legal protection for them that we wouldn't leak the news to the media (though we would certainly not have done so, even in the absence of such an agreement).