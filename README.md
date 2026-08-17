# nuphy-linux
 Fixes connectivity issues for nuphy keyboards, under linux devices using udev, in browsers. For apps like ( [usevia.app](https://usevia.app/) or even [nuphy.io](https://www.drive.nuphy.io/) )
 
# Nuphy udev rules

Welcome to the GitHub repository for the Nuphy udev rules! This repository contains the essential udev rules needed to ensure compatibility and proper permissions for nuphy hardware. These rules are particularly designed to work seamlessly with the VIA web application at [usevia.app](https://usevia.app/) or even [nuphy.io](https://www.drive.nuphy.io/).

## Overview

Udev is a device manager for the Linux kernel, which dynamically creates or removes device nodes in the `/dev` directory. For the nuphy keyboards, specific udev rules are required to set the correct permissions, allowing applications like [usevia.app](https://usevia.app/) and [nuphy.io](https://www.drive.nuphy.io/) to interact with them without needing root privileges.

This repository provides the necessary udev rules to facilitate this interaction, ensuring a smooth and secure experience for users of Nupy Keyboards on Linux systems.

I cannot gurantee or verify if all devices will work because I do not own all of them (Why should I?!). But using the json files from the offficial site, I do have some of the IDs they used. So should work right?

**Add any device missing and become a beloved contributer <3**

## Supported devices
Keyboards tested by developer:
-  Nuphy Air96 v2
-  Nuphy Air60 v2

Keyboards untested (Imported from Nuphys Website):
-  Nuphy Air75 v2
-  NuPhy Gem80
-  NuPhy Halo75
-  NuPhy Halo96
-  NuPhy Nos75


> **_NOTE:_**  contributions will only be verified by logic! There may be false entries created by 3rd parties. I do my best ;)

Keyboards tested/added by contributors (Thank you <3):
- NuPhy Field75 HE V2 (vleeuwenmenno)
- Nuphy Air60 HE (Phrozenn1)
- Nuphy Kick75 (mfiumara)
- NuPhy Halo65 HE (IcarusSosie)
- NuPhy Field75 HE (gtrias)
- NuPhyX BH65 (pigdey)
- NuPhy Air75 v3 (jwa464)
- NuPhy Field75 (gtrias)
- NuPhy Air75 HE (venomyt3)
- NuPhy Node75 LP (FazleArefin)
- NuPhy Air75 v3 ISO (lyynsch)
- NuPhy Node100 LP (digit4lsh4d0w)
- NuPhy Node100 LP ISO (przmkg)
- NuPhy Node100 HP (janpeterka)
- NuPhy Air65 V3 (notonetotalk)
- NuPhy Halo75 V2 (Nicktriez)

Dongles tested/added by contributors (Thank you <3):
- Nuphy Kick 75 Upgrader neversun
- NuPhy Air75 v3 Upgrader (a-szulc)
- NuPhy Node100 LP Dongle (digit4lsh4d0w)
- NuPhy Air65 V3 Upgrader (notonetotalk)

## Installation

### Prerequisites

- A Linux-based operating system.
- A supported Nuphy device.

### Steps for installation


1. **Clone the Repository:**
   ```bash
   git clone https://github.com/Z3R0-CDS/nuphy-linux
   ```

2. **Navigate to the Repository:**
   ```bash
   cd nuphy-linux
   ```

3. **Install the Udev Rule:**

   Automated
   ```bash
   chmod +x install_rules.sh
   ```
   ```bash
   ./install_rules.sh
   ```

   Manual
   ```bash
   sudo cp nuphy.rules /etc/udev/rules.d/
   ```
   ```bash
   sudo udevadm control --reload-rules && sudo udevadm trigger
   ```

4. **Verify Installation:**
   Connect your Nuphy device and verify if it's detected correctly by the [via](https://usevia.app/) or [nuphy.io](https://www.drive.nuphy.io/) application.
   Make sure to follow the guide of the [Official website](https://nuphy.com/pages/via-usage-guide-for-nuphy-keyboards) to ensure its working as intended.
   Also keep in mind it might be required to reopen the browser or try in a private tab if you attempted to use via before.
   I had some cached issues with the permissions at first and testing in a private tab helped.

## Usage

Once installed, the udev rules will automatically set the correct permissions for your Nuphy Device.
This allows the [via](https://usevia.app/) or [nuphy.io](https://www.drive.nuphy.io/) web application to detect and interact with your device without requiring additional configurations.


## Contributing

Want to add support for a new Nuphy device? See [CONTRIBUTING.md](CONTRIBUTING.md) for a full step-by-step guide — or follow the quick instructions below:

1. Run `lsusb | grep nuphy` to find your device ID
2. Copy and paste the template from the top of `nuphy.rules`
3. Replace `<vendorID>` and `<deviceID>` with your values
4. Create a file like `nuphy-air96-v2.rules` and open a PR

```bash
# Install locally without cloning the repo
curl -L -O https://raw.githubusercontent.com/Z3R0-CDS/nuphy-linux/main/nuphy.rules
sudo cp nuphy.rules /etc/udev/rules.d/
sudo udevadm control --reload-rules && sudo udevadm trigger
```

---

For more information or support, open an issue in this repository. I will try to respond asap.