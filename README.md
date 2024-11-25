# PintoGPi
![Gentoo](https://assets.gentoo.org/tyrian/v1/site-logo.svg "Gentoo")

## This project is just a Gentoo intalation in Pi model 1 B+ with a [Zx Spectrum](https://en.wikipedia.org/wiki/ZX_Spectrum) emulator
- Why [Gentoo](https://www.gentoo.org), just because I can, and Raspberry Pi 1 B is a great little device for learning, but it can be challenging to find a suitable operating system for it.
- The instalations will be made all from  my Arch Linux [PintArch](https://github.com/dpnpinto/PintArch)
- Don't use my version of Arch, do yourself a favor and install [Arch](https://archlinux.org) and, then, you are prepared for [Gentoo](https://www.gentoo.org)
- I will leave here the image with all config done but It's nice to learn with a Gentoo instalation, I sugest that you do it yourself. "This is the way" (Malandorian way :D). 

### Steps to get it done

- Partition the SD card the right way
   - partition 1 - Fat 32 as Boot
   - partition 2 - As SWAP, 2x memory
   - partition 3 - Root system, I use ext4
I use cfdisk, but you can use other software like fdisk or parted. 
- Format the SD card
   - Make partition 1 as Fat 16
     mkfs.vfat -F 16 /dev/"partition 1"
   - Make partition 2 as SWAP
     mkswap /dev/"partition 2"
   - MAke partition 3 as ext4
     mkfs.ext4 /dev/"partition 3"
- Mount stuff in your linux distro (I use Arch BTW :D))
   - Create a directory in /mnt and mount your sd card partition 3 to that directory
     mkdir /mnt/PintoGPi
     mount /dev/"partition 3" /mnt/PintoGPi
   - Same thing for the boot
     mkdir /mnt/PintoGPi/boot/
     mount /dev/"partition 1" /mnt/PintoGPi/boot
- Copy the stage 3 Gentoo to your mounted SD drive
   - They are here [Gentoo stage 3 images](https://gentoo.osuosl.org/releases/arm/autobuilds/),
    For this project (RaspBery Pi 1 B+, ARM V6)I use this on stage3-armv6j_hardfp-openrc-20241120T233322Z.tar.xz (OpenRC)
    Then get the tar file, for example wget https://gentoo.osuosl.org/releases/arm/autobuilds/current-stage3-armv6j-openrc/stage3-armv6j-openrc-20241120T233322Z.tar.xz
    Then uncomrpess the tar file to you SD card mounted in /mnt/PintoGPi tar -xf stage3-armv6j-openrc-20241120T233322Z.tar.xz -C /mnt/PintoGPi/
- Copy the boot stuff Kernel and modules to boot
- Config correct keyboard
- Config correct local
- Config FSTAB
- remove pass from root user
- reboot
... Will continue
