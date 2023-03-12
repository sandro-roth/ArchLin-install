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

## 2.1 Start installation
- Insert the USB stick and boot hodling F2

- Iniside BIOS change booting from x to USB

- Reboot

- Click on install Linux

- A virtual user is created and access to terminal is given

## 2.1 Change Keyboar layout (not permanent)
- Change the Keyboard
  - ``` loadkeys de_CH-latin1 ```

- Verify bootmode actualy UEFI (if something is shown = verified)
  - ``` ls /sys/firmware/efi/efivars ```

## 2.2 Connect to wifi
- ``` iwctl ```
  - ``` device list ```
  - ``` station wlan0 scan ```
  - ``` station wlan0 get-networks ```
  - ``` station wlan0 connect MyWlan ```
  - ``` exit ```

- check connection
  - ``` ping -c 3 google.com ```

## 2.3 Update system clock
- check the status of the current time
  - ``` timedatectl ```

- change timezone
  - ``` ln -sf /usr/share/zoneinfo/Europe/Zurich /etc/localtime ```

- reset hardwareclock
  - ``` hwclock --systohc --utc ```

- If date is not shown correctly enable timesync at startup
  - ``` timedatectl status ```
  - ``` systemctl start systemd-timesyncd.service ```


## 2.4 Partition the disk
- show all the disks
  - ``` fdisk -l ```

- access the disk where to OS should run on (nvme0n1)
  - ``` cfdisk /dev/nvme0n1 ```

- change the table to the following 
    Partition     | Type          | Size          | Name
    ------------- | ------------- | ------------- | -------------
    EFI System    | EFI system    | 1G            | nvme0n1p1
    SWAP          | Linux Swap    | ~ 16G         | nvme0n1p2
    Free space    | Linux file    | rest          | nvme0n1p3

- Agree with the option Write and afterwards quit the partition menue

- Format the partitions
  - show the partitions names by:
    ``` fdisk -l ```
  
  - For EFI System
    - ``` mkfs.fat -F 32 /dev/nvme0n1p1 ```

  - For SWAP
    - ``` mkswap /dev/nvme0n1p2 ```
    
  - For Free space (root partition)
    - ``` mkfs.ext4 /dev/nvme0n1p3 ```

- mount the file systems (boot and swap)
  - ``` mount /dev/nvme0n1p3 /mnt ```
  - ``` mkdir /mnt/boot ```
  - ``` mount /dev/nvme0n1p1 /mnt/boot ```

  - enable swap partition
    - ``` swapon /dev/nvme0n1p2 ```
  
  - check if mounted correctly
    - ``` lsblk ```

## 2.5 Installation
  
