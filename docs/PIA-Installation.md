# PIA VPN Installation on Raspberry Pi 4 (rpi-torrent)

**Device**: `192.168.10.115` (VLAN10 - Servers)

## Prerequisites
- Raspberry Pi OS (Bookworm or later)
- Internet access on the Pi
- PIA account credentials

## 1. Install PIA Client

```bash
# Download and install (run as pi user)
wget https://www.privateinternetaccess.com/installer/pia-linux-arm64-3.6.1-08339.tar.gz
tar xzf pia-linux-arm64-3.6.1-08339.tar.gz
cd pia-linux-arm64-3.6.1-08339
sudo ./install.sh

# Create login file (secure permissions)
echo -e "p1684898\naG6iNa33NA" | sudo tee /home/pi/pia_login.txt
sudo chmod 600 /home/pi/pia_login.txt

# Login
piactl login /home/pi/pia_login.txt

# Allow LAN traffic (critical for local SSH/VNC)
piactl set allowlan true

# Enable background mode (so piactl works without GUI)
piactl background enable

piactl connect
piactl get connectionstate     # Should show "Connected"
piactl get pubip               # Should show PIA exit IP