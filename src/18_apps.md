# Apps

## Torrent

Download torrents with `aria2`:

```sh
pacman -S --asexplicit aria2
```

It's simple to use:

```sh
aria2c --file-allocation=falloc --enable-mmap --check-integrity myfile.torrent
```

It can resume downloads, what could you want?

## Khal

TODO: Khal for calendar

```sh
pacman -S --asexplicit khal
pacman -S --needed --asdeps vdirsyncer
```

TODO: google with vdirsyncer?
