# Audio

`pacmatic -S alsa-utils`

Use `alsamixer` to explore your speakers and microphones. Find the right "card" with `F6`.

## Set default

`cat /proc/asound/modules`

Set the ordering:

`/etc/modprobe.d/alsa-conf.base`

```
options snd_hda_intel index=1,2
options snd_usb_audio index=3
```

Reboot for changes to take effect.

This is necessary because the default index (for "speakers" below will change on boot otherwise).

## Recording

See microphone properties (for the right `card2`) with:

```terminal
cat /proc/asound/card2/stream0
```

This gives us the format, rate(s) and number of channels.

We can create an alias for the microphone to make it (a bit) easier to use:

`~/.asoundrc`

```
# Alias: arecord -D mic -f S16_LE -r 48000 -c 1 record.wav
pcm.mic {
    type hw
    card 2
    device 0
}
```

Unfortunately, I have no idea how you can make those format/rates the default for any recording.

Record a sound with `arecord -D mic -f S16_LE -r 48000 -c 1 record.wav`.

## Speakers

See speaker properties (for the right `card1`) with:

```terminal
cat /proc/asound/card1/codec\#0
```

It is a lot of output, but you can parse for the rates and formats.

Set the playback device

`~/.asoundrc`

```
# Playback default
defaults.pcm.card 1
defaults.pcm.device 0
# Controller (alsamixer) default
defaults.ctl.card 1
```

Play the recording: `aplay record.wav`.

**NOTE: Do not forget to unmute the microphone and speakers with alsamixer**.

Or we could do `mpv record.wav`.

## Volume

Sending notifications

```terminal
notify-send -h STRING:synchronous:1 -h STRING:transient:1 -h INT:value:2 -u low -t 3000 -c device 'Volume'
```
