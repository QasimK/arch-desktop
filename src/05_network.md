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

We need to resolve domain names.

Just set it in /etc/resolv.conf:

```
# LAN
# nameserver=192.168.1.1

# Cloudflare
nameserver=1.1.1.1
```

This does not cache DNS queries :(

It's possible to use more secure DNS resolvers:

* DoH (DNS-over-HTTPS)
* oDoH (Oblivious DNS-over-HTTPS)
* DNSCrypt

TODO: Note: dnscrypt-proxy has literally added support for ODoH, but waiting for new release. Who knew Arch Linux could be so behind :p

Use `getent hosts google.com` to test timing.

## WiFi crda

Configure the wireless regulation domain:

`/etc/conf.d/wireless-regdom`

---

systemd-resolved and systemd-networkd

* Configuration inside /etc/systemd/networkd
* Use `networkctl` to view
