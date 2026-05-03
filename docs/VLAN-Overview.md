# VLAN Overview

| VLAN | Subnet             | Description     | Purpose                     |
|------|--------------------|-----------------|-----------------------------|
| 1    | 192.168.1.0/24     | Management      | Admin devices, ER-4, APs    |
| 10   | 192.168.10.0/24    | Servers         | TrueNAS, RPi services       |
| 20   | 192.168.20.0/24    | IoT             | Smart devices               |
| 30   | 192.168.30.0/24    | Clients         | Phones, PCs                 |
| 40   | 192.168.40.0/24    | Guests          | Isolated guest network      |

**rpi-torrent**: `192.168.10.115` (VLAN10)