# Secure boot

https://gist.github.com/umbernhard/d1f4a44430d6d21b3881652c7a7c9ae5

## Password-protect the firmware

Prevent modifications to UEFI settings with a password.

CMOS reset destroys this? Do we need TPM?

## Secure boot

Check the boot loader / kernel image signature.

Dual booting with Windows:

> Plain EFISTUB (https://wiki.archlinux.org/index.php/EFISTUB) allows turning the kernel image + initramfs + kernel command line into a single binary than can be signed with your own Secure Boot key (https://wiki.archlinux.org/index.php/Secure_Boot#Using_your_own_keys).

Look at sbupdate, sbctl, *dracut*

## Encrypted boot

There is no particular reason to do this.
