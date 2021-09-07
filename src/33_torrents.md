# Torrent

Download torrents with rtorrent:

`pacmatic -S --needed rtorrent`

## Target the app with Sway app_id

```sh
#!/usr/bin/dash
alacritty --title rtorrent --class rtorrent -e nice -n19 ionice -n7 rtorrent
```

## Issues

### Random Freezes

It is due to the DNS. Set up a local DNS cache.

```
network.http.dns_cache_timeout.set = 3600
```

https://github.com/rakshasa/rtorrent/issues/1075
https://github.com/rakshasa/rtorrent/issues/180

Consider a variant on https://github.com/vi/dnscache.

TODO: Basically, an in-memory dumb cache that forwards to a real DNS server.
