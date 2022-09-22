# Installation

Follow the [Arch Wiki](https://wiki.archlinux.org/title/Installation_guide) using the specific commands below.

Consider using [Ventoy](https://www.ventoy.net/en/index.html) to _easily_ create a bootable USB drive.

Storage Commands: <https://qasimk.io/2020/borg-backup/>

fdisk
use expert mode to set partition labels
set linux LUKS as partition type for root

NOTE: EFI partition /efi to be 256MiB (for two images; 512MiB for 4 images!)

Basically as above

cryptsetup

see cryptsetup benchmark
see cryptsetup --help for defaults

cryptsetup --persistent --perf-no_read_workqueue --perf-no_write_workqueue open /dev/... clearroot

(no work queues for SSD)

```terminal
mkfs.ext4 -v -L root -T huge -m 1 -O encrypt /dev/mapper/clearroot
```
```
mount -o noatime,lazytime ...
```

(huge is one inode per 64k, default is per 16k)
(reserve 1% for optimum ssd performance anyway)

```terminal
pacstrap /mnt base linux linux-zen linux-lts linux-firmware amd-ucode efibootmgr man-db man-pages texinfo vim tmux htop fish iwd python pacmatic
```

First thing after installing, install optional

```terminal
pacmatic -S --needed --asdeps linux-firmware (linux)
pacmatic -S --needed --asdeps wireless-regdb (iwd)
pacmatic -S --needed --asdeps pkgfile (fish)
pacmatic -S --needed --asdeps python-html2text (pacmatic)
pacmatic -S --needed --asdeps lm_sensors lsof strace (htop)
```

## BOOT LOADER

https://wiki.archlinux.org/title/Unified_kernel_image

```terminal
rm /etc/mkinitcpio.d/linux-lts.preset
```

TODO: this rm does not work.

Modify `/etc/mkinitcpio.d/linux.preset`


```
ALL_config="/etc/mkinitcpio.conf"
ALL_microcode="/boot/*-ucode.img"

PRESETS=('default' 'fallback')

default_kver="/boot/vmlinuz-linux"
default_image="/boot/initramfs-linux.img"
default_efi_image="/efi/efi/boot/bootx64.efi"
# default_options=""

fallback_kver="/boot/vmlinuz-linux-lts"
fallback_image="/boot/initramfs-linux-lts-fallback.img"
fallback_efi_image="esp/archlinux-lts-fallback.efi"
fallback_options="-S autodetect"
```

Modify `/etc/kernel/cmdline`:

```
rw quiet splash bgrt_disable root=/dev/nvme0n1p2
```

NOTE: this will auto-boot `linus-lts-fallback`

Create a script `efiboot.sh`

```terminal
#!/bin/bash
# Create boot entries
# List: efibootmgr
# Delete: efibootmgr -Bb xxxx
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

Then mkinitcpio -P

Reorder the boot order, set a timeout.





Note: for the linux tty (virtual terminal), the screen will disable after 5 minutes (`consoleblank`).

Note: `quiet splash` is just to reduce the printing of log messages

Also:

Modify /etc/mkinitcpio.conf

```
HOOKS=(base udev autodetect block filesystems keyboard)
COMPRESSION="cat"
```





TODO: How to skip mkinitcpio.conf (no cryptsetup)

Add `modules=(amdgpu)` (or whatever) to get the right resolution for the luks prompt...
<https://wiki.archlinux.org/title/Kernel_mode_setting#Early_KMS_start>


TODO: mkinitcpio v31
    Bundle all files into one
    Splash image
    https://linderud.dev/blog/mkinitcpio-v31-and-uefi-stubs/

    combine with https://nwildner.com/posts/2020-07-04-secure-your-boot-process/?

    See: https://github.com/archlinux/mkinitcpio/blob/master/man/mkinitcpio.8.txt
        Full mkinitcpio options
