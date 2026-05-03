# Raspberry Pi 4 - PIA VPN with Persistent SSH & VNC Access

**Project Goal**: Run Private Internet Access (PIA) VPN on `rpi-torrent` (`192.168.10.115`) while maintaining full **local SSH (port 22)** and **VNC (port 5900)** access from the Management VLAN (`192.168.1.0/24`) and Clients VLAN (`192.168.30.0/24`) — even after reboots.

---

## Features

- iptables-based split tunneling (SSH & VNC bypass)
- Persistent configuration across reboots (`netfilter-persistent` + systemd)
- Full local network access from trusted VLANs
- Detailed EdgeRouter-4 firewall rules
- Tailscale as secure backup remote access

## Table of Contents

- [PIA VPN Installation](docs/PIA-Installation.md)
- [iptables Split Tunneling](docs/iptables-split-tunnel.md)
- [Systemd Services](docs/Systemd-Services.md)
- [EdgeRouter-4 Firewall Rules](docs/ER4-Firewall-Rules.md)
- [VLAN Overview](docs/VLAN-Overview.md)
- [Troubleshooting](docs/Troubleshooting.md)

## Quick Start

1. Follow [PIA Installation](docs/PIA-Installation.md)
2. Set up [iptables bypass](docs/iptables-split-tunnel.md)
3. Configure [Systemd Services](docs/Systemd-Services.md)
4. Add firewall rules on ER-4

---

**Repository Purpose**: Fully documented, repeatable home lab setup for future reinstalls or upgrades.

**Last Updated**: May 2026