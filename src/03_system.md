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

Configure `/etc/pacman.conf` to enable `Color`, `VerbosePkgLists`.


### Backup the local database

Backup the local pacman database when it changes to facilitate restore:

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
pacmatic -S --needed pacman-contrib
```

Automatically remove all versions of an uninstalled package:

`/etc/pacman.d/hooks/paccache-remove.hook`
```ini
[Trigger]
Operation = Remove
Type = Package
Target = *

[Action]
Description = Removing package cache for uninstalled packages...
When = PostTransaction
Exec = /usr/bin/paccache -ruk0
```

Keep only the latest three versions of each installed package:

`/etc/pacman.d/hooks/paccache-upgrade.hook`
```ini
[Trigger]
Operation = Upgrade
Type = Package
Target = *

[Action]
Description = Removing old cached packages...
When = PostTransaction
Exec = /usr/bin/paccache -rk3
```


### Reflector

Optimise the mirror list using `reflector`:

```sh
pacmatic -S --needed reflector`.
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
pacmatic -S --needed opendoas
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
pacmatic -S --needed tlp
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

`/etc/rc.local`
```txt
echo 0 > /sys/class/graphics/fbcon/cursor_blink
```

### Powertop

Unnecessary.
