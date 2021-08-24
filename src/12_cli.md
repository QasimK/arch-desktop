# Essential CLI tools

The CLI tools are an excellent complement to a GUI.

## Dash

Use dash for scripts because it has a faster start up time (1.5ms vs 3ms).

```
pacman -S --needed dash
```

## Lock screen

I have found `swaylock` to actually be surprisingly unreliable. Instead use `physlock`:

```
pacman -S --needed physlock
```

Lock with `physlock -m`.

Note: use the `-s` flag to disable sysrq hotkeys (if you have enabled them).

Create a script called `,lock`:

```
#!/usr/bin/dash
exec physlock -m
```

(This will let us easily change this in the future if we want to.)

Ref: <https://old.reddit.com/r/swaywm/comments/n344ey/swaylock_alternatives/gx0jkt8/>

## Other

* `mosh`, `fish`, `vim`
* `nnn` - file browser
* `trash-cli` - it's safer!
* `desktop-file-utils` - for creating .desktop files
