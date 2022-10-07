# Mounting

Encryption.

```sh
pacman -S --asexplicit udisks2
```


## ntfs-3g

???


## iPhone

See: <https://wiki.archlinux.org/title/IOS>

```sh
pacman -S --asexplicit libimobiledevice
```

```
# pacman -S --asdeps base-devel
$ git clone https://aur.archlinux.org/packages/ifuse-git/
$ makepkg -sirc
# pacman -Qtdq | pacman -Rns -
```

Using:

```sh
ifuse ~/mnt/iphone --udid (idevicepair list | head -n1)
fusermount -u ~/mnt/iphone
```
