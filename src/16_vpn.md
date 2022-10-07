# VPN

VPNs vary, but this is a generic way to connect to a WireGuard VPN.

`pacman -S --asexplicit wireguard-tools`

Generate a WireGuard configuration file `vpn.conf`. This is out-of-scope of this guide.

## WireGuard Network Namespace

```
# ip netns add nsvpn
# ip link add wgvpn type wireguard
# ip link set wgvpn netns nsvpn
# ip netns exec nsvpn wg setconf wgvpn /etc/wireguard/vpn.conf
# ip netns exec nsvpn ip <ADDRESS> add address/32 dev wgvpn
# ip netns exec nsvpn ip link set mtu 1420 dev wgvpn
# ip netns exec nsvpn ip route add default dev wgvpn
```

Note: remove the address line from the WireGuard configuration file.

Configure the DNS resolver to prevent DNS leaks:

`/etc/netns/nsvpn/resolv.conf`

```
nameserver 1.1.1.1
```

Use the VPN's DNS server here, or another one.

## doas

`/etc/doas.conf`

```
permit nopass nolog keepenv me as root cmd /usr/bin/ip args netns exec nsvpn su me
```

## Scripts

Open a shell inside the network namespace:

`,vpnshell`

```sh
#!/usr/bin/dash
exec doas /usr/bin/ip netns exec nsvpn su me
```

Check if we're in a network namespace:

```sh
netns="$(ip netns identify)"
if [ "$netns" != "nsvpn" ]; then
    echo "Run in the nsvpn network namespace!"
    exit 1
fi
```
