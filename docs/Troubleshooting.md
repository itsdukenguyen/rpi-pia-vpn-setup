# Troubleshooting Guide

## 1. No SSH/VNC Access After Reboot

```bash
# Check iptables
sudo iptables -L -v -n --line-numbers | grep -E '22|5900'

# Check routing
ip rule show
ip route show table bypass

# Re-apply routing
sudo /etc/network/if-up.d/restore-routing
```


## 2. PIA VPN Not Starting
```bash
sudo systemctl status pia-vpn
sudo journalctl -u pia-vpn -e
piactl get connectionstate
```

## 3. Local Access Still Blocked
- Check ER-4 logs: show log | grep 192.168.10.115
- Verify firewall rules: show firewall name LAN_IN
- Test with PIA disconnected: piactl disconnect

## 4. General Commands
```bash
piactl --help
piactl get allowlan
sudo netstat -tulnp | grep -E ':22|:5900'
```