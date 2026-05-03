# Raspberry Pi 4 - PIA VPN with Persistent SSH & VNC Access

**Project Goal**: Run Private Internet Access (PIA) VPN on `rpi-torrent` (`192.168.10.115`) while maintaining **local SSH (22)** and **VNC (5900)** access from Management and Clients VLANs — even after reboots.

---

## Features

- iptables policy routing to bypass VPN for SSH/VNC
- Persistent across reboots (`netfilter-persistent` + systemd)
- Full local network access from VLAN1 & VLAN30
- Detailed EdgeRouter-4 firewall configuration
- Tailscale as backup remote access

## Table of Contents

- [PIA VPN Installation](docs/PIA-Installation.md)
- [iptables Split Tunneling](docs/iptables-split-tunnel.md)
- [Systemd Services](docs/Systemd-Services.md)
- [EdgeRouter-4 Firewall Rules](docs/ER4-Firewall-Rules.md)
- [Troubleshooting](docs/Troubleshooting.md)

## Quick Start

1. Install PIA client → [Installation](docs/PIA-Installation.md)
2. Configure iptables bypass → [Split Tunneling](docs/iptables-split-tunnel.md)
3. Set up systemd services
4. Add ER-4 firewall rules

---

**Repository Purpose**: Fully documented, repeatable home lab setup for future reinstalls.

**Last Updated**: May 2026