# Storage

For home, two disks:

* Use dm-integrity with dm-crypt to detect bitrot
* Use mdadm raid1 to correct bitrot [it's possible to do this later]
* Use ext4 for simplicity

For root, a single, much smaller disk without mdadm.

LVM raid is not used because folders can accomplish the same thing, and all data should be protected with raid1.

What's missing:

1. Snapshot (LVM is not great?)
2. Snapshot send/receive for ultra-fast backups (à la `btrfs`)
2. Compression

What do we not want:

* It's oh-so-very tempting to want tiered storage or caching with super-fast SSDs, but, honestly, spend a little more money to not need this. (For a NAS, it's a different story.)
* LVM for snapshots for backups.

So this is a three disk solution that separates the OS from the data. The home directory _does_ usually end up containing some installation files, but these can easily be cleaned up.

The ideal solution would be [bcachefs](https://bcachefs.org/) but it is not feature complete and battle-hardened yet.

Self-encrypting drives are not used because the use of `dm-integrity` requires some level of use of encryption anyway.

## Windows

A separate disk can be used to run Windows.

## fscrypt

Use fscrypt to encrypt folders with a password to protect sensitive documents from malware.

## Installation Commands

https://qasimk.io/2020/borg-backup/

Note: dm-integrity max speed is on the order of ~100MiB/s even on an NVMe drive.


--allow-discards --persistent X
periodic trim instead.

dm-integrity does not support discard.


Write performance hit nvme - 1.7GB/s vs 374 MB/s - 4.5x slower
(crypt vs crypt/integrity)


440 vs 179 = 2.5x slower

Encryption has practically no overhead.


**IMPORTANT**

Basically dm-integrity is a dead-end.

We are probably better off with using a cshatag approach.
Store a checksum/mtime of each file in extended attributes.
Run the checker manually before every backup.

NVMe read @ 6.9 GB/s => 500 GB in 72s
SSD read @ 0.5 GB/s => 4000 GB in 2 hours

This is probably better than anything else and is more like snapraids approach.

Recover file from backup only. Error exit -> Prevent backup.

md5 = 138240/3s 16k
sha1 = 315856/3s 16k ~~ 1.6 GB/s
sha256 = 249840/3s 16k

## Smart

...

### Installation

Basically as above

pacstrap: base linux linux-lts linux-firmware amd-ucode vim tmux htop man-db man-pages texinfo iwd

crda - iwd
python
lm_sensors
lsof
strace



cryptroot = e6e67e3d-c904-254b-a433-4a982d3be70c (PARTUUID)
root = 1ee89039-468a-45e3-bc6b-80ae9ea6366a (UUID)

efibootmgr --disk /dev/nvme0n1 --part 1 --create --label "Arch Linux" --loader /vmlinuz-linux --unicode 'cryptdevice=PARTUUID=e6e67e3d-c904-254b-a433-4a982d3be70c:root root=UUID=1ee89039-468a-45e3-bc6b-80ae9ea6366a rw initrd=\amd-ucode.img initrd=\initramfs-linux.img' --verbose


Set perm flags;

cryptsetup --allow-discards --perf-no_read_workqueue --perf-no_write_workqueue --persistent open ...
