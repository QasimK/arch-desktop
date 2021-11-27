# Documents

## PDFs

```terminal
pacmatic -S --needed zathura
```

Plugin for PDF, ePub and OpenXPS (there are more plugins):

```terminal
pacmatic -S --asdeps zathura-pdf-mupdf
```

Set as default PDF reader:

```terminal
xdg-mime default org.pwmt.zathura.desktop application/pdf
```

Read the keyboard shortcuts with `man zathura`.

Consider `xpdf` (for encrypted PDFs), `okular` (for forms), `llpp`, or even `evince` (for forms).

Ref: <https://wiki.archlinux.org/title/PDF,_PS_and_DjVu>

Note: `zathura` tracks history in `~/.local/share/zathura`.

## Office

```
pacmatic -S --needed libreoffice-fresh-en-gb hunspell-en_gb hyphen-en
```

Consider poppler-data for pdf encodings??

## Calendar / Contacts

gcalcli
goobook
