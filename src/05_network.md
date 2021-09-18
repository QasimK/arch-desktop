# Network

Use iwd for wireless. `iwctl` cli.

Setup iwd config to enable built-in DHCP.

vim /etc/iwd/main.conf.

But since it's a desktop, just assign a static one. We'll need to add a static route as well then.

Note: static config is not saved across reboots. So don't actually do this :)

## Route

Static (not recommended):

```
ip route add 192.168.121.1 dev wlan0
ip route add default via 192.168.121.1 dev wlan0
```

## IP Address

Static (not recommended):

```
ip address add 192.168.121.2/32 broadcast + dev wlan0
```

## DNS

We need to resolve domain names. A simple configuration like the following has problems.

`/etc/resolv.conf`

```
# LAN
# nameserver=192.168.1.1

# Cloudflare
nameserver=1.1.1.1
```

* DNS queries are not cached - every single lookup involves a network request.
* DNS queries have no privacy.

Instead, use `dnscrypt-proxy`:

```sh
pacmatic -S --needed dnscrypt-proxy
```

There are a number of options like DoH (DNS-over-HTTPS), oDoh (Oblivious DoH), or DNSCrypt. We will use oDOH.

`/etc/dnscrypt-proxy/dnscrypt-proxy.toml`

```
# Note: be sure to set other servers to false
doh_servers = false
odoh_servers = true

# Filters
block_ipv6 = true

# Cache
cache_size = 1000000
cache_min_ttl = 3600

# Servers - uncomment oDoH servers and relays
# ...

# Routes - following routes are not optimal, but it is quick to set up
routes = [
    { server_name="*", via=[*] }
]
skip_incompatible = true
```

```sh
systemctl enable --now dnscrypt-proxy.service
````

We can test timing and caching with `time getent hosts google.com`.

## WiFi crda

Configure the wireless regulation domain:

`/etc/conf.d/wireless-regdom`

---

systemd-resolved and systemd-networkd

* Configuration inside /etc/systemd/networkd
* Use `networkctl` to view

## Wireguard (personal vpn)

Server setup:

<https://qasimk.gitbooks.io/piserver-book/content/personal-vpn-wireguard.html>

```sh
systemctl enable --now wgquick@...
```

## Samba Mounts

Certain mount options like `credentials` require `cifs-utils`:

```sh
pacmatic -S --needed cifs-utils
```

Example mount file:

```ini
[Unit]
Description=myserver/myshare

[Mount]
What=//192.168.1.100/MyShare
Where=/mnt/myserver/myshare
Type=cifs
Options=rw,file_mode=0640,dir_mode=0750,uid=me,gid=me,credentials=/etc/mnt-myserver.credentials
TimeoutSec=5s
```

Example automount file:

```ini
[Unit]
Description=automount myserver/myshare

[Automount]
Where=/mnt/myserver/myshare
TimeoutIdleSec=1m

[Install]
WantedBy=multi-user.target
```
