# macOS on Lenovo ThinkPad X1 Carbon Gen 7 (20R2)

OpenCore-based EFI for Lenovo ThinkPad X1 Carbon 7th Generation | Model 20R2
<img align="right" src="https://raw.githubusercontent.com/medkintos/ThinkPad-X1C7-Hackintosh/main/Docs/X1C8.png" alt="Lenovo ThinkPad X1 Carbon Gen 8" width="460">

**Status: Stable | Daily driver**

[![macOS](https://img.shields.io/badge/macOS-Sequoia-green.svg)](https://www.apple.com/macos/sequoia/)
[![Version](https://img.shields.io/badge/15.5-green.svg)](https://support.apple.com/en-us/120283)
[![OpenCore](https://img.shields.io/badge/OpenCore-1.0.4-blue.svg)](https://github.com/acidanthera/OpenCorePkg/releases/tag/1.0.4)
[![Model](https://img.shields.io/badge/Model-20R2-red)](https://psref.lenovo.com/syspool/Sys/PDF/ThinkPad/ThinkPad_X1_Carbon_7th_Gen/ThinkPad_X1_Carbon_7th_Gen_Spec.pdf)

This repo is based from [HJebbour's ThinkPad-X1C8-Hackintosh](https://github.com/HJebbour/ThinkPad-X1C8-Hackintosh/tree/main) and forked from several Comet Lake/Whiskey Lake based ThinkPad Hackintosh repositories (See **OTHER REPOSITORIES**)

**DISCLAIMER:**
As you embark on your Hackintosh journey you are encouraged to **READ** the entire README and [Dortania](https://dortania.github.io/getting-started/) guides before you start.

This X1C7 Hackintosh project aims to be an all-in-one maintained hub for OpenCore based hackintoshes on the Thinkad X1 Carbon Gen 7.

This is my last hurrah on doing Hackintosh since 10.5 Leopard days, and the one that I always avoid: doing Hackintosh on laptops. The last Intel based MacBooks sucks, and my M3 Max MacBook Pro too heavy to carry. So i bought the X1 Carbon to create the perfect and light Intel based MacBook that I'll love to use

This build suprisingly very stable with some minor caveats, and currently is my daily driver for some office work. I fully recommentd this project to anyone looking dor a MacBook alternative.

You can find a wealth of knowledge on [Reddit](https://www.reddit.com/r/hackintosh/), [TonyMacX86](https://www.tonymacx86.com) or [Google](https://www.google.com).

Should you find an error, or improve anything, be it in the config itself or in the my documentation, please consider opening an issue or a pull request to contribute.

**I am not responsible for any damages you may cause.**

---

WIP for ToC

---

# About
OpenCore EFI folder and config for running macOS Sonoma and newer on the Lenovo ThinkPad X1 Carbon Gen 7. Read the following documentation carefully in order to install/boot macOS successfully!

### Before you begin
⚠️ The built-in Samsung PM981a NVMe that comes with the system is NOT compatible with macOS. You _must_ use a different NVMe!

⚠️ If your X1 Carbon equipped with i7-10710U (like mine), don't forget to add these CPU Mask on `Kernel/Emulate`:
Key | Value
-------|------------
`Cpuid1Data` | `EC060800 00000000 00000000 00000000`
`Cpuid1Mask` | `FFFFFFFF 00000000 00000000 00000000`

### Notable Features
- [x] Compatible with macOS Sonoma and Sequoia (sorry, no support for macOS older than that)
- [x] USB Port Mapping with support for USB-C Monitor HUB/Docking Station 
- [x] Optimized Framebuffer Patch for smoother handshake with external displays via HDMI with 4K 30hz working
- [x] Working clamshell mode (when connected to A/C and external display and USB-C Display)
- [x] YogaSMC-free build based on 5T33Z0's DSDT T490 patches

### Known Issues
- [ ] Hibernation Mode 25 does not work properly
- [ ] Fingerprint sensor does not work under macOS since there is currently no way to emulate Touch ID.
- [ ] The internal mic isn't working because [AppleALC doesn't support Intel DMIC microphone setup](https://github.com/acidanthera/bugtracker/issues/2084)
- [ ] HDMI hotplug works properly after being put to sleep and woken up once. Internal screen will garbled if hotplug initiated before sleep.

> [!IMPORTANT]
> 
> - Before reporting any issues, ensure that your system uses the latest available UEFI and EC Firmware.
> - Don't install macOS on an external disk or flash drive – use a compatible internal disk.

### Future Developments
- [ ] Optimizing framebuffer patch to make HDMI Hotplug to work on cold boot
- [ ] Working Thunderbolt 3

---

# Feature Details

### Graphics
| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| Full Graphics Accleration (QE/CI) | ✅ | `WhateverGreen.kext` & `AAPL,ig-platform-id` = 00009B3E & `device-id` = 9B3E0000 | - |
| HDMI 1.4 | ✅ | `con1`, BusID `0x01` | It only works properly after being put to sleep and woken up once (Hotplug & 4K resolution are supported, with notes below) |
| 1st USB-C (Display output) | ✅ | `con1`, BusID `0x01` | It only works properly after being put to sleep and woken up once (Hotplug & 4K resolution are supported, with notes below) |
| 2nd USB-C (Display output) | ✅ | `con2`, BusID `0x02` | It works properly (Hotplug is supported on cold boot) |

> [!NOTE]
> - 1st USB-C and HDMI 1.4 shared its connector (using `con1`). I learned that if you plug your display into 1st USB-C, the HDMI port not working until the next reboot!
> - I think to make DisplayPort on both USB-C ports working, Thunderbolt must working too. As long as it not working, it will be driven by HDMI Protocol, even System Profiler says the output is `DisplayPort/Thunderbolt`

### Audio
| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| Audio Output | ✅ | `AppleALC.kext` with Layout ID = 71 | - |
| Audio Speakers | ✅ | `AppleALC.kext` with Layout ID = 71 | You have to manually aggregate the two output using "Audio MIDI Setup" to have 4 speakers working |
| Audio Input | ✅ | `AppleALC.kext` with Layout ID = 71 | Headset microphone is inconsistent and needs more testing |
| Automatic Headphone Output Switching | ✅ | `AppleALC.kext` with Layout ID = 71 | - |
