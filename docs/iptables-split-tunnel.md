# iptables Split Tunneling for SSH & VNC (Persistent)

**Purpose**: Bypass PIA VPN tunnel for ports 22 (SSH) and 5900 (VNC) so local devices on Management and Clients VLANs can still connect.

## 1. Mark SSH and VNC Traffic

```bash
sudo iptables -A OUTPUT -p tcp --dport 22   -j MARK --set-mark 1
sudo iptables -A OUTPUT -p tcp --sport 22   -j MARK --set-mark 1
sudo iptables -A OUTPUT -p tcp --dport 5900 -j MARK --set-mark 1
sudo iptables -A OUTPUT -p tcp --sport 5900 -j MARK --set-mark 1

sudo iptables -A INPUT  -p tcp --dport 22   -j MARK --set-mark 1
sudo iptables -A INPUT  -p tcp --sport 22   -j MARK --set-mark 1
sudo iptables -A INPUT  -p tcp --dport 5900 -j MARK --set-mark 1
sudo iptables -A INPUT  -p tcp --sport 5900 -j MARK --set-mark 1

# Add custom routing table
echo "200 bypass" | sudo tee -a /etc/iproute2/rt_tables

# Add policy rule and default route via ER-4
sudo ip rule add fwmark 1 table bypass
sudo ip route add default via 192.168.10.1 dev eth0 table bypass
sudo ip route flush cache

# Save iptables rules
sudo iptables-save | sudo tee /etc/iptables/rules.v4

# Enable persistence service
sudo systemctl enable netfilter-persistent

# Make routing rules run on network up
sudo nano /etc/network/if-up.d/restore-routing

#!/bin/sh
ip rule add fwmark 1 table bypass
ip route add default via 192.168.10.1 dev eth0 table bypass
ip route add 192.168.1.0/24 via 192.168.10.1 dev eth0
ip route add 192.168.30.0/24 via 192.168.10.1 dev eth0
ip route flush cache

sudo chmod +x /etc/network/if-up.d/restore-routing


---

### 2. `docs/iptables-split-tunnel.md` (Full Updated Content)

Copy and paste the entire content below into Notepad:

```markdown
# iptables Split Tunneling for SSH & VNC (Persistent)

**Purpose**: Bypass the PIA VPN tunnel for ports **22 (SSH)** and **5900 (VNC)** so devices on the Management VLAN (`192.168.1.0/24`) and Clients VLAN (`192.168.30.0/24`) can still connect locally, even while the VPN is active.

---

## 1. Mark SSH and VNC Traffic

```bash
sudo iptables -A OUTPUT -p tcp --dport 22   -j MARK --set-mark 1
sudo iptables -A OUTPUT -p tcp --sport 22   -j MARK --set-mark 1
sudo iptables -A OUTPUT -p tcp --dport 5900 -j MARK --set-mark 1
sudo iptables -A OUTPUT -p tcp --sport 5900 -j MARK --set-mark 1

sudo iptables -A INPUT  -p tcp --dport 22   -j MARK --set-mark 1
sudo iptables -A INPUT  -p tcp --sport 22   -j MARK --set-mark 1
sudo iptables -A INPUT  -p tcp --dport 5900 -j MARK --set-mark 1
sudo iptables -A INPUT  -p tcp --sport 5900 -j MARK --set-mark 1

# Add custom routing table
echo "200 bypass" | sudo tee -a /etc/iproute2/rt_tables

# Add policy rule + default route via ER-4 (VLAN10 gateway)
sudo ip rule add fwmark 1 table bypass
sudo ip route add default via 192.168.10.1 dev eth0 table bypass
sudo ip route flush cache

# Save iptables rules
sudo iptables-save | sudo tee /etc/iptables/rules.v4

# Enable persistence service
sudo systemctl enable netfilter-persistent
sudo systemctl status netfilter-persistent

sudo nano /etc/network/if-up.d/restore-routing

#!/bin/sh
# Restore iptables bypass routing on network interface up
ip rule add fwmark 1 table bypass
ip route add default via 192.168.10.1 dev eth0 table bypass
ip route add 192.168.1.0/24 via 192.168.10.1 dev eth0
ip route add 192.168.30.0/24 via 192.168.10.1 dev eth0
ip route flush cache

sudo chmod +x /etc/network/if-up.d/restore-routing

# Check rules
sudo iptables -L -v -n --line-numbers
ip rule show
ip route show table bypass

# Test local access (with PIA connected)
ping 192.168.10.115
ssh pi@192.168.10.115