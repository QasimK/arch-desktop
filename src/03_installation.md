# Installation

Follow the [Arch Wiki](https://wiki.archlinux.org/title/Installation_guide) using the specific commands below.

Storage Commands: <https://qasimk.io/2020/borg-backup/>


Basically as above

pacstrap: base linux linux-lts linux-firmware amd-ucode vim tmux htop man-db man-pages texinfo iwd

crda - iwd
python
lm_sensors
lsof
strace



cryptroot = e6e67e3d-c904-254b-a433-4a982d3be70c (PARTUUID)
root = 1ee89039-468a-45e3-bc6b-80ae9ea6366a (UUID)

```terminal
efibootmgr \
    --disk /dev/nvme0n1 \
    --part 1 \
    --create \
    --label "Arch Linux" \
    --loader /vmlinuz-linux \
    --verbose \
    --unicode 'cryptdevice=PARTUUID=e6e67e3d-c904-254b-a433-4a982d3be70c:root root=UUID=1ee89039-468a-45e3-bc6b-80ae9ea6366a rw initrd=\amd-ucode.img initrd=\initramfs-linux.img'
```



Set perm flags;

cryptsetup --persistent --perf-no_read_workqueue --perf-no_write_workqueue  open ...

## Installation
