# Framework Laptop

## Hardware

* **CPU** Intel 12th Gen i5-1240p
* **GPU** iGP
* **Screen** 13.5" 3:2 2256x1504px sRGB 400 nit
* **Battery** 55Wh 15.4V 3572mAh
* **Webcam** 1080p 60fps
* **Size** 297 x 229 x 15.9mm
* **Weight** 1.3 KG


## Configuration

For power savings:

`/etc/tlp.d/00-laptop.conf`
```ini
PCIE_ASPM_ON_BAT=powersupersave
```

`/etc/kernel/cmdline`
```txt
i915.enable_fbc=1 nvme.noacpi=1
```

In the UEFI.
