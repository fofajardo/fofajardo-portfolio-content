---
tags: 
  - "personal"
  - "packages"
title: "rtl8851bu"
subtitle: "Modified and updated version of Realtek RTL8851BU Wi-Fi USB Driver for Linux"
dateStart: "2024-11"
technologies: 
  - "c"
  - "linux"
points: []
preview: "16"
links: 
  - type: "github"
    url: "https://github.com/fofajardo/rtl8851bu"
hasBody: true
---

This repository hosts a modified and updated version of the Realtek RTL8851BU Wi-Fi driver for Linux. It is primarily tested on Arch Linux with a [COMFAST CF-943AX](https://www.alibaba.com/product-detail/COMFAST-RTL8851BU-Wireless-BT-Adapter-Dongle_1601014889255.html), but users of other distributions are welcome to contribute and report their experiences.

#### Features
- Supports **IEEE 802.11 b/g/n/ac/ax**
- Implements **WPA3-SAE R3** security
- **Soft AP mode**, **WiFi-Direct**, and **Miracast** support
- **WOWLAN** (Wake on Wireless LAN)
- **Bluetooth coexistence (BT-COEXIST)**
- Site survey scanning and manual connection
- **WPS** - PIN and PBC Methods

#### Supported Platforms
- **Linux Kernel Versions:** 3.13 to 6.13
- **CPU Architectures:** x86, ARM, MIPS

#### Acknowledgments
This project is based on Realtek's official driver release **v1.19.10-78-gfbe3fba11.20240422**.

#### Disclaimer
This project is maintained by independent developers and is not affiliated with, endorsed by, or supported by Realtek Corporation. The maintainers are not employees of Realtek.
