# Backup

<https://qasimk.io/2020/borg-backup/>

Possible enhancements:

1. Mount and decrypt USB drive (either systemd or script)
2. Ask for a password in the script and use it for each command
3. Use LVM to create a temporary snapshot

Veracrypt - disable "preserve modification timestamp of file containers".

## Borg

Use par2 for data recovery?

We already protect against bit-rot using dm-integrity, but cannot recover if it actually happens.

Use xattrs for mtime checks and a different directory for storage.

## Bitrot

The checksum is stored with the file metadata, and can be manually checked at any time.

We are probably better off with using a cshatag approach.
Store a checksum/mtime of each file in extended attributes.
Run the checker manually before every backup.

NVMe read @ 6.9 GB/s => 500 GB in 72s
SSD read @ 0.5 GB/s => 4000 GB in 2 hours

Recover file from backup only. Error exit -> Prevent backup.

md5 = 138240/3s 16k
sha1 = 315856/3s 16k ~~ 1.6 GB/s
sha256 = 249840/3s 16k
