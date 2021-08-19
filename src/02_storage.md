# Storage

Use a single disk with ext4 because anything else invites bikeshedding and problems.

We'll have to complement this ourselves with:

* Regular backups to avoid data loss
* Encryption to avoid theft and fraud
* Checksums to avoid bitrot and tampering

We miss out on:

1. Snapshots
2. Snapshot send/receive for ultra-fast backups (à la `btrfs`)
3. File Compression

The remaining page discusses alternatives.

## Self-encrypting drives

It's possible to use [sedutil](https://github.com/Drive-Trust-Alliance/sedutil/), but:

1. Sleep mode seems to be dubious.
2. The firmware may be dubious.

It's also possible to use hdparm for a non-boot drive.

1. https://wiki.archlinux.org/title/Solid_state_drive/Memory_cell_clearing#Step_2_-_Enable_security_by_setting_a_user_password
2. https://www.pugetsystems.com/labs/articles/Introduction-to-Self-Encrypting-Drives-SED-557/
3. https://unix.stackexchange.com/questions/481564/sedutils-vs-hpdarm-for-sed-hard-disks

But this does not seem to be well-documented elsewhere.

## Tiered storage

It's oh-so-very tempting to want tiered storage or caching with super-fast SSDs, but honestly, spend a little more money to not have this additional complexity.

For a NAS, it's a different story.

## mdadm

RAID1 can be useful to reduce downtime, and data loss between backups. Go for it, bearing in mind the cost.

## dm-integrity

Used with dm-crypt to detect bitrot.

The maximum speed of dm-integrity is on the order of \~100 MB/s on an NVMe drive that is capable of \~7 GB/s.

Therefore, this is a dead-end which is truly unfortunate.

(Also, discard is not supported.)

I ran a couple of benchmarks comparing encryption only with encryption and integrity.

PCIe 4.0 NVMe:

* 1.7 GB/s write with dm-crypt only, 374 MB/s with both (4.5x slower).

SATA SSD:

* 440 MB/s write with dm-crypt only, 179 MB/s with both (2.5x slower).

To automatically recover from bitrot, you will need RAID. You can always restore files from a backup.

## LVM

LVM can be incredibly useful:

1. Suddenly creating a new partition to install another OS.
2. Creating a emergency, temporary snapshot (but, apparently LVM is not great for this).
3. Transparently increasing storage by adding more disks.

However, the risk of the storage array failing increases with every disk. RAID must be used to prevent this.

## bcachefs

The ideal solution would be [bcachefs](https://bcachefs.org/) but it is far, far from feature-complete and battle-hardened.

## SMART

Monitoring disks.

TODO: Be smart, and do this.
