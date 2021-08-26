# Video

We'll want to configure `mpv` for optimal settings.

## Playback (mpv)

```terminal
pacman -S --needed mpv youtube-dl
youtube-dl 'https://www.youtube.com/watch?v=LXb3EKWsInQ' -o 4k.webm
mpv 4k.webm
```

(This is a 1 GB 4K file.)

`~/.config/mpv/mpv.conf`

```
# TODO: My config goes here
```

(Get an ICC profile if you have a non-sRGB display, if you can.)

`~/.config/mpv/input.conf`

```
LEFT no-osd seek -1
RIGHT no-osd seek 1

WHEEL_DOWN no-osd seek -1
WHEEL_UP no-osd seek +1

Shift+LEFT seek -5
Shift+RIGHT seek 5

DOWN seek -60
UP seek +60

Shift+DOWN seek -360
Shift+UP seek +360

DEL run 'trash "${path}"'
```

Keys: <https://github.com/mpv-player/mpv/blob/master/etc/input.conf>

Ref: <https://mpv.io/manual/stable/#video-output-drivers-vo>
Ref: <https://wiki.archlinux.org/title/Mpv#High_quality_configurations>

Note: Hardware-accelerated decoding can be overloaded if the decoding is too complex or the decoding units are being used by something else including other videos.

TODO: profile for fast playback in this case.

## Recording

How do I record my screen?
