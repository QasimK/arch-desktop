
# Installation

Follow the [Arch Wiki](https://wiki.archlinux.org/title/Installation_guide) using the specific commands below.

Consider using [Ventoy](https://www.ventoy.net/en/index.html) to _easily_ create a bootable USB drive.

Detailed storage commands: <https://qasimk.io/2020/borg-backup/>

The below just lists differences to the Arch installation guide.


## Partitions

* Use `fdisk` expert mode to set partition labels
* 256MiB is sufficient for the EFI partition
* Don't bother with a swap partition.
* (Set `Linux LUKS` as the partition type for encrypted partitions)


## cryptsetup

This is not recommended — use a self-encrypting drive.


## Filesystems

```sh
mkfs.ext4 -v -L root -T huge -m 1 -O encrypt /dev/nvme0n1p1
```

* `huge` is one inode per 64k; the default is one per 16k
* reserve 1% for root (this helps SSDs anyway)
* `encrypt` is used for `fscrypt`


When mounting:

```sh
mount -o noatime,lazytime /dev/nvme0n1p2 /mnt
mount -o noatime,lazytime /dev/nvme0n1pi /mnt/efi
```

(Do not use `relatime`.)


## pacstrap + arch-chroot

These are essential packages!

```sh
pacstrap /mnt base linux linux-zen linux-lts intel-ucode efibootmgr \
    man-db man-pages texinfo vim tmux htop fish iwd python pacmatic
```

After `arch-chroot`, install optional dependencies:

```sh
pacman -S --needed --asdeps linux-firmware    # linux
pacman -S --needed --asdeps wireless-regdb    # iwd
pacman -S --needed --asdeps pkgfile           # fish
pacman -S --needed --asdeps python-html2text  # pacmatic
pacman -S --needed --asdeps lm_sensors lsof   # htop
```

## Boot Loader

Remove an unnecessary present:

```sh
truncate /etc/mkinitcpio.d/linux-lts.preset
```


Generate unified kernel images:

`/etc/mkinitcpio.d/linux.preset`
```
ALL_config="/etc/mkinitcpio.conf"
ALL_microcode="/boot/intel-ucode.img"

PRESETS=('default' 'fallback')

default_kver="/boot/vmlinuz-linux"
default_image="/boot/initramfs-linux.img"
default_efi_image="/efi/archlinux.efi"
# default_options=""

fallback_kver="/boot/vmlinuz-linux-lts"
fallback_image="/boot/initramfs-linux-lts-fallback.img"
fallback_efi_image="/efi/EFI/boot/bootx64.efi"
fallback_options="-S autodetect"
```

Set the kernel parameters:

`/etc/kernel/cmdline`:
```
rw quiet bgrt_disable root=/dev/nvme0n1p2
```

* `quiet` stops printing log messages
* `bgrt_disable` hides the OEM splash image


Create a script `efiboot.sh`:

```sh
#!/bin/bash
# Create boot entries
# List: efibootmgr
# Delete: efibootmgr -Bb xxxx
# Reorder: efibootmgr -o xxxx,yyyy
set -euo pipefail

efibootmgr \
    --verbose \
    --create \
    --disk /dev/nvme0n1 \
    --part 1 \
    --label "Arch Linux" \
    --loader /archlinux.efi \
    --unicode
```


Modify the default config:

`/etc/mkinitcpio.conf`
```
COMPRESSION="cat"
```

* `cat` reduces the load time because NVME drives are blazing-fast now.


Finally, re-generate the boot images:

```sh
mkinitcpio -P
```


You may also want to reorder the boot order and set a timeout.


TODO: How to skip using `mkinitcpio`?
TODO: Splash image
