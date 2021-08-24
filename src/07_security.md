# Security settings

There are various security settings that can be done. These are all optional.

<https://wiki.archlinux.org/title/Security>

It's important to remember this XKCD <https://xkcd.com/1200/>.


## umask

`/etc/profile`

```
umask 027
```

## ptrace

`/etc/sysctl.d/00-ptrace-scope.conf`

```
# Restrict ptrace to root
kernel.yama.ptrace_scope = 2
```

## kexec

`/etc/sysctl.d/00-kexec-restrict.conf`

```
# Restrict replacing current kernel
kernel.kexec_load_disabled = 1
```

## bpf

`/etc/sysctl.d/00-bpf-harden.conf`

```
# Prevent spraying attacks from non-privileged code
net.core.bpf_jit_harden = 1
```
