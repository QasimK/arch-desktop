# Terminal

We need a terminal emulator for the GUI.

## foot

```
pacman -S --asexplicit foot
pacman -S --asdeps foot-terminfo
```

TODO: Usage & config:

```
foot --server
footclient
```

### Set TERM (terminfo)


TODO: SSH - https://news.ycombinator.com/item?id=29561140

Copy it over if it cannot be installed.

```
S=my_server ; ssh $S 'mkdir -p ~/.terminfo/f/' ; scp /usr/share/terminfo/f/foot $S:~/.terminfo/f/foot
```

## abduco

TODO: Attach/Detach?
