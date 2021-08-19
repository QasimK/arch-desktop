# System config

1. SSHD harden
2. a. Pacman config changes
2. b. Pacman cache - https://qasimk.gitbooks.io/piserver-book/content/initial-setup.html
2. c. Simplified https://github.com/gs93/pakbak
3. fstrim timer
4. umask - https://wiki.archlinux.org/index.php/Umask#Set_the_mask_value
5. a. sysctl - kernel.yama.ptrace_scope=3,
5. b. `vm.swappiness=1`
5. c. `kernel.kexec_load_disabled=1`
6. Install crda - /etc/conf.d/wireless-regdom
7. Use `doas` instead of sudo.

TODO: lockdown mode

READ kernel messages - `journalctl -b`, it will spot errors!

TODO: Use linux-zen for desktop for better responsiveness (https://liquorix.net/)

TODO: Use paru instead of yay (next version).
