---
title: "Setup Raspberry Pi 5 16GB from scratch"
date: 2025-11-04
author: Ujwal Iyer
tags: [Raspberry Pi, HAT,  NVMe SSD]
description: Setup Raspberry Pi5 16 GB, with M.2 HAT+ 256GB SSD Kit, active Cooler with heat sink- and finally install OS on the assembled Pi.

---

## 1. OS Setup

- Setup Raspberry Pi OS 64-bit (Bookworm) → best for GPIO/camera + easiest device support.
- Download Raspberry Pi Imager from https://www.raspberrypi.com/software/
- Install it on your computer (Windows, macOS, or Linux)
- Select Raspberry Pi official OS 64-bit, the SD-card to flash, and the actual device bought
- Now edit settings- set hostname(raspberrypi.local), Set username(admin) and password, configure WLAN Wifi name, enable SSH
- Now finally write the image to the SD card- will take a while. 

Raspberry Pi 16GB

![][def4]


[def4]: /assets/img/pi-16gb.jpg

Cooler, microSD card, and 27W official charger

![][def5]


[def5]: /assets/img/cooler-SD-charger.png

## 2. Hardware Setup

- Join Cooler with the board: Align plastic connectors and stickers to the pi board and hear 2 clicks, then join fan cable to the fan connector on the board. 
- Attach M2.HAT + NVMe SSD: Storage Solution HAT connects the NVMe drive via PCIe. 
- Attach micro-SD card to the bottom of the pi board

Pi and Cooler attached

![][def6]


[def6]: /assets/img/pi+cooler.png

M.2 HAT+ with 256GB SSD

![][def7]


[def7]: /assets/img/m2hat-case.jpg

All components combined: 

![][def8]


[def8]: /assets/img/pi+cooler+ssd.jpg


## 3. Boot up
- Connect power and wifi network.
- The Pi will boot- the initial setup runs automatically.
- You can now SSH in from your computer: ssh username@hostname.local
- If you set: hostname: pi-lab, username: ujwal, You’d connect like this: ssh ujwal@pi-lab.local. 
> After 2 hours of debugging, this was the issue: if ur wifi or ssid is on 5ghz, you must change the channel number to 36, reboot the router, and then finally flash your SD with the image. 

![][def]


[def]: /assets/img/wifi-fix.png

finally ssh into the pi: 

![][def2]


[def2]: /assets/img/ssh-successful.png

## 4. Update software

This brings Raspberry Pi OS, firmware, and drivers up to date (especially important for Wi-Fi stability and SSD support).
```bash
sudo apt update && sudo apt full-upgrade -y
```

Reboot now, takes 1-2 mins.
```bash
sudo reboot
```

Now ssh back into the pi, and boot from the NVMe SSD (faster and more reliable than microSD)

```bash
sudo raspi-config
```
Advanced Options → Boot Order → NVMe/USB Boot First
Then use the “SD Card Copier” tool (sdcardcopy) to clone your system from the microSD to the NVMe drive.
Power off, remove the microSD card, and power back on — it will now boot from the SSD.

## 5. Copy SD to SSD for boot

Make sure nothing from the NVMe is mounted: 
```bash
sudo umount -R /mnt/clone 2>/dev/null || true
lsblk
```

Wipe leftover signatures from the NVMe:
```bash
sudo wipefs -a /dev/nvme0n1
```

Clone SD → NVMe (bit-for-bit):
```bash
sudo dd if=/dev/mmcblk0 of=/dev/nvme0n1 bs=16M status=progress conv=fsync
sudo partprobe /dev/nvme0n1
```

Grow the root partition to fill the NVMe. Use growpart (simplest), then grow the filesystem:
```bash
sudo apt-get update
sudo apt-get install -y cloud-guest-utils
```

Expand partition 2 (root) to the end of the disk:
```bash
sudo growpart /dev/nvme0n1 2
```

Check/resize the ext4 filesystem:
```bash
sudo e2fsck -f /dev/nvme0n1p2
sudo resize2fs /dev/nvme0n1p2
```

Boot from NVMe:
```bash
sudo poweroff
```

Now remove SD card, power on the PI, it should boot from SSD. Verify after boot:
```bash
lsblk -o NAME,SIZE,FSTYPE,MOUNTPOINT
mount | grep " / "
```

![][def3]


[def3]: /assets/img/boot-from-ssd.PNG
