# ProtonOS

```text
==================================================
 ProtonOS Kernel v1.0.0 (XNU-Darwin ARM64 Custom) 
 Target Hardware: Samsung SM-T510 (Exynos 7904)   
 Compiled by: Clanker AI & Dev Team              
==================================================
```

An experimental, open-source research project aimed at patching and compiling Apple's open-source **XNU (Darwin) kernel** to boot a native, Wi-Fi-only iOS/iPadOS 16 userland layer directly on the **Samsung Galaxy Tab A 10.1 (2019) [SM-T510]**.

Inspired directly by pioneering low-level community milestones like *HakiOS*, *Bergamota*, and the *iOS-Galaxy-S8* porting projects.

---

## 🎯 The Core Strategy
Because the Samsung Galaxy Tab A 10.1 is a **Wi-Fi-only tablet**, ProtonOS targets the system profile and architecture definitions of matching Wi-Fi-only Apple iPad variants (such as the iPad 6th Generation running 2GB RAM / 32GB Storage configurations). 

By explicitly choosing a Wi-Fi-only software footprint, the project completely drops cellular baseband, telephony layers, and RIL complexities, focusing strictly on bringing up fundamental core hardware blocks.

---

## 🛠 Hardware Mapping & Targets

| Component | Target Device (SM-T510) | Architecture Strategy | Status |
| :--- | :--- | :--- | :--- |
| **Processor** | Exynos 7904 (Octa-Core ARM64) | Porting custom Apple Device Tree registers | 🔄 Researching |
| **Bootloader**| Samsung S-Boot -> Custom Shim | Flat physical EL2/EL1 memory reset via assembly | 💻 Coding |
| **Storage**   | eMMC 5.1 Flash Controller | Custom XNU kernel block-device storage wrapper | 🔄 Researching |
| **Wireless**  | Broadcom BCM43438 Combo Chip | Leveraging native iPadOS Broadcom support via SDIO | 💻 Coding |
| **Graphics**  | ARM Mali-G71 MP2 | Software-mapped low-level linear memory framebuffer | 💻 Coding |

---

## 📂 Source Tree Overview

*   `/arch/arm64/start.S`: Low-level assembly entry-point that masks interrupts, drops execution levels, clears Android TLBs, and configures hardware registers to match basic Apple SoC environments.
*   `/include/protonos_version.h`: Core OS identity banner, version strings, and the model identification engine used to spoof incoming iPadOS system binaries.
*   `/drivers/ProtonOSBroadcomWiFi.c`: Custom kernel layer mapping the Exynos 7904 SDIO interface parameters to wake up and feed configuration blobs to the Broadcom wireless module.
*   `/drivers/ProtonOS_Mali_FB.c`: Flat display pipeline framework handling 32-bit pixel mapping configured directly to the tablet's native 1200 x 1920 panel dimensions.

---

## ⚠️ Disclaimer & Current Project State
**ProtonOS is a highly experimental developer proof-of-concept.** 
* It is **not** a daily-driver operating system.
* It does **not** bypass Apple activation locks, nor does it connect to proprietary Apple cloud infrastructure (iCloud, iMessage, and FaceTime are completely unreachable due to physical cryptographic constraints).
* Flashing custom shims or messing with deep boot partitions carries a high risk of hard-bricking your tablet. Proceed at your own structural risk.

---
*Built with absolute dedication to the open-source mobile reverse-engineering movement.*
