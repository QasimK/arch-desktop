# Installation

Follow the [Arch Wiki](https://wiki.archlinux.org/title/Installation_guide) using the specific commands below.

Storage Commands: <https://qasimk.io/2020/borg-backup/>

fdisk
use expert mode to set partition labels
set linux LUKS as partition type for root

Basically as above

cryptsetup

see cryptsetup benchmark
see cryptsetup --help for defaults

cryptsetup --persistent --perf-no_read_workqueue --perf-no_write_workqueue open /dev/... clearroot

(no work queues for SSD)

mkfs.ext4 -v -L root -T huge -m 1 /dev/mapper/clearroot

mount -o noatime,lazytime ...

(huge is one inode per 64k, default is per 16k)
(reserve 1% for optimum ssd performance anyway)

pacstrap /mnt base linux linux-zen linux-lts linux-firmware amd-ucode efibootmgr man-db man-pages texinfo vim tmux htop fish iwd crda lm_sensors lsof strace python


Create a script:

```terminal
#!/bin/bash
# Create boot entries
# List: efibootmgr
# Delete: efibootmgr -Bb xxxx
set -euo pipefail

efibootmgr \
    --disk /dev/sdc \
    --part 1 \
    --create \
    --label "Arch Linux" \
    --loader /vmlinuz-linux \
    --verbose \
    --unicode 'cryptdevice=PARTLABEL=mypartlabel:clearroot root=/dev/mapper/clearroot rw initrd=\amd-ucode.img initrd=\initramfs-linux.img'
```

Be sure to add the fallbacks and other kernels.

Remove some unnecessary building. i.e. linux and linux-lts should be fallbacks.
linux-zen should be default only.

Modify: /etc/mkinitcpio.d/..preset
Then mkinitcpio -P

Reorder the boot order, set a timeout.
