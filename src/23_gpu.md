## GPU (AMD)

This will vary depending on your GPU manufacturer.

Hardware acceleration for videos etc.

```terminal
pacman -S --needed mesa vulkan-radeon libva-mesa-driver mesa-vdpau
```

(`amdvlk` is pretty much the same as `vulkan-radeon` but has a larger install size)

Ref: <https://wiki.archlinux.org/title/AMDGPU>

Ref: <https://wiki.archlinux.org/title/Hardware_video_acceleration#ATI/AMD>
