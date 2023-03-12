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
