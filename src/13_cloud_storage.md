# Cloud Storage

Use cloud storage as a mirror of local storage rather than as a replacement (unless you're talking about terabytes of data...).

Sensitive documents must be encrypted locally.

[CryFs][cryfs-compare] is one possible solution. The comparison shows the main advantage over Veracrypt is not needing a statically-sized container file, and authenticated encryption (to prevent tampering).

**Warning:** Data corruption is possible on power loss, system crashes, and multiple writers.

Alternative: https://cryptomator.org/

[cryfs-compare]: https://www.cryfs.org/comparison
