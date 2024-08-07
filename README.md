# nuphy-linux
 Fix browser (VIA) not able to connect to nuphy
 
# Nuphy udev rules

Welcome to the GitHub repository for the Nuphy Air96 udev rules! This repository contains the essential udev rules needed to ensure compatibility and proper permissions for the nuphy air 96. These rules are particularly designed to work seamlessly with the VIA web application at [usevia.app](https://usevia.app/).

## Overview

Udev is a device manager for the Linux kernel, which dynamically creates or removes device nodes in the `/dev` directory. For the nuphy air 96, specific udev rules are required to set the correct permissions, allowing applications like [usevia.app](https://usevia.app/) to interact with them without needing root privileges.

This repository provides the necessary udev rules to facilitate this interaction, ensuring a smooth and secure experience for users of Nupy Air96 on Linux systems.
I do not support other nuphys because I don't own one and don't know the id's feel free to open merge requests if you own them.

## Installation

### Prerequisites

- A Linux-based operating system.
- A Nuphy air96.

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
   sudo cp nuphy-air96.rules /etc/udev/rules.d/
   ```

4. **Reload Udev Rules:**
   ```bash
   sudo udevadm control --reload-rules && sudo udevadm trigger
   ```

5. **Verify Installation:**
   Connect your Nuphy device and verify if it's detected correctly by the [via](https://usevia.app/) application.
   Make sure to follow the guide of the [Official website](https://nuphy.com/pages/via-usage-guide-for-nuphy-keyboards) to ensure its working as intended.

## Usage

Once installed, the udev rules will automatically set the correct permissions for your Nuphy Air96.
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

