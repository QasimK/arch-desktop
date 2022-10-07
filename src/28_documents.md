# Documents

## PDFs

```sh
pacman -S --asexplicit zathura
```

Plugin for PDF, ePub and OpenXPS (there are more plugins):

```sh
pacman -S --asdeps zathura-pdf-mupdf
```

Set as default PDF reader:

```sh
xdg-mime default org.pwmt.zathura.desktop application/pdf
```

Read the keyboard shortcuts with `man zathura`.

Consider `xpdf` (for encrypted PDFs), `okular` (for forms), `llpp`, or even `evince` (for forms).

Ref: <https://wiki.archlinux.org/title/PDF,_PS_and_DjVu>

Note: `zathura` tracks history in `~/.local/share/zathura`.


### Modifying PDFs

Consider `qpdf` (lightweight), or `mupdf-tools`.

OLD:

Use `pdftk`.

```sh
pacman -S --asexplicit pdftk
pacamtic -S --asdeps bcprov
```

(The latter dependency is to support signed/encrypted PDFs.)

## Office

```
pacman -S --asexplicit libreoffice-fresh-en-gb hyphen-en hunspell-en_gb mythes-en
pacman -S --needed --asdeps hunspell hyphen libmythes
```

Consider poppler-data for pdf encodings??


## Calendar / Contacts

gcalcli
goobook
