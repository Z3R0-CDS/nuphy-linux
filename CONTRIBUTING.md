# Contributing to nuphy-linux

Thank you for contributing to this project! This guide explains how to add support for a new Nuphy device.

## Before you start

If you just want to fix your keyboard, see the [README](README.md) for installation instructions. This document is for people who want to add their device to the rules.

## What this project does

This repository provides udev rules that allow standard Linux users to access Nuphy keyboards directly via [usevia.app](https://usevia.app/) or [nuphy.io](https://drive.nuphy.io/) without requiring root privileges.


## Adding a new device

### Quick summary

1. Find your device's USB product ID
2. Copy the template from the bottom of `nuphy.rules`
3. Fill in the template with your device details
4. Submit a PR

### Step-by-step

#### 0. **Are you sure!?**

**Please verify your device is not supported yet!**

#### 1. Get your device ID

Plug in your keyboard and run:

```bash
lsusb | grep -i nuphy
```

You'll see something like:

   ```
   Bus 005 Device 007: ID 19f5:3265 NuPhy NuPhy Air96 V2 <- Example output for my nuphy
                              ^ 
                            These are the vendor ID on the left and device ID on the right
   ```

The vendor ID is always `19f5` — you only need the **device ID** (`XXXX`). Make a note of the full device name too.

#### 2. Find a free slot

- Open `nuphy.rules` and look at the top section where all device comments are listed. 
- Look at the repo for openend Issues/PRs and check slot numbers to it.
- Take the next available slot that you can see in the `nuphy.rules` file.

No slot? Create an issue first :) Leave your info. No need to stalk your inbox. Worst case I will add the device for you!


#### 3. Create your entry

THE SLOT MUST BE NOTED IN ISSUE/MERGE REQUEST! 

Copy the **ENTIRE** template for your Issue/Request:

```
# Device name: <your device name>
# Product ID:  <your product hex in lowercase>
# Tested:      <yes/no>
# Date:        <today's date>
#
# USB_DEVICE rules (uncomment and fill below):
# SUBSYSTEM=="usb", ENV{DEVTYPE}=="usb_device", ATTR{idVendor}=="19f5", ATTR{idProduct}=="<your_product>", MODE="0666"
#
# HIDRAW rules (uncomment and fill below):
# KERNEL=="hidraw*", ATTRS{idVendor}=="19f5", ATTRS{idProduct}=="<your_product>", MODE="0666"
```
Fill in the template with your values. **Two rule pairs are required**: one for `usb_device` and one for `hidraw*`.

Add the device to the `nuphy.rules` file. 

Including addding the Device to the reserved slot in the comment above the rules.

To take a slot means you will when editing REMOVE THE LINE of that said slot. Do not write below or above!



#### 4. Validate your entry

If you want to test:

```bash
udevadm verify nuphy.rules
```


### What to NOT do

- **Do NOT reorder existing rules or comments** — this causes conflicts
- **Do NOT delete or modify existing entries** — even if there's a typo
- **Do NOT add rules below the reserved slot section** — that section is for your contribution only
- **Do NOT edit the README to avoid issues with the merge**
- **Do NOT add slots. That will be done by me when needed.**
- **Do NOT write above or below your slot**

### PR Checklist

- [ ] I found the id using the command
- [ ] I found the next available slot
- [ ] I created a patched version of the rules
- [ ] I opened a PR with changes and description


### Submitting the PR

Create a new branch from `main`, make your changes, then submit a PR:

```bash
git checkout -b add-<device-name>-support
# edit nuphy.rules
git add nuphy.rules
git commit -m "feat: add <device_name> support"
git push origin add-<device-name>-support
```

Your PR only needs to touch `nuphy.rules` — nothing else.

Your PR should contain all information stated in step 3.

Tag the PR with enhancement for new rules.

### Troubleshooting

**Your device doesn't show up in VIA after installing:**

1. Try unplugging and replugging the keyboard
2. Check in your browser's dev tools that the device is detected
3. Verify the product ID in your PR matches exactly (hex, case-sensitive)
4. Create a test rules file as shown above and check `sudo dmesg` for errors
5. Reboot... Might sound stupid but solves a good chunk of issues

**Still no luck?** Open an issue with:
- Your exact device name (from `lsusb`)
- The product ID you added
- What you tried

We'll figure it out together.
