# Create a new user

```terminal
pacman -S --needed xdg-user-dirs
useradd --create-home --shell /usr/bin/fish me
passwd me
```

## Auto-login

`systemctl edit getty@tty1.service`

```ini
[Service]
ExecStart=
ExecStart=-/usr/bin/agetty --autologin me --noclear %I $TERM
```
