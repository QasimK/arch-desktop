# Terminal

We need a terminal emulator for the GUI.

`foot` looks excellent but it's only in the AUR for now.

Two alternatives:

* ~~`termite`~~ is dead!
* `alacritty`

`pacmatic -S --needed alacritty`

(note: this installs some X dependencies.)

## Set TERM (terminfo)

TODO: SSH - https://news.ycombinator.com/item?id=29561140

```
S=my_server ; ssh $S 'mkdir -p ~/.terminfo/f/' ; scp /usr/share/terminfo/f/foot $S:~/.terminfo/f/foot
```

## foot

```
pacmatic -S --needed foot
pacmatic -S --asdeps foot-terminfo
```

TODO: Usage & config:

```
foot --server
footclient
```

## Alacritty

Select text: `<ctrl>-<shift>-<space>`

* v (character)
* alt-v (semantic)
* shift-v (line)
* ctrl-v (block)
* y - copy selection

Search text: ctrl-shift-f, ctrl-shift-b

Spawn new instances in the same directory with ctrl-shift-enter:

`.config/alacritty/alacritty.yml`

```yaml
key_bindings:
  - { key: Return,   mods: Control|Shift, action: SpawnNewInstance }
```

## abduco

TODO: Attach/Detach?
