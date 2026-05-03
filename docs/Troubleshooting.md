# Troubleshooting Guide

## 1. No SSH/VNC Access After Reboot

```bash
# Check iptables rules
sudo iptables -L -v -n --line-numbers | grep -E '22|5900'

# Check routing
ip rule show
ip route show table bypass

# Re-apply routing rules
sudo /etc/network/if-up.d/restore-routing


sudo systemctl status pia-vpn
sudo journalctl -u pia-vpn -e
piactl get connectionstate


piactl --help
piactl get allowlan
sudo netstat -tulnp | grep -E ':22|:5900'