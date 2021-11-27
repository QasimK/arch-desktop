# Mounting

Encryption.

```sh
pacmatic -S --needed udisks2
```

I didn't get unlock to work.

```sh
udisksctl mount -b /dev/mapper/mycontainer
```


## ntfs-3g


## iPhone

See: <https://wiki.archlinux.org/title/IOS>

```sh
pacmatic -S --needed libimobiledevice
```

```
# pacmatic -S --asdeps base-devel
$ git clone https://aur.archlinux.org/packages/ifuse-git/
$ makepkg -sirc
# pacman -Qtdq | pacman -Rns -
```

Using:

```sh
ifuse ~/mnt/iphone --udid (idevicepair list | head -n1)
fusermount -u ~/mnt/iphone
```
