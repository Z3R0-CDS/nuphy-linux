# nuphy-linux
 Fix browser (VIA) not able to connect to nuphy
 
# Nuphy udev rules

Welcome to the GitHub repository for the Nuphy udev rules! This repository contains the essential udev rules needed to ensure compatibility and proper permissions for nuphy hardware. These rules are particularly designed to work seamlessly with the VIA web application at [usevia.app](https://usevia.app/).

## Overview

Udev is a device manager for the Linux kernel, which dynamically creates or removes device nodes in the `/dev` directory. For the nuphy keyboards, specific udev rules are required to set the correct permissions, allowing applications like [usevia.app](https://usevia.app/) to interact with them without needing root privileges.

This repository provides the necessary udev rules to facilitate this interaction, ensuring a smooth and secure experience for users of Nupy Keyboards on Linux systems.

I cannot gurantee or verify if all devices will work because I do not own all of them (Why should I?!). But using the json files from the offficial site I do have the IDs they used. So should work right?
In the worst case open an issue and let me know.

## Supported devices
Tested:
-  Nuphy Air96 v2

Untested (Should work I dont have one tho):
-  Nuphy Air75 v2
-  Nuphy Air60 v2
-  NuPhy Gem80
-  NuPhy Halo75
-  NuPhy Halo96
-  NuPhy Nos75

## Installation

### Prerequisites

- A Linux-based operating system.
- A supported Nuphy device.

### Steps

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/Z3R0-CDS/nuphy-linux
   ```
   
2. **Navigate to the Repository:**
   ```bash
   cd nuphy-linux
   ```

3. **Copy the Udev Rule:**
   ```bash
   sudo cp nuphy.rules /etc/udev/rules.d/
   ```

4. **Reload Udev Rules:**
   ```bash
   sudo udevadm control --reload-rules && sudo udevadm trigger
   ```

5. **Verify Installation:**
   Connect your Nuphy device and verify if it's detected correctly by the [via](https://usevia.app/) application.
   Make sure to follow the guide of the [Official website](https://nuphy.com/pages/via-usage-guide-for-nuphy-keyboards) to ensure its working as intended.
   Also keep in mind it might be required to reopen the browser or try in a private tab if you attempted to use via before.
   I had some cached issues with the permissions at first and testing in a private tab helped.

## Usage

Once installed, the udev rules will automatically set the correct permissions for your Nuphy Device.
This allows the [via](https://usevia.app/) web application to detect and interact with your device without requiring additional configurations.

---

For more information or support, open an issue in this repository. I will try to respond asap

## Create a rule yourself.

### Commands

1. **Get a list of usb devices.**
   ```bash
   lsusb
   ```
2. **Get data of your device.**
   ```
   Bus 005 Device 007: ID 19f5:3265 NuPhy NuPhy Air96 V2 <- Example output for my nuphy
                              ^ 
                            These are the vendor ID and device ID
   Vendor will be 19f5 because nuphy is nuphy.
   ```
3. **Create a rule.**
   ```
    <notepad app(kate)> nuphy-<something>.rules
    Enter the rules:
    SUBSYSTEM=="usb", ENV{DEVTYPE}=="usb_device", ATTR{idVendor}=="<vendorID>", ATTR{idProduct}=="<deviceID>", MODE="0666"
    
    KERNEL=="hidraw*", ATTRS{idVendor}=="<vendorID>", ATTRS{idProduct}=="<deviceID>", MODE="0666"
   ```
4. **Create a rule.**
   Then just copy and apply as above.
   Also sharing is caring so open a merge request.

