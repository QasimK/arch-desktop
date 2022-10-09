# Post-installation System Configuration

Read kernel messages with `journalctl -b` — you will spot problems!

## Swap

I don't bother with it.


## Pacmatic Fix

**Note: you may need a temporary fix for `pacmatic`**

<https://github.com/keenerd/pacmatic/issues/41>
<https://github.com/keenerd/pacmatic/pull/42/files>

Or, alternatively set the environment variable `rss_feed=https://archlinux.org/feeds/news/`.

## Time sync

```sh
systemctl enable --now systemd-timesyncd
timedatectl set-ntp true
```

## Pacman settings

Configure `/etc/pacman.conf` to enable `Color`, `VerbosePkgLists`, and `ParallelDownloads`.


### Backup the local database

Backup the local pacman database when it changes to facilitate restore:

```sh
mkdir -p /root/backups/var/lib/pacman/local

`/etc/pacman.d/hooks/pacbackup.hook`
```ini
[Trigger]
Operation = Install
Operation = Upgrade
Operation = Remove
Type = Package
Target = *

[Action]
Description = Backing up database...
When = PostTransaction
Exec = /usr/bin/tar --create --zstd --file /root/backups/pacman-db.zstd.tar --directory / var/lib/pacman/local
```

(NOTE: Space at the start of `/ var/lib/pacman/local` is deliberate.)


### Clean-up cached files

Install `paccache`:

```sh
pacman -S --asexplicit pacman-contrib
systeml enable --now paccache.timer
```

The timer will clean the local store of packages weekly and keep only the
three latest versions of each package.


### Reflector

Optimise the mirror list using `reflector`:

```sh
pacman -S --asexplicit reflector`.
```

`/etc/xdg/reflector/reflector.conf`
```txt
--save /etc/pacman.d/mirrorlist
--protocol https
--country 'United Kingdom'
--latest 5
--sort rate
--ipv4
```

Enable the weekly timer `systemctl enable reflector.timer`.

Ignore new mirrorlist files:

`/etc/pacman.conf`
```ini
NoExtract = etc/pacman.d/mirrorlist
```


### Ignore common pacnews

```ini
NoExtract = etc/locale.gen
```


## Trim

Enable weekly trim of filesystems.

```sh
systemctl enable --now fstrim.timer
```


## Journald

Reduce the journal size because who really needs 4 GiB of logs?

`/etc/systemd/journald.conf.d/00-journal-size.conf`

```ini
[Journal]
SystemMaxUse=100M
```

## doas

Use `doas` instead of `sudo` because it is simpler.

```sh
pacman -S --asexplicit opendoas
```


## Ananicy

Unfortunately, this is AUR.


## Safety features

Some free space that can be deleted if ever necessary:

```sh
truncate -s 500M /freespace
```

Prevent `rm`'ing root:

```sh
touch -- /-i && chmod 0444 -- /-i
```

## Power-savings (Laptop)

### UEFI

* Disable unnecessary components: fingerprint reader, etc.
* Set a battery limit to preserve the longevity of the battery.


### TLP

The primary tool is `tlp`:

```sh
pacman -S --asexplicit tlp
```

```sh
systemctl enable --now tlp.service
```

This will automatically configure the system between being plugged-in and running on battery. It's fire-and-forget.

Use `tlp-stat -b` to see that state of the battery.

This parameter helps with the Framework laptop:

`/etc/tlp.d/00-laptop.conf`
```ini
PCIE_ASPM_ON_BAT=powersupersave
```

### Kernel

These kernel parameters help with the Framework laptop:

`/etc/kernel/cmdline`
```txt
i915.enable_fbc=1 nvme.noacpi=1
```

### Cursor

Stop the cursor from blinking (yes, it makes a measurable difference!):

`/etc/tmpfiles.d/cursor_blink.conf`
```txt
w /sys/class/graphics/fbcon/cursor_blink - - - - 0
```

### Powertop

Unnecessary.
