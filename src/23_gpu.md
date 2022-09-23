## GPU

## Intel

```sh
pacmatic -S --needed mesa vulkan-intel intel-media-driver
```

## AMD

This will vary depending on your GPU manufacturer.

Hardware acceleration for videos etc.

```sh
pacmatic -S --needed mesa vulkan-radeon libva-mesa-driver mesa-vdpau
```

(`amdvlk` is pretty much the same as `vulkan-radeon` but has a larger install size)

Ref: <https://wiki.archlinux.org/title/AMDGPU>

Ref: <https://wiki.archlinux.org/title/Hardware_video_acceleration#ATI/AMD>

## Test

```sh
pacmatic -S --needed vulkan-tools
```

```sh
vulkaninfo
```

```sh
pacmatic -S --needed lib-va-utils
```

```sh
vainfo
```
