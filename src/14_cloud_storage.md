# Cloud Storage

Use cloud storage as a mirror of local storage rather than as a replacement (unless you're talking about terabytes of data...).

Sensitive documents should be encrypted locally.

## Resilio

TODO: PKGBUILD has a bug where it doesn't set chmod o+r for `/etc/rslsync.conf`.

Follow the setup instructions.

Sample config:

`~/.config/rslsync/rslsync.conf`

```
{
    "device_name": "My Sync Device"
  , "storage_path": "/home/me/.local/share/rslsync"
  , "pid_file" : "/home/me/.cache/rslsync/resilio.pid"

    // WebUI Folder browser start location
  , "directory_root" : "/home/me/"
    // Restrict folder creation to directory_root
  , "directory_root_policy" : "belowroot"

    // use UPnP for port mapping
  , "use_upnp" : true

    // Limits in kB/s (0 - no limit)
  , "download_limit" : 0
  , "upload_limit" : 0

  , "webui": {
        // Remove "listen" field to disable WebUI
        "listen" : "127.0.0.1:8888"
      , "login": "me"
      , "allow_empty_password": true

        // Whitelist folders relative to directory_root
        // Only these can be shown to the user or have folders added
      , "dir_whitelist": [
            "Documents"
        ]
    }

    // Advanced preferences
    // https://help.resilio.com/hc/articles/207371636
  , "send_statistics": false
  , "share_file_ttl": 7
  , "keep_expired_transfer_days": 3
  , "show_service_disk_thread": true
  , "parallel_indexing": true
  , "disk_low_priority": true
}
```

Create:

```sh
mkdir -p ~/.local/share/rslsync
mkdir -p ~/.cache/rslsync
```

Start:

```sh
systemctl --user enable --now rslsync.service
```

NOTE: The WebUI will prompt you for a name—this is your _identity_. It can be the same across all your devices.

Reduce logging under Advanced settings.

## Dropbox

Follow the setup instructions: <https://wiki.archlinux.org/title/Dropbox>.

Except. To put the Dropbox folder somewhere other than the root of the home directory, we must set the `HOME` environment variable to the parent directory where we want the Dropbox folder.

```sh
systemctl --user edit dropbox.service
```

```ini
[Service]
Environment="HOME=/home/me/Documents"
```

```sh
systemctl --user enable --now dropbox.service
```

There is a `dropbox.py` CLI script that I couldn't get working. Oh well, we don't really need to interact with it now.

## CryFS

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
