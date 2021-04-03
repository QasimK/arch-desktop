# Backup

<https://qasimk.io/2020/borg-backup/>

Possible enhancements:

1. Mount and decrypt USB drive (either systemd or script)
2. Ask for a password in the script and use it for each command
3. Use LVM to create a temporary snapshot

Veracrypt - disable "preserve modification timestamp of file containers".

## Borg

Use par2 for data recovery?

We already protect against bit-rot, but cannot recover if it happens.

Use xattrs for mtime checks and a different directory for storage.
