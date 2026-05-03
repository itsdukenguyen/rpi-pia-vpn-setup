<<<<<<< HEAD
# Raspberry Pi 4 - PIA VPN with Persistent SSH & VNC Access

**Goal**: Run Private Internet Access (PIA) VPN on `rpi-torrent` (192.168.10.115) while maintaining local SSH (port 22) and VNC (port 5900) access from Management VLAN (`192.168.1.0/24`) and Clients VLAN (`192.168.30.0/24`), even after reboots.

## Hardware & Software
- **Device**: Raspberry Pi 4B (rpi-torrent @ 192.168.10.115)
- **VPN Client**: PIA Linux ARM64 (`pia-linux-arm64-3.6.1-08339`)
- **Router**: Ubiquiti EdgeRouter 4 (ER-4 @ 192.168.1.1)
- **Access**: Tailscale (backup), SSH, VNC

## Table of Contents
- [Installation Steps](docs/PIA-Installation.md)
- [EdgeRouter-4 Firewall Rules](docs/ER4-Firewall-Rules.md)
- [iptables Split Tunneling](docs/iptables-split-tunnel.md)
- [Systemd Services](docs/Systemd-Services.md)
- [Troubleshooting](docs/Troubleshooting.md)

## Features
- SSH and VNC bypass PIA VPN tunnel using iptables + policy routing
- Persistent across reboots via `netfilter-persistent` and systemd
- Full local network access from Management and Clients VLANs
- Tailscale as backup remote access

## Prerequisites
- Raspberry Pi OS (Bookworm or later)
- PIA account (username: `p1684898`)
- ER-4 with VLAN10 (Servers) configured
=======
# rpi-pia-vpn-setup
PIA VPN + iptables split-tunneling setup on Raspberry Pi 4 for maintaining SSH/VNC access while torrenting
>>>>>>> 77e16f4adb63934230e02f5e6535ea40fb5613c0
