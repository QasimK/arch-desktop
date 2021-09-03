# Wayland/Sway

We are finally here.

<https://arewewaylandyet.com/>

`pacmatic -S --needed sway`

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

exec sway
```

Run it with `exec ,sway`.

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

`pacmatic -S --needed swayidle`

`~/.config/swayidle/config`

```
timeout 300 ',lock'
before-sleep ',lock'
after-sleep ',lock'
```

## Notifications

`pacmatic -S --needed dunst libnotify`

<https://www.galago-project.org/specs/notification/>

### App launcher

yofi?

### Screenshots

flameshot?

### Screen Sharing

### Screen Recording

### Status Bar
