# Laptop-specific configuration

## Backlight

Control the backlight:

`/usr/bin/,brightness`
```sh
#!/usr/bin/dash
# Set the brightness
set -eu

max=$(cat /sys/class/backlight/intel_backlight/max_brightness)
val=$((max * $1 / 100))

echo "Setting display brightness to $val/$max"
echo "$val" >> /sys/class/backlight/intel_backlight/brightness
```

Allow unprivileged users to control the backlight:

```sh
groupadd backlight
usermod -aG backlight me
```

`/etc/udev/rules.d/00-backlight-permissions.rules`
```txt
ACTION=="add", SUBSYSTEM=="backlight", KERNEL=="intel_backlight", RUN+="/usr/bin/chgrp backlight /sys/class/backlight/intel_backlight/brightness"
ACTION=="add", SUBSYSTEM=="backlight", KERNEL=="intel_backlight", RUN+="/usr/bin/chmod g+w /sys/class/backlight/intel_backlight/brightness"
```
