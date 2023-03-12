# ArchLin-install
The repository will describe on how to setup a fresh install of Arch linux (2023)

# 1. Bootable stick
This section describs on how to create a bootable stick on mac os for installation on a desktop pc

## 1.1 Get the iso file
The isofile can be downloaded from the [here](https://archlinux.org/download/ "here title")

## 1.2 Install the file on the stick (max os)
- Open terminal
  - ```diskutil list```

- Check for your USB device (Storagesize) X replaces the number of USB stick
  - ``` diskutil unmountDisk /dev/diskX ```

- Copy the Iso file to the USB stick
  - ``` dd if=path/to/archlinux-version-x86_64.iso of=/dev/rdiskX bs=1m ``` 

# 2 Install Arch linux on target machine
The following describes on how to do a clean installation with SWAP partition

## 2.1 Change Keyboar layout (not permanent)
- Insert the USB stick and boot hodling F2
- Iniside BIOS change booting from x to USB
- Reboot
- Click on install Linux
- A virtual user is created and access to terminal is given
- Change the Keyboard
  - ``` loadkeys de_CH-latin1 ```
- Verify bootmode actualy UEFI (if something is shown = verified)
  - ``` ls /sys/firmware/efi/efivars ```
