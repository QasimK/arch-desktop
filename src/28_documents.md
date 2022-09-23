# Documents

## PDFs

```sh
pacmatic -S --needed zathura
```

Plugin for PDF, ePub and OpenXPS (there are more plugins):

```sh
pacmatic -S --asdeps zathura-pdf-mupdf
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

Use `pdftk`.

```sh
pacmatic -S --needed pdftk
pacamtic -S --asdeps bcprov
```

(The latter dependency is to support signed/encrypted PDFs.)

## Office

```
pacmatic -S --needed libreoffice-fresh-en-gb hunspell-en_gb hyphen-en
```

Consider poppler-data for pdf encodings??

## Calendar / Contacts

gcalcli
goobook
