# System config

TODO: lockdown mode

READ kernel messages - `journalctl -b`, it will spot errors!

TODO: Use paru instead of yay (next version).

## Pacmatic Fix

Note: you may need a temporary fix for `pacmatic`:

<https://github.com/keenerd/pacmatic/issues/41>
<https://github.com/keenerd/pacmatic/pull/42/files>

Or, alternatively set the environment variable `rss_feed=https://archlinux.org/feeds/news/`.

## Time sync

```
systemctl enable --now systemd-timesyncd
timedatectl set-ntp true
```

## Pacman settings

Configure `/etc/pacman.conf` to enable `Color`, `CheckSpace`, `VerbosePkgLists`, and `ParallelDownloads = 5`.

Install `paccache`:

```
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
Exec = /usr/bin/tar --create --zstd --file /root/pacman-backup.zstd.tar --directory / var/lib/pacman/local
```

(This would have saved my hide!)

Optimise the `mirrorlist` mirrorlist using `reflector`: `pacmatic -S --needed reflector`.

`/etc/xdg/reflector/reflector.conf`

```
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

```
NoExtract = /etc/pacman.d/mirrorlist
```

### Package Stats

Consider opting-in to telemetry on package statistics:

<https://pkgstats.archlinux.de/>

Stats: <https://pkgstats.archlinux.de/fun>

## Trim

Enable weekly trim of filesystems.

```terminal
systemctl enable --now fstrim.timer
```

(Note this leaks empty spaces on encrypted drives.)

## Journald

Reduce the journal size because who really needs 4 GiB of logs?

`/etc/systemd/journald.conf.d/00-journal-size.conf`

```ini
[Journal]
SystemMaxUse=50M
```

## doas

Use `doas` instead of `sudo` because it is simpler.

```terminal
pacmatic -S --needed opendoas
```

Note: Consider not using this and opening a tty with root instead.

## Ananicy

Unfortunately, this is AUR.

## Safety features

Some free space that can be deleted if ever necessary.

```
truncate -s 500M /freespace
touch -- /-i && chmod 0444 -- /-i
```
