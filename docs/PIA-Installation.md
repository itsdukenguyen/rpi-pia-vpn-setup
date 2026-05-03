# PIA VPN Installation on Raspberry Pi 4 (rpi-torrent)

**Device**: `192.168.10.115` (VLAN10 - Servers)  
**Client Version**: `pia-linux-arm64-3.6.1-08339`

## Prerequisites
- Raspberry Pi OS (Bookworm or later)
- Internet connectivity on the Pi
- PIA account credentials

---

## 1. Install PIA Client

```bash
# Run as the 'pi' user
wget https://www.privateinternetaccess.com/installer/pia-linux-arm64-3.6.1-08339.tar.gz
tar xzf pia-linux-arm64-3.6.1-08339.tar.gz
cd pia-linux-arm64-3.6.1-08339
sudo ./install.sh

piactl --version

# Create secure login file
echo -e "p1684898\naG6iNa33NA" | sudo tee /home/pi/pia_login.txt
sudo chmod 600 /home/pi/pia_login.txt

# Login
piactl login /home/pi/pia_login.txt

# Critical: Allow local network traffic (SSH/VNC)
piactl set allowlan true

# Enable background mode so piactl works without GUI
piactl background enable

piactl get allowlan

# Connect to VPN
piactl connect

# Check status
piactl get connectionstate     # Should return "Connected"
piactl get pubip               # Should show PIA server IP (not your home IP)

