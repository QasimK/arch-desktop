# Torrent

Download torrents with `aria2`:

```sh
pacman -S --asexplicit aria2
```

It's simple to use:

```sh
aria2c --file-allocation=falloc --enable-mmap --check-integrity myfile.torrent
```

It can resume downloads, what could you want?
