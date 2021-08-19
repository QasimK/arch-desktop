# Dual boot with Windows

Always use different disks - it's just easier.

Use UEFI's boot menu to switch between the systems. There is no need to have a separate boot loader.

Configure Windows to use UTC for UEFI clock:

1. Disable internet updates in Window settings
2. Use UTC for the UEFI clock by creating the file `fix.reg`

```reg
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation]
     "RealTimeIsUniversal"=hex(b):01,00,00,00,00,00,00,00
```
