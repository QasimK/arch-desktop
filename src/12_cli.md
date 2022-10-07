# Essential CLI tools

The CLI tools are an excellent complement to a GUI.


## Scripting

Use `dash` for scripts because it has a faster start up time (1.5ms vs 3ms for `bash`).

```sh
pacman -S --asexplicit dash
```

Use `shellcheck` to check scripts for errors.

```sh
pacman -S --asexplicit shellcheck
```

Use `checkbashisms` to check for `sh` vs `bash` peculiarities:

```sh
pacman -S --asexplicit checkbashisms
```

Common scripting helpers:

```sh
pacman -S --asexplicit fzf
```


## Lock screen

I have found `swaylock` to actually be surprisingly unreliable. Instead use `physlock`:

```sh
pacman -S --asexplicit physlock
```

Lock with `physlock -m`.

Note: use the `-s` flag to disable sysrq hotkeys (if you have enabled them).

Create a script called `,lock`:

```sh
#!/usr/bin/dash
exec physlock -ms
```

(This will let us easily change this in the future if we want to.)

Ref: <https://old.reddit.com/r/swaywm/comments/n344ey/swaylock_alternatives/gx0jkt8/>


## Trash

A safer way to delete.

```sh
pacman -S --asexplicit trash-cli
```

Note: there are various commands starting with `trash*`!

Automatically delete after 30 days:

`~/.config/systemd/user/trash.service`
```ini
[Unit]
Description=Delete old trash

[Service]
Type=oneshot
ExecStart=/usr/bin/trash-empty -f 30
Nice=19
```

`~/.config/systemd/user/trash.timer`
```ini
[Unit]
Description=Empty trash daily

[Timer]
OnStartupSec=1 minute

[Install]
WantedBy=timers.target
```

```sh
systemctl --user enable --now trash.timer
```


## Opening files / setting default applications

```sh
pacman -S --asexplicit handlr
```

This is better than xdg-...


## Other

* `nnn` - file browser
