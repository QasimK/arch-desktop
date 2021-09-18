# Images

## View images

Use `imv`:

`pacmatic -S --needed imv`

## Screen capture

We can use a trio of tools to create a simple take-and-edit workflow:

1. Select a portion of the screen to take a screenshot of
2. Immediately edit the screenshot (highlighting and adding text)
3. Finally, either copy it to the clipboard or save it to a file

```sh
pacmatic -S --needed grim slurp swappy
pacmatic -S --asdeps wl-clipboard otf-font-awesome
```

Configure keyboard shortcut:

`~/.config/sway/config`

```
bindsym Print exec ',screenshot'
```

Reusable script to take the screenshot:

`~/s/,screenshot`

```
#!/usr/bin/dash
set -eu
grim -g "$(slurp)" - | swappy -f -
```

Configure default save directory:

`~/.config/swappy/config`:

```
[Default]
save_dir=$XDG_PICTURES_DIR
```
