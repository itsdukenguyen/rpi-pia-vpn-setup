# Systemd Services for Automatic Startup

These services ensure **PIA VPN**, **SSH**, and **VNC** start automatically after every reboot.

---

## 1. PIA VPN Service

Create the service file:

```bash
sudo nano /etc/systemd/system/pia-vpn.service
```

## Paste this content:
```ini
[Unit]
Description=Private Internet Access VPN
After=network-online.target
Wants=network-online.target

[Service]
Type=simple
User=root
ExecStartPre=/usr/bin/piactl set allowlan true
ExecStartPre=/usr/bin/piactl login /home/pi/pia_login.txt
ExecStart=/usr/bin/piactl connect
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
```

## Enable and start:
```bash
sudo systemctl daemon-reload
sudo systemctl enable pia-vpn
sudo systemctl start pia-vpn
sudo systemctl status pia-vpn
```

## 2. SSH & VNC Services
```bash
# SSH
sudo systemctl enable --now ssh

# VNC (adjust @1 or @0 depending on your display)
sudo systemctl enable --now vncserver@1
```
## Check status:
```bash
systemctl status ssh
systemctl status vncserver@*
```

## Verification After Reboot:
```bash
piactl get connectionstate
sudo netstat -tulnp | grep -E ':22|:5900'
```