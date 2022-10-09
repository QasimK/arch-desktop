# Wayland/Sway (Desktop\Environment)

We are finally here.

<https://arewewaylandyet.com/>

```sh
pacman -S --asexplicit sway
usermod -aG seat me
```

## Start script

It's useful to have a start-up script with common environment variables

```sh
#!/usr/bin/dash
XDG_SESSION_TYPE=wayland
XDG_CURRENT_DESKTOP=sway
QT_QPA_PLATFORM=wayland
CLUTTER_BACKEND=wayland
SDL_VIDEODRIVER=wayland
MOZ_ENABLE_WAYLAND=1

exec dbus-run-session sway
```

Run it with `exec ,sway`.

`dbus-run-session` allows us to open multiple sways.

### Disable Accessibility Services

Stop the `at-spi-bus-launcher` process from starting (`firefox`):

`.pam_environment`
```
# Disable accessibility service
NO_AT_BRIDGE=1
```

`/etc/systemd/system/user@1000.service.d/override.conf`
```
[System]
NO_AT_BRIDGE=1
```

`/etc/pacman.conf`
```ini
NoExtract = usr/share/dbus-1/accessibility-services/org.a11y.*
NoExtract = usr/share/dbus-1/services/org.a11y.*
```

## Configuration

<https://github.com/swaywm/sway/wiki#configuration>

Configure your inputs and outputs.

```
man 5 sway-output
swaymsg -t get_outputs

man 5 sway-input
swaymsg -t get_inputs
```

TODO: xkb_options, layers, etc. This is all confusing.
    man xkeyboard-config

Use `libinput debug-events --show-keycodes` to get keyboard keys.

(THIS IS WRONG, YOU WANT `wev` but that is AUR!)

The common media keys are:

* `XF86VolumeMute`


## Lock screen

Configure a keyboard shortcut:

`~/.config/sway/config`
```
bindsym --release Ctrl+Shift+l exec ',lock'
```

(There is no need for `swayidle` to lock for you.)


## Notifications

`pacman -S --asexplicit dunst libnotify`

...


### App launcher

Just launch from terminal like so:

```sh
setsid &>/dev/null firefox
```

Create an alias to just type `s firefox`.


### Screenshots

```sh
pacman -S --asexplicit grim slurp swappy
pacman -S --needed --asdeps wl-clipboard otf-font-awesome
```

...


### Screen Recording

...
