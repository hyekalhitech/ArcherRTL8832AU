# ArcherRTL8832AU
TP Link Archer TX20 Plus (Wifi 6) Driver and added custom patch to make it work on latest Linux distro. 
# Equine Tracker

![Logo](hyekalhitech.png)

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![GitHub Stars](https://img.shields.io/github/stars/yourusername/equine-tracker)](https://github.com/yourusername/equine-tracker/stargazers)
[![GitHub Forks](https://img.shields.io/github/forks/yourusername/equine-tracker)](https://github.com/yourusername/equine-tracker/network/members)
[![GitHub Issues](https://img.shields.io/github/issues/yourusername/equine-tracker)](https://github.com/yourusername/equine-tracker/issues)
[![GitHub Pull Requests](https://img.shields.io/github/issues-pr/yourusername/equine-tracker)](https://github.com/yourusername/equine-tracker/pulls)

## Table of Contents

1. [Introduction](#introduction)
2. [Special Thanks](#Special)
3. [Installation](#Installation)
4. [License](#license)
5. [Acknowledgments](#acknowledgments)

## Introduction

TP Link Archer TX20 Plus (Wifi 6) use Realtek 8832AU Chipset which is NOT a In-Linux Driver supported in the latest Linux Kernel. In order to make it work, we have to use an another driver which is NOT the 8832AU but its worked on the most Linux systems.

## Special Thanks To the Developer and the contributor who ACTUALLY make this works !

Equine Tracker comes with a wide range of features tailored for horse care:

- **<a href="https://github.com/lwfinger">lwfinger</a></p>**   : For Creating The Driver On Linux
- **<a href="https://github.com/dovandung">dovandung</a></p>** : For Sharing the line code that need to change (To make Injection mode Working!).
- **<a href="https://github.com/JeCuRoz">JeCuRoz</a></p>**     : For sharing the injection code patch !

For a detailed guide on using these features, refer to our [User Manual](docs/user-manual.md).

## Installation Guide

Step 1, Update & Install

Requirements
You will need to install "make", "gcc", "kernel headers", "kernel build essentials", and "git".

Clone the repository:

   ```bash
   sudo apt-get upgrade
   sudo apt-get install make gcc linux-headers-$(uname -r) build-essential git
   ```

If any of the packages above are not found check if your distro installs them like that.

Step 2, Downloading the driver

For all distros:

```bash
git clone https://github.com/lwfinger/rtl8852au.git
```

Step 3, Downloading the patch (Packet Injection is working)

```bash
git clone https://github.com/hyekalhitech/ArcherRTL8832AU.git
```

Step 4, Rename the patch file.
If you're already download the patch file, you may notice that got 2 different file in there, you have to rename the files by removing the "patch_"

1. patch_drv_conf.h
2. patch_rtw_xmit.c

Rename to :-

1. drv_conf.h
2. rtw_xmit.c

Step 5, move the patch files into the downloaded driver directory.

```bash
mv drv_conf.h /rtl8852au/core/
mv rtw_xmit.c /rtl8852au/include/
```
Step 6, Build & Install the driver

When a USB device is plugged in, or detected at boot, this rule causes the utulity
usb_modeswitch to unload any 0bda:1a2b devices that it finds. If you have a
device with different ID, change the rule accordingly.

The build this driver, do the following:

For all distros:
```bash
git clone https://github.com/lwfinger/rtl8852au.git
cd rtl8852au
make
sudo make install

When you get a new kernel, you will need to rebuild the driver. Do the following:
cd rtl8852au
git pull
make
sudo make install
```
Step 7, Unplug and plug back the TP-Link device (For Live Usb) OR Reboot (Installed Host)

Step 8, check the interface.
```bash
sudo airmon-ng
```
Step 9, test monitor mode
```bash
sudo airmon-ng start <interfacename>
```


Step 10, Test packet injection
```bash
sudo aireplay-ng --test <interfacename>
```
## License

refer to the [LICENSE](LICENSE) file.

## Acknowledgments

I would like to thank you to the developer and the contributors for sharing their valuable knowledge and sharing the info.

## Updated on 03/01/2024 ##