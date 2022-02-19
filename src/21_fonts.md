## Font

TODO: https://old.reddit.com/r/archlinux/comments/sltmoi/update_changed_the_font/

We need a basic fallback font:

* ttf-dejavu (basic font families: serif, sans-serif, and monospace)

We need to replace some commonly used fonts.

* ttf-croscore (MS Arial, Times New Roman, and Courier New)
* ttf-caladea (MS Cambria)
* ttf-carlito (MS Calibri)
* tex-gyre-fonts (Helvetica, Palatino, Bookman and others)

We need a font for coding:

* ttf-fira-code (coding with ligatures)

We need a fallback font for every other Unicode symbol:

* noto-fonts (full coverage - cjk, emoji for fallback)

There are many other substitutes in the AUR.

Ref: <https://wiki.archlinux.org/index.php/Fonts>
Ref: <https://wiki.archlinux.org/title/Metric-compatible_fonts>

## Configuration

`pacmatic -S --needed fontconfig`

```
cd /etc/fontconf/conf.d
ln -s /usr/share/fontconfig/conf.avail/09-autohint-if-no-hinting.conf
ln -s /usr/share/fontconfig/conf.avail/10-sub-pixel-rgb.conf
ln -s /usr/share/fontconfig/conf.avail/11-lcdfilter-default.conf
```

Ref: <https://wiki.archlinux.org/title/Font_configuration#LCD_filter>
