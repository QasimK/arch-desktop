# Video

## Playback (mpv)

```sh
pacman -S --asexplicit mpv yt-dlp
pacman -S --needed --asdeps atomicparsley

yt-dlp 'https://www.youtube.com/watch?v=LXb3EKWsInQ' -o 4k.webm
mpv 4k.webm
```

(This is a 1 GB 4K VP9 file.)

`~/.config/mpv/mpv.conf`
```ini
# Hardware-acceleration
vo=gpu
hwdec=vaapi
gpu-context=waylandvk
gpu-api=vulkan

# ICC
icc-profile=/etc/framework.icm
gamut-warning

# Faster seeks (over network)
demuxer-max-bytes=1000000000  # 1 GB
demuxer-max-back-bytes=10000000000  # 10 GB (hell yeah!)
network-timeout=10

# youtube-dl
ytdl-format='bestvideo[height<=?2160][fps<=?240]+bestaudio/best'

# youtube-dl (efficient): "mpv --profile=small"
[small]
ytdl-format='bestvideo[height<=?1080][fps<=?60]+bestaudio/best'
```

(The small profile can be aliased.)

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

## Recording

How do I record my screen?
