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
