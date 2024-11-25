# PintoGPi
![Gentoo](https://assets.gentoo.org/tyrian/v1/site-logo.svg "Gentoo")

## This project is just a Gentoo intalation in Pi model 1 B+ with a [Zx Spectrum](https://en.wikipedia.org/wiki/ZX_Spectrum) emulator
- Why [Gentoo](https://www.gentoo.org), just because I can, and Raspberry Pi 1 B is a great little device for learning, but it can be challenging to find a suitable operating system for it.
- The instalations will be made all from  my Arch Linux [PintArch](https://github.com/dpnpinto/PintArch)
- Don't use my version of Arch, do yourself a favor and install [Arch](https://archlinux.org) and, then, you are prepared for [Gentoo](https://www.gentoo.org)
- I will leave here the image with all config done but It's nice to learn with a Gentoo instalation, I sugest that you do it yourself. "This is the way" (Malandorian way :D). 

### Steps to get it done

- Partition the SD card the right way
   - Partion 1 - Fat 32 as Boot
   - Partion 2 - As SWAP, 2x memory
   - Partition 3 - Root system, I use ext4
- Format the SD card
   - Make partition 1 as Fat 16
   - Make partition 2 as SWAP
   - MAke partition 3 as ext4
- Mount stuff in your linux distro (I use Arch BTW :D))
   - Create a directory in /mnt
   - mount your sd card aprtition 3 to that directory
   - 
- Copy the stage 3 Gentoo to your mounted SD drive
- Copy the boot stuff Kernel and modules to boot
- Config correct keyboard
- Config correct local
- Config FSTAB
- remove pass from root user
- reboot
... Will continue
