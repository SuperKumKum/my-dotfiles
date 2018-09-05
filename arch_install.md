# Installation of Arch Linux 
this guide is more a go-to-fast-lold guide for my personnal use to install Arch. I'll ugrade it with my personal needs. My actual config is :
* ASUSPRO B9940ua
* i5-7500U
* 8Gb RAM
* 512 SSD
* Intel 620

## Basic installation 

    loadkeys fr
### Format disk 
|device |mount point    |Size   |file system    |
|-------|---------------|-------|---------------|
|/dev/sda1  |/boot/efi  |128 Mb   |ext4         |
|/dev/sda2  |SWAP       |8 Gb     |swap         |
|/dev/sda3  |/          |> 20 Gb  |ext4         |
|/dev/sda4  |/home      |The rest |ext4         |

```bash
mkfs.fat -F32 /dev/sda1
mkswap /dev/sda2
swapon /dev/sda2
mkfs.ext4 /dev/sda3
mkfs.ext4 /dev/sda4
```

add mount point : 
```base
mount /dev/sda2 /mnt
mkdir /mnt/boot && mkdir /mnt/home
mkdir /mnt/boot/efi
mount /dev/sda1 /mnt/boot/efi
mount /dev/sda3 /mnt/home
```
check if everything is ok :

![format](https://puu.sh/BqiSg/13af8d4ea9.png)

### Choose the mirrorlist
you need to edit the file : **/etc/pacman.d/mirrorlist**
For this I need to use *nano* and then search & replace with **ALT+R**
I'll just take the nearest mirrors from **Belgium, France and Netherlands**


### Install arch and cli-basis
```bash
pacstrap /mnt base base-devel pacman-contrib
pacstrap /mnt zip unzip p7zip vim mc alsa-utils syslog-ng mtools dosfstools lsb-release ntfs-3g exfat-utils bash-completion
```
For my laptop I can add LTP for the battery 

![](https://wiki.archlinux.org/index.php/TLP)

### Configuration of fresh install 

* **add keyboard layout:**

    ```bash
    # /etc/vconsole.conf
    KEYMAP = fr-latin9
    ```
* **put language:**

    ```bash
    # /etc/locale.conf
    LANG=en_US.UTF-8
    LC_COLLATE=C
    # /etc/locale.gen
    # Uncomment 
    en_US.UTF-8
    # Generate the file
    locale-gen
    ```
* **change hostname:**

edit the file */etc/hostname*

* **choose time & zone:**

    ```bash
    ln -sf /usr/share/zoneinfo/Europe/Brussels /etc/localtime
    hwclock --systohc --utc
    ```
* **generate the grub file:**



