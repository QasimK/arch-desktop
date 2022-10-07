# GPU

## Intel

```sh
pacman -S --asexplicit mesa vulkan-intel intel-media-driver
```

## AMD

This will vary depending on your GPU manufacturer.

Hardware acceleration for videos etc.

```sh
pacman -S --asexplicit mesa vulkan-radeon libva-mesa-driver mesa-vdpau
```

(`amdvlk` is pretty much the same as `vulkan-radeon` but has a larger install size)

Ref: <https://wiki.archlinux.org/title/AMDGPU>

Ref: <https://wiki.archlinux.org/title/Hardware_video_acceleration#ATI/AMD>


## Testing

Test Vulkan:

```sh
pacman -S --asexplicit vulkan-tools
vulkaninfo
```

Test VAAPI:

```sh
pacman -S --asexplicit lib-va-utils
vainfo
```
