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

# System Specs

Category | Description
:-------:|------------
**Model** | Lenovo ThinkPad X1 Carbon Gen 7
**Variant** | [**20R2**](https://psref.lenovo.com/syspool/Sys/PDF/ThinkPad/ThinkPad_X1_Carbon_7th_Gen/ThinkPad_X1_Carbon_7th_Gen_Spec.pdf)
**CPU** | Intel [**Intel Core i7-10710U**](https://www.intel.com/content/www/us/en/products/sku/196448/intel-core-i710710u-processor-12m-cache-up-to-4-70-ghz/specifications.html) (Hexa Core)
**RAM** | Soldered 16 GB DDR4 @2133 Mhz
**Storage** | Teamgroup TM8FP6512G
**Display** | Full HD (1080p) (Non-Touch with ThinkPad Privacy Guard )
**iGPU** | Intel(R) Grpahics UHD 620
**Audio** | [**Realtek ALC285**](https://github.com/dreamwhite/ChonkyAppleALC-Build/blob/master/Realtek/ALC285.md) (using Layout `71`)
**Thunderbolt** | Alpine Ridge 4C 2016
**Ethernet** | Intel I219-V
**WiFi** | Intel AC-9560 <br> **Firmware**: [**`iwm-9000-46`**](https://www.intel.com/content/www/us/en/support/articles/000005511/wireless.html)
**Bluetooth** | **Device**: Intel Wireless Bluetooth <br> **BT Version**: 5.1 <br> **VID**: `0x8087`, **PID**: `0x0aaa` <br> **Firmware**: `ibt-17-16-1.sfi`, `ibt17-16-1.ddc` <br>**USB Port**: `HS10`
**Trackpad** | Synaptics <br>**Device-id**: `pci8086,9de8`. Controlled via I2C.
**USB-C Display w/ Hub** | [**Dell UltraSharp U2723QE**](https://www.dell.com/en-us/shop/dell-ultrasharp-27-4k-usb-c-hub-monitor-u2723qe/apd/210-bdpf/monitors-monitor-accessories)

---

# BIOS Settings
After powering on the machine, spam <kbd>F1</kbd> until you hear a beep to enter the BIOS. Change the following settings:

Category | Setting
:-------:|------------
**Config** | **Display** <ul> <li>Shared Display Priority: `HDMI` <li> Total Graphics Memory: irrelevant for macOS </ul> **CPU** <ul> <li> Intel Hyperthreading Technology: `ON` 
**Security** | **Fingerprint** <ul><li>Predesktop Authentication: `OFF` </ul> **Security Chip** <ul><li>Security Chip`ON` or `OFF` (enable for Windows 11) </ul> **Memory Protection** <ul> <li> Execution Prevention: `ON`</ul></ul> **Virtualization** <ul><li> Kernel DMA Protection: `ON` (enables `VT-D` by design)</ul> **I/O Port Access** <ul> <li> Ethernet LAN: `ON` <li> Wireless LAN: `ON` <li> Bluetooth: `ON` <li> USB Port: `ON` <li> Memory Card Slot: `ON` <li> Smart Card Slot: `OFF` <li> Integrated Camera: `ON` <li> Integrated Audio: `ON` <li> Microphone: `ON` <li> Fingerprint Reader: `ON` (works in Windows only) or `OFF` <li> Thunderbolt 3: `ON` </ul> **Absolute Persistance Module** <ul><li> Absolute Persistance Module Activation: `Disabled`</ul> **Secure Boot Configuration** <ul><li> Secure Boot: `OFF` </ul> **Intel SGX** <ul><li> Intel SGX Control: `Disabled`
**Startup** | <ul> <li> **UEFI/ Legacy Boot**: `UEFI Only` <li> **Boot Mode**: `Quick` (Skips Diagnostics)

---

# Feature Details

### Graphics
Fully working graphics acceleration with `WhateverGreen.kext` & `AAPL,ig-platform-id` = 00009B3E & `device-id` = 9B3E0000
| Displays                             | Status | Connector, BusID, Port Type          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| Internal Display | ✴️ | `con0`, BusID `0x00`, type `LVDS` | Screen garbled/glitching if HDMI/1st USB-C plugged in on cold boot. If you encounter the glitch, TURN OFF YOUR LAPTOP IMMEDIATELY to avoid damaging your display! |
| HDMI 1.4 | ✴️ | `con1`, BusID `0x01`, type `HDMI` | It only works properly after being put to sleep and woken up once (Hotplug & 4K resolution are supported, with notes below) |
| 1st USB-C (Display output) | ✴️ | `con1`, BusID `0x01`, type `HDMI` | It only works properly after being put to sleep and woken up once (Hotplug & 4K resolution are supported, with notes below) |
| 2nd USB-C (Display output) | ✅ | `con2`, BusID `0x02`, type `HDMI` | It works properly (Hotplug is supported on cold boot) |
| DRM | ❌ | iGPU | DRM is broken with iGPUs |

> [!NOTE]
> - 1st USB-C and HDMI 1.4 shared its connector (using `con1`). I learned that if you plug your display into 1st USB-C, the HDMI port not working until the next reboot!
> - I think to make DisplayPort on both USB-C ports working, Thunderbolt must working too. As long as it not working, it will be driven by HDMI Protocol, even System Profiler says the output is `DisplayPort/Thunderbolt` and `framebuffer-conX-type` set to `DisplayPort`

### Audio
Works with `AppleALC.kext` and `LayoutID=71`
| Feature                              | Status | Remarks                      |
| :----------------------------------- | ------ | ---------------------------- |
| Internal Speakers | ✅ | You have to manually aggregate the two output using "Audio MIDI Setup" to have 4 speakers working |
| Internal Microphone | ❌ | Unsupported by AppleALC, see known issues. |
| Headphone Jack Output | ✴️ |  Output sometimes inconsistent, fixed by replugging. Output switching works |
| Headphone Jack Input | ✴️ | Input sometimes inconsistent, fixed by replugging. Input switching works |

### Power Management
| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| Battery | ✅ | `ECEnabler.kext` | - |
| CPU Power Management (SpeedShift) | ✅ | `CPUFriend.kext` with `CPUFriendDataProvider.kext` Don't forget to create yours yourself | - |
| iGPU Power Management | ✅ | `WhateverGreen.kext` | Apple GuC Firmware enabled by `igfxfw=0x02` |
| NVMe Drive Battery Management | ✅ | `NVMeFix.kext` | Improves NVMe drive power management |
| S3 Sleep / Hibernation Mode 3 | ✅ | - | - |

### Connectivity
| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| WiFi | ✅ | `AirportIltwm.kext` | - |
| Bluetooth | ✅ | `IntelBluetoothFirmware.kext`, `BlueToolFixup.kext`, and `USBMap.kext` | BTLE devices won't pair and headset's microphone is not working via Bluetooth |
| Ethernet | ✅ | `IntelMausi.kext` | - |
| Wireless WAN | ❌ | `DISABLED` in BIOS to save power. | Unable to investigate as I have no need and my model did not come with WWAN |
| USB 2.0 / USB 3.0 | ✅ | `USBMap.kext` | Create your own USBMap.kext using [CorpNewt](https://github.com/corpnewt/USBMap) |
| USB 3.1 (Type-C) | ✅ | `USBMap.kext` and enable Thunderbolt 3 in `BIOS` | Hotplug is working |
| Thunderbolt 3 | ✴️ | - | Ongoing research as there's a way to enable Thunderbolt in Alpine Ridge platform |

### Input/Output
| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| Built-in Keyboard | ✅ | `VoodooPS2Controller.kext` | - |
| Brightness Adjustments | ✅ | `BrightnessKeys.kext`| - |
| Hotkeys | ✅ | 5T33Z0's `SSDT-T490-KBD.aml`| - |
| Trackpoint | ✅ | `VoodooPS2Controller.kext` | - |
| Trackpad | ✅ | `VoodooI2C.kext` and `VoodooI2CHID.kext` | - |
| Fingerprint Reader | ❌ | - | Will never work |
| Webcam | ✅ | `USBMap.kext` | - |

### macOS Features
| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| iCloud, iMessage, FaceTime | ✅ | Whitelisted Apple ID, Valid SMBIOS See [Dortania / OpenCore-Install-Guide](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html) | Works as long as Ethernet detected as `en0` |
| Wired Sidecar | ✅ | - | Tested with iPad Pro (2018) with USB-C to USB-C cable |
| Handoff | ✅ | - | Works everytime I use Handoff supported apps  |
| Instant Hotspot | ❌ | - | Detects but won't connect |
| Continuity Camera | ❌ | - | Not working with Intel wireless cards |
| AirDrop | ❌ | - | Not working with Intel wireless cards |
| Apple Watch Auto Unlock | ❌ | - | Not working with Intel wireless cards |
| Wireless Sidecar | ❌ | - | Not working with Intel wireless cards |
| Continuity Markup and Sketch | ❌ | - | Not working with Intel wireless cards |
| Universal Clipboard | ❌ | - | Support dropped with macOS Sonoma and the new AirportIltwm kext |
| SMS & Phone Call via iPhone | ❌ | - | Support dropped with macOS Sonoma and the new AirportIltwm kext |
| AirPlay to Mac | ❌ | - | Support dropped with macOS Sonoma and the new AirportIltwm kext |
| FireVault 2 | ❓ | - | Untested because I don't like macOS encrypting my drive |

### Miscellaneous
| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| Multiple Boot | ✅ | - | macOS & Windows. As I don't like OpenCore to inject DSDT's to Windows, I use rEFInd to pick the Windows Boot Manager/OpenCore |
| YogaSMC | ❌ | `YogaSMC.kext` | I disabled YogaSMC because of some performance issues after multiple sleep and wakes. Also, the DYTC function not working on Sonoma+. Hotkeys function superseeded by `SSDT-T490-KBD.aml` although I lose functionality to enable the Privacy Screen Guard |
| OpenCore Boot chime | ✅ | - | Working like a charm! |

