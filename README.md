# PintoGPi
![Gentoo](https://assets.gentoo.org/tyrian/v1/site-logo.svg "Gentoo")

## This project is a [Gentoo](https://pt.wikipedia.org/wiki/Gentoo_Linux) intalation in a 2014 [Pi model 1 B+](https://en.wikipedia.org/wiki/Raspberry_Pi), with a [Zx Spectrum](https://en.wikipedia.org/wiki/ZX_Spectrum) emulator, and some cross compiler for Gentoo, yes the Pi is very weak for [Portage](https://wiki.gentoo.org/wiki/Portage).
- Why [Gentoo](https://www.gentoo.org), just because I can, and Raspberry Pi 1 B is a great little device for learning, it can be challenging to find a suitable small operating system for it.
- The instalations will be made all from  my Arch Linux [PintArch](https://github.com/dpnpinto/PintArch)
- Don't use my version of Arch, do yourself a favor and install [Arch](https://archlinux.org) and, then, you are prepared for [Gentoo](https://www.gentoo.org)
- I will leave here the image with all my config done but It's very nice to learn with a Gentoo instalation, I sugest that you do it yourself. "This is the way" (Malandorian way :D). 

### Steps to get it done, format and copy stage 3 Gentoo to SD

- Partition the [SD card](https://en.wikipedia.org/wiki/SD_card) the right way
   - partition 1 - Fat 32 as Boot
   - partition 2 - As SWAP, 2x memory
   - partition 3 - Root system, I use ext4
I use cfdisk, but you can use other software like fdisk or parted. 
- Format the SD card
   - Make partition 1 as Fat 16
     - mkfs.vfat -F 16 /dev/"partition 1"
   - Make partition 2 as SWAP
     - mkswap /dev/"partition 2"
   - MAke partition 3 as ext4
     - mkfs.ext4 /dev/"partition 3"
- Mount stuff in your linux distro (I use Arch BTW :D))
   - Create a directory in /mnt and mount your sd card partition 3 to that directory
     - mkdir /mnt/PintoGPi
     - mount /dev/"partition 3" /mnt/PintoGPi
   - Same thing for the boot
     - mkdir /mnt/PintoGPi/boot/
     - mount /dev/"partition 1" /mnt/PintoGPi/boot
- Copy the stage 3 Gentoo to your mounted SD drive
   - They are here [Gentoo stage 3 images](https://gentoo.osuosl.org/releases/arm/autobuilds/),
      - For this project (RaspBerry Pi 1 B+, ARM V6)I use this one stage3-armv6j_hardfp-openrc-20241120T233322Z.tar.xz (With OpenRC ;))
    - Then get the tar file to a folder, for example
      - wget https://gentoo.osuosl.org/releases/arm/autobuilds/current-stage3-armv6j-openrc/stage3-armv6j-openrc-20241120T233322Z.tar.xz
    - Uncomrpess the tar file to you SD card mounted in /mnt/PintoGPi
      - tar -xf stage3-armv6j-openrc-20241120T233322Z.tar.xz -C /mnt/PintoGPi/
- You have now to install Portage, that is the oficial pakage manager of Gentoo (a very advanced one ;) )
    - To install it you have to download the snapshot of it and copy it to /usr (user system resorces)
    - The snapshot is located in https://gentoo.osuosl.org/snapshots/ the file portage-latest.tar.xz
      - Get it with wget https://gentoo.osuosl.org/snapshots/portage-latest.tar.xz
      - Extract to your /usr in sd card tar -xf portage-latest.tar.xz -C /mnt/PintoGPi/usr
- Install the Kernel and modules of the Raspberry Pi
    - You can get all the stuff of Raepbery Pi from https://github.com/raspberrypi/firmware/
      - Clone the stable repository
        - git clone -b stable --depth 1 https://github.com/raspberrypi/firmware/
      - get inside the cloned firmware cd firmware
        - copy boot cp -r /boot /mnt/PintoGPi/boot/
        - copy modules cp -r /modules /mnt/PintoGPi/lib/
- Config the correct fstab
   - Here you must use the correct devices that will start in Rapbery Pi, the SD is named mmcblk0p, edit the /mnt/PintoGPi/etc/fstab
     - /dev/mmcblk0p1		/boot		auto		noauto,noatime	1 2
     - /dev/mmcblk0p2		none		swap		sw		0 0
     - /dev/mmcblk0p3		/		ext4		noatime		0 1    
- Set the boot options
   - Must configure the boot options in /mnt/PintoGPi/boot/cmdline.txt
     - Add to cmdline.txt this dwc_otg.lpm_enable=0 console=ttyAMA0,115200 kgdboc=ttyAMA0,115200 console=tty1 root=/dev/mmcblk0p3 rootfstype=ext4 elevator=deadline rootwait 
- Config correct time zon
   - For Azores cp /mnt/PintoGPi/usr/share/zoneinfo/Atlantic/Azores /mnt/PintoGPi/etc/localtime (normaly I use a simbolic link)
   - echo "Atlantic/Azores" > /mnt/PintoGPi/etc/timezone
- remove pass from root user
   - Lets force first start with no password in root
     - sed -i 's/^root:.*/root::::::::/' /mnt/PintoGPi/etc/shadow
- Unmount SD drives and reboot
   - umount /mnt/PintoGPi/boot
   - umount /mnt/PintoGPi 
- Remove SD Card from your system and put it in RarpberryPi 

## Steps to get it done, booting with the Raspberry Pi
... Will continue
