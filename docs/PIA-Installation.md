# PIA VPN Installation on Raspberry Pi 4 (rpi-torrent)

**Device**: `192.168.10.115` (VLAN10 - Servers)  
**Client Version**: `pia-linux-arm64-3.6.1-08339`

## Prerequisites
- Raspberry Pi OS (Bookworm or later)
- Internet connectivity
- PIA account

---

## 1. Install PIA Client

```bash
wget https://www.privateinternetaccess.com/installer/pia-linux-arm64-3.6.1-08339.tar.gz
tar xzf pia-linux-arm64-3.6.1-08339.tar.gz
cd pia-linux-arm64-3.6.1-08339
sudo ./install.sh
```

## Verify:
```bash
piactl --version
```

## 2. Login
```bash
echo -e "p1684898\naG6iNa33NA" | sudo tee /home/pi/pia_login.txt
sudo chmod 600 /home/pi/pia_login.txt

piactl login /home/pi/pia_login.txt
```

## 3. Basic Settings
```bash
piactl set allowlan true
piactl background enable
```

## Verify:
```bash
piactl get allowlan
```

## 4. Connect & Test
```bash
piactl connect
piactl get connectionstate     # Should return "Connected"
piactl get pubip               # Should show PIA server IP
```
