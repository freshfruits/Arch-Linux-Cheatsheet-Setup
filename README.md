# Arch-Linux-Cheatsheet-Setup

Original Author: [Jacob](https://github.com/freshfruits)

### Introduction
**Note: This cheatsheet is directed towards myself. (UEFI)**

> Basically, this is my Arch Linux cheat sheet (Arch Linux setup), that I will mostly update from time to time, whenever I find something, that I need to remember, but will forget at some point. 
I am also partly writing on a arch linux install script, to help myself learn bash, and other pretty cool features, that I had no knowledge of. 


## Install guide
```
key: alt+ctrl+f2
$ less install.txt
```

###  Verify boot
```
$ ls /sys/firmware/efi/efivars
```

###  Internet
One of the most important ones! Remember to check the internet connection. Dhcpcd daemon already started for wired devices.

```
$ ping archlinux.org
``` 
### Wireless
Arch linux should by default have found the network card. Check by writting **ip addr**.

To connect to the wireless access point, use the following command.
```
$ wifi-menu (interface name for wireless network card)
```

### Format Partitions
```
EF00 = boot
8200 = swap
8300 = filesystem / root/home
```

#### Size of Partitions
```
boot partition = 100MiB (There is a lot of shit in Boot, so only 100MB) 
```

```
swap partition = 6GiB/8GiB/12GiB/24GiB (x = ram, equation : 1.5*x. Though you don't really need more than 6GiB)  
```

```
root partition = 10GiB/20GiB (There is not really need for more, completely depends on what you wish to achieve) 
```

```
home partition = rest of GiB data.   
```

### filesystem
sda1 = boot
sda2 = swap
sda3 = root
sda4 = home

Example
```
$ mkfs.fat -F32 /dev/sda1
$ mkswap /dev/sda2 
$ swapon /dev/sda2 
$ mkfs.ext4 /dev/sda3
$ mkfs.ext4 /dev/sda4
```

Y == partition number

```
# mkfs.fat 	-F32 	/dev/sdaY
# mkswap 	/dev/sdaY
# swapon 	/dev/sdaY
# mkfs.ext4 	/dev/sdaY
# mkfs.ext4 	/dev/sdaY
```

### Mounting
sda1 = boot
sda2 = swap
sda3 = root
sda4 = home

Example
```
$ mount /dev/sda3 /mnt
$ mkdir /mnt/boot
$ mkdir /mnt/home
$ mount /dev/sda1 / mnt/boot
$ mount /dev/sda4 /mnt/home
```

Y == partition number
```
# mount /dev/sdaY /mnt
# mkdir /mnt/boot
# mkdir /mnt/home
# mount /dev/sdaY /mnt/boot
# mount /dev/sdaY /mnt/home
```

### Mirrors
For help. 
```
rankmirrors -h
```

Backup the current mirrorlist 
```
$ cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.backup
```

Run the following sed line to uncomment every mirror
```
$ sed -i 's/^#Server/Server/' /etc/pacman.d/mirrorlist.backup
```

Rank the mirrors
```
$ rankmirrors -n 6 /etc/pacman.d/mirrorlist.backup > /etc/pacman.d/mirrorlist
```

### Base
```
$ pacstrap -i /mnt base base-devel
```

### Fstab
```
$ genfstab -U /mnt >> /mnt/etc/fstab
```

### Chroot
Enter chroot
```
$ arch-chroot /mnt
```

### TimeZone
Set ur timezone
```
$ ln -s /usr/share/zoneinfo/Region/City > /etc/localtime
```

Set hardware clock
```
$ hwclock --systohc
```

### Locale
Uncomment the language you want.
```
$ nano /etc/locale.gen
```

To generate the locale
```
$ locale-gen
```

```
$ echo LANG=en_DK.UTF-8 > /etc/locale.conf
$ export LANG=en_DK.UTF-8
```

### Hostname
Choose whatever thats fits. 
```
$ echo xxx > /etc/hostname
```

### AUR
```
$ nano /etc/pacman.conf
```

Uncomment these two lines
```
[multilib]
Include = /etc/pacman.d/mirrorlist
```

Add these lines at the bottom of the file. So you can install the AUR packages.
```
[archlinuxfr]
SigLevel = Never
Server = http://repo.archlinux.fr/$arch
```

Next step would be optional. Update with. 
```
$ pacman -Syu
```

### Root password
```
$ passwd
```

### bootloader 
```
$ bootctl install
(LONG ID) # blkid -s PARTUUID -o value /dev/sdxY > /boot/loader/entries/arch.conf
$ vim/nano /boot/loader/entries/arch.conf
```
#### arch.conf
```
title Arch Linux
linux /vmlinuz-linux
initrd /initramfs-linux.img
options root=PARTUUID=LONGID rw
```

### User
Make a user

```
$ useradd -m -g users -G wheel,storage,power -s /bin/bash (name)
```

Create a password for the user
```
$ passwd (name)
```

Create a password for the user
```
$ passwd (name)
```

Find %Wheel All=(ALL) ALL .. uncomment the line (Optional : add the following line under it (To do a sudo command, you have to know the root password). )
```
# Defaults rootpw
```

### Reboot
```
$ exit
$ umount -R /mnt
$ reboot
```

### Post-Install
All that is left to do, is to install xorg (or wayland), and a window- or desktop manager 

I use xorg as it seems that wayland is still rather unstable.
```
$ sudo pacman -S xorg-server xorg-xinit 
```
### i3wm
Personally I use i3gaps (eye candy). i3lock (Note: Its not secure anymore), is your lock screen. 
```
$ sudo pacman -S i3 i3lock
```

Setting up i3wm/i3gaps. 
```
$ echo "exec i3" >> $HOME/.xinitrc
```
Reboot, Login, write. 
```
$ startx
```

I hope you enjoy Arch-Linux. <br>
Best wishes. 

### References

Simon <br>
Kristian

https://wiki.archlinux.org/index.php/installation_guide <br>
https://wiki.archlinux.org/index.php/Arch_User_Repository <br>
https://wiki.archlinux.org/index.php/mirrors
