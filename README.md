# Arch-Linux-Cheat-Sheet

<h1 align="center">
	<img src="https://www.archlinux.org/static/logos/archlinux-logo-dark-90dpi.ebdee92a15b3.png" alt="arch">
</h1>

Awesome Arch Linux cheat sheet, that I will mostly update from time to time, whenever I find something, that I need to remember, but find it hard to. 

I am also partly writing my own arch linux install script, to help myself learn bash, and other pretty cool features, that I had no knowledge of. 

## Install guide
```
key: alt+ctrl+f2
# less install.txt
```

###  Verify boot
```
# ls /sys/firmware/efi/efivars
```

###  Internet
One of the most important ones! Remember to check the internet connection. Dhcpcd daemon already started for wired devices.

```
# ping archlinux.org
``` 
### Wireless
Arch linux should by default have found the network card. Check by writting **ip addr**.

To connect to the wireless access point, use the following command.
```
# wifi-menu (interface name for wireless network card)
```

### Format Partitions
```
EF00 = boot
8200 = swap
8300 = filesystem / root/home
```
## Good-Stuff

### GIT
https://github.com/freshfruits/Git-Cheat-Sheet

### Font
https://www.archlinux.org/packages/community/any/adobe-source-han-sans-otc-fonts/

`# sudo pacman -S adobe-source-han-sans-otc-fonts `

### Pacman-Commands

```
# pacman -Syy      	  # force synchronization of repository databases
# pacman -Syu		 # 

# pacman -Ss xyz   	# search repository database for packages for xyz
# pacman -S xyz    	 # install package xyz

# pacman -Sy xyz   	# synchronize repo and install xyz
# pacman -Syy xyz        # really synchronize repo and install xyz

# pacman -R xyz    	 # remove package xyz but keep its dependencies installed
# pacman -Rs xyz   	# remove package xyz and all its dependencies (if they are not required by any other package)
# pacman -Rsc xyz        # remove package xyz, all its dependencies and packages that depend on the target package
# pacman -Ql xyz   	# show all files installed by the package xyz
# pacman -Qo /path     # find the package which installed the file at /pat
```
