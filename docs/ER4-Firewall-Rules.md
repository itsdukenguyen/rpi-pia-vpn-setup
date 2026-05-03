# EdgeRouter-4 Firewall Rules (LAN_IN)

**All rules are under `firewall name LAN_IN`**

## Key Rules Summary

### Management VLAN (`192.168.1.0/24`)
- Rule 1 & 10: Allow Management to Any
- Rule 11: Cockpit (9090) on COCKPIT_SERVERS group
- **Rule 8 (Added)**: SSH (22) + VNC (5900) to `192.168.10.115`

### Tailscale (`100.64.0.0/10`)
- Rule 17: VNC (5900) to rpi-torrent
- Rule 18: SSH (22) to rpi-torrent
- Rule 19: VLAN10 Services

### Clients VLAN (`192.168.30.0/24`)
- **Rule 9 (Added)**: SSH (22) + VNC (5900) to `192.168.10.115`

---

## Commands to Add Rules (via PuTTY / SSH)

```bash
configure

# Management VLAN → rpi-torrent (SSH + VNC)
set firewall name LAN_IN rule 8 action accept
set firewall name LAN_IN rule 8 description "Allow Management to SSH/VNC on RPi"
set firewall name LAN_IN rule 8 destination address 192.168.10.115
set firewall name LAN_IN rule 8 destination port 22,5900
set firewall name LAN_IN rule 8 protocol tcp
set firewall name LAN_IN rule 8 source address 192.168.1.0/24
set firewall name LAN_IN rule 8 state new enable
set firewall name LAN_IN rule 8 state established enable
set firewall name LAN_IN rule 8 state related enable

# Clients VLAN → rpi-torrent (SSH + VNC)
set firewall name LAN_IN rule 9 action accept
set firewall name LAN_IN rule 9 description "Allow Clients to SSH/VNC on RPi"
set firewall name LAN_IN rule 9 destination address 192.168.10.115
set firewall name LAN_IN rule 9 destination port 22,5900
set firewall name LAN_IN rule 9 protocol tcp
set firewall name LAN_IN rule 9 source address 192.168.30.0/24
set firewall name LAN_IN rule 9 state new enable
set firewall name LAN_IN rule 9 state established enable
set firewall name LAN_IN rule 9 state related enable

commit
save
exit


show firewall name LAN_IN