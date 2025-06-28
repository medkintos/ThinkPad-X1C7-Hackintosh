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

This X1C7 Hackintosh project aims to be an all-in-one maintained hub for OpenCore based hackintoshes on the Thinkad X1 Carbon Gen 7. In short, this X1C7-Hackintosh is very stable and is currently my daily driver. I fully recommend this project to anyone looking for a MacBook alternative.

You can find a wealth of knowledge on [Reddit](https://www.reddit.com/r/hackintosh/), [TonyMacX86](https://www.tonymacx86.com) or [Google](https://www.google.com).

**Important:** If you are upgrading to macOS 14.4+ you have to set the value of `Misc -> Security -> SecureBootModel` to `Disabled` in config.plist and disable AirportItlwm kext untill the upgrade finishes and then use "AirportItlwm_v2.3.0_stable_Sonoma14.4.kext".

Should you find an error, or improve anything, be it in the config itself or in the my documentation, please consider opening an issue or a pull request to contribute.

**I am not responsible for any damages you may cause.**
