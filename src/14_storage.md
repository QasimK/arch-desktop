# Storage

Synchronising and sharing files with people and between devices.

With cloud storage, sensitive documents should be encrypted locally.


## Syncthing (sync files)

Synchronise files between devices using `syncthing`:

```sh
pacmatic -S --needed syncthing

systemctl --user enable --now syncthing.service
```

The web interface is available at `http://localhost:8384/`.


## rclone (cloud storage)

```sh
pacmatic -S --needed rclone
pacmatic -S --needed --asdeps fuse2
```


### Google Drive

The web documentation describes how to set this up.

Copy individual folders:

```sh
rclone copy --progress "drive:<folder>" "<folder>"
```

Mount whole drives:

```sh
rclone mount --vfs-cache-mode full "drive:" "<folder>"
```

* `vfs-cache-mode full` will buffer files to disk



## fscrypt (encrypt locally)

Encrypt a directory, including its filenames, but excluding metadata like timestamps, the sizes and number of files and extended attributes.

This is a simple solution to protect sensitive documents from malware or mistakes—to a certain extent. It can also be used to provide an additional level of isolation where Linux users are used as sort-of "profiles".

**WARNING:** The `/.fscrypt` directory is essential to be able to decrypt files. A recovery passphrase will be generated if the encrypted directory is not on the root partition which can be used to recover backups.



## CryFS (encrypt for cloud storage)

Encrypt files in cloud storage on desktop operating systems.

The [CryFs comparison table](https://www.cryfs.org/comparison) shows the main advantage over Veracrypt is not needing a statically-sized container file, and authenticated encryption (to prevent tampering).

`fscrypt` is not appropriate because it encrypts/decrypts files in-place which causes unnecessary and dangerous syncing.

**Note:** Ensure only one device has the encrypted folder mounted.

**Warning:** Data corruption is possible on power loss, system crashes, and multiple writers.

```sh
pacmatic -S --needed cryfs
```

Create an encrypted folder:

```sh
cryfs ~/encrypted ~/mountpoint
```

Mount an encrypted folder:

```sh
cryfs --foreground --fuse-option noatime ~/encrypted ~/mountpoint
```

See <https://www.cryfs.org/tutorial>.
