# iptables Split Tunneling for SSH & VNC (Persistent)

**Purpose**: Bypass the PIA VPN tunnel for ports **22 (SSH)** and **5900 (VNC)** so local devices can still connect.

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
```

## 2. Create Bypass Routing Table
```bash
echo "200 bypass" | sudo tee -a /etc/iproute2/rt_tables

sudo ip rule add fwmark 1 table bypass
sudo ip route add default via 192.168.10.1 dev eth0 table bypass
sudo ip route flush cache
```

## 3. Make Persistent
```bash
# Save iptables rules
sudo iptables-save | sudo tee /etc/iptables/rules.v4

# Enable persistence
sudo systemctl enable netfilter-persistent
```

## Create network hook:
```bash
sudo nano /etc/network/if-up.d/restore-routing
```

## Paste:
```bash
#!/bin/sh
ip rule add fwmark 1 table bypass
ip route add default via 192.168.10.1 dev eth0 table bypass
ip route add 192.168.1.0/24 via 192.168.10.1 dev eth0
ip route add 192.168.30.0/24 via 192.168.10.1 dev eth0
ip route flush cache
```

```bash
sudo chmod +x /etc/network/if-up.d/restore-routing
```

## Verification:
```bash
sudo iptables -L -v -n --line-numbers
ip rule show
ip route show table bypass
```