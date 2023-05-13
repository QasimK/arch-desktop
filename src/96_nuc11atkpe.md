# Intel NUC 11 Essential (2022)

Manual

User Guide

Model: NUC11ATKPE
SKU: BNUC11ATKPE000

## HardwareW

* **CPU** Intel Pentium Silver Jasper Lake Pentium N6005 (4 cores) (2021)
* **GPU** iGPU Intel Jasper Lake UHD Graphics
* **RAM** 2 x DDR4-2993 1.2V SO-DIMM (up to 32 GiB)
* **Storage** M.2 2280/42 PCIe x2 Gen 3
* **Wireless** 1 x M.2 2230 Key E; Intel Wireless-AC 9462, 802.11ac, Dual Band, 2x2 Wi-Fi + Bluetooth 5.0
* **LAN** Realtek RTL8111H-CG Gigabit Ethernet Controller
* **Front Ports**
    * Front Panel Header
    * 2 x Front USB3.2 Gen 1
    * 3.5mm stereo out jack
    * 3.5mm headphone in jack
* **Back Ports**
    * DisplayPort 1.4 (4096x2160 at 60Hz)
    * HDMI 2.0b (4096x2160 at 60Hz)
    * 2 x USB 3.2 Gen 2
    * 2 x USB 2.0
    * RJ-45 Kensington Security Slot
    * 19V DC Input Jack
* **Internal Ports**
    * CR2032 battery
    * BIOS Security Jumper
* **Size** 135 x 36 x 115 mm

Pick your own RAM and Storage.

## UEFI

Set the harddrive start pre-delay to zero (it is pointless).

### UEFI Lockdown Mode

Consult the manual to change the jumper to lock down the UEFI.

No POST hotkeys (F2 for setup; F10 for boot menu).
No power button menu.

### UEFI Update

Download the .cab file from the Intel Website, place on to a USB stick, and
press F7 on power-up to enter the UEFI update menu.


## Power Consumption

* **Base + WiFi** 3.0 W
* **Keyboard** +0.2 W
* **Mouse** +0.4 W
* **HDMI** +1.5 W
* **Syncthing** +2.5-3.5 W (when actively syncing)
* **CPU Stress Test** 25.5 W

The base power consumption is with a plain Arch Linux installation with many
UEFI features turned off except WiFi which is connected to a network. In
particular, the Bluetooth, SATA port, VT-d, and TPM features are disabled

I have not tested disabling WiFi, or with the Ethernet port.

There is no difference between USB2 and USB3 power consumption for peripherals.

There is no difference to power consumption whether the monitor is switched to
the HDMI input or not so long as it is connected.

The overall power consumption with all of the above plugged in was 5.3 W which
is slightly higher than the sum of the individual components due to rounding.

Thus using the NUC in headless mode saves ~£7/year with 2022 electricity prices
of 0.39 p/kWh.
