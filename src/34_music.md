# Music

Spotify with `spotifyd` and `spotify-tui`.

## spotifyd

Creates a Spotify device (controllable via phone).

```sh
pacmatic -S --needed spotifyd
```

Configure: <https://spotifyd.github.io/spotifyd/config/File.html>

`~/.config/spotifyd/spotifyd.toml`.

```toml
[global]
username = "me"
password = "..."
# use_mpris = true
bitrate = 320
cache_path = "/home/me/.cache/spotifyd"
device_type = "computer"
```

Start the service:

```sh
systemctl --user enable --now spotifyd.service
```

## spotify-tui

Control Spotify from the desktop...

This and every other client is in the AUR. Sigh.
