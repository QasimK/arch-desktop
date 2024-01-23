# Framework Laptop

## Hardware

* **CPU** Intel 12th Gen i5-1240p (4p+8e cores)
* **GPU** iGP
* **RAM** 2 x DDR4 SODIMM
* **Screen** 13.5" 3:2 2256x1504 px sRGB 400 nit
* **Storage** M.2 2280
* **Battery** 55Wh 15.4V 3572mAh; 80% capacity after 1000 cycles
* **Webcam** 1080p 60fps with hardware kill-switch
* **Wireless** Intel AX210 WiFi 6E and Bluetooth 5.2
    * Has problems...
* **Speakers** 2 x 2 W speakers with 5cc backvolume
* **Microphones** Dual MEMS with hardware kill-switch
* **Keyboard** 1.5mm key travel with backlight
* **Touchpad** 115 x 77 mm
* **Size** 297 x 229 x 15.9 mm
* **Weight** 1.3 KG
* **Cooling** 30 W continuous load
* **Ports** 4 x USB-C (modules) + 3.5mm headset jack

Pick your own RAM and SSD.


## Power Savings

The USB-A, microSD, HDMI modules all consume extra battery when plugged in,
particularly for 11th & 12th Gen Intel CPUs.

For power savings on battery and performance on A/C:

`/etc/tlp.d/00-laptop.conf`
```ini
PCIE_ASPM_ON_AC=default
PCIE_ASPM_ON_BAT=powersupersave

CPU_SCALING_GOVERNOR_ON_AC=performance
CPU_SCALING_GOVERNOR_ON_BAT=powersave

CPU_ENERGY_PERF_POLICY_ON_AC=performance
CPU_ENERGY_PERF_POLICY_ON_BAT=power

CPU_BOOST_ON_AC=1
CPU_BOOST_ON_BAT=0

CPU_HWP_DYN_BOOST_ON_AC=1
CPU_HWP_DYN_BOOST_ON_BAT=0
```

`/etc/kernel/cmdline`
```txt
nowatchdog nmi_watchdog=0 i915.enable_fbc=1 nvme.noacpi=1
```

In the UEFI disable the fingerprint reader.

It is not possible to disable bluetooth in the UEFI.
