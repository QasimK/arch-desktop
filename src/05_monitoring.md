# Monitoring

## Monitoring Tools

### SMART

TODO: Be smart and write this section.


### htop

Monitor CPU + MEM + DISK + NET.


### Intel GPU

```sh
pacman -S --asexplicit intel-gpu-tools

intel_gpu_top
```


### AMD GPU

Use `radeontop`.


### Power & Battery

```sh
tlp-stat -b
```


## Controlling Resource usage

Use `cpulimit` to limit cpu core usage of a process.

Use `nice` and `ionice` to adjust cpu and io priority of a process.

NOTE: autogroup! nice will not work. ionice is placebo for ssds.


## Stress Testing

### CPU

```sh
pacman -S --asexplicit stress

stress --cpu 12 --timeout 60
```
