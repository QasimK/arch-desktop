# Swap

1. Don't bother, buy more RAM instead.

2. Use in-memory zswap or zram.

3. We want to use swap on a newly-encrypted partition on each boot. This will protect sensitive keys that end up in memory. Possible downsides include: hibernate (suspend-to-ram) not working.

If it is used:

`/etc/sysctl.d/99-swappiness.conf`: `vm.swappiness=1`
