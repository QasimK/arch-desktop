# Swap

1. Don't bother, buy more RAM instead

2. Use in-memory zram if you can't buy more RAM.

2. Use swap on video RAM...

3. If you really need swap on a disk, use zswap.

4. We want to use swap on a newly-encrypted partition on each boot. This will protect sensitive keys that end up in memory. Possible downsides include: hibernate (suspend-to-disk) not working.

Don't use zram with swap because of LRU inversion (most recently swapped data goes to slow disk if zram is full of old inactive stuff.)

If it is used, for increased responsiveness, use a large swap with

`/etc/sysctl.d/99-swappiness.conf`: `vm.swappiness=1`

(still relevant for SSD???)

Or a small swap with the default swappiness.
