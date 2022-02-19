# Essential CLI tools

The CLI tools are an excellent complement to a GUI.

## Scripting

Use `dash` for scripts because it has a faster start up time (1.5ms vs 3ms for bash).

```terminal
pacmatic -S --needed dash
```

Use `shellcheck` to check scripts for errors.

```terminal
pacmatic -S --needed shellcheck
```

Use `checkbashisms` to check for `sh` vs `bash` peculiarities:

```terminal
pacmatic -S --needed checkbashisms
```

## Lock screen

I have found `swaylock` to actually be surprisingly unreliable. Instead use `physlock`:

```terminal
pacmatic -S --needed physlock
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

## Other

* `mosh`, `fish`, `vim`
* `nnn` - file browser
* `trash-cli` - it's safer!
* `desktop-file-utils` - for creating .desktop files?
