# fscrypt

A directory, including its filenames, but excluding metadata like timestamps, the sizes and number of files and extended attributes, can be encrypted using `fscrypt`.

This is a simple solution to protect sensitive documents from malware or mistakes—to a certain extent. It can also be used to provide an additional level of isolation where Linux users are used as sort-of "profiles".

**WARNING:** The `/.fscrypt` directory is essential to be able to decrypt files. A recovery passphrase will be generated if the encrypted directory is not on the root partition which can be used to recover backups.
