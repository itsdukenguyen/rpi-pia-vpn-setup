# Vaultwarden on TrueNAS Scale - Home Lab Setup

![Vaultwarden](https://img.shields.io/badge/Vaultwarden-000000?style=for-the-badge&logo=bitwarden&logoColor=white)
![TrueNAS Scale](https://img.shields.io/badge/TrueNAS-Scale-00A3E0?style=for-the-badge&logo=truenas)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

Complete guide for installing, configuring, and maintaining **Vaultwarden** (Bitwarden-compatible password manager) on my **TrueNAS Scale** server as part of my home lab.

**Last Updated:** April 30, 2026

## Screenshots

<div align="center">
  <img src="screenshots/01-vaultwarden-storage-config.png" width="600" alt="Storage Configuration">
  <img src="screenshots/03-nginx-proxy-host-01.png" width="600" alt="Nginx Proxy Host">
  <img src="screenshots/04-vaultwarden-admin-ui-03.png" width="600" alt="SMTP Settings">
</div>

## Quick Links

- [Setup Checklist](SETUP-CHECKLIST.md)
- [EdgeRouter-4 Firewall Rules](edge-router-firewall-rules.md)
- [Backup Script](scripts/vaultwarden_backup.sh)
- [VLAN Overview](docs/vlan-overview.md)

## Overview

- **Server**: TrueNAS Scale @ `192.168.10.101`
- **Public URL**: [https://vaultwarden-nguyen.duckdns.org](https://vaultwarden-nguyen.duckdns.org)
- **Backup**: Daily encrypted GPG backups (30-day retention)

---

**Save and close Notepad.**

---

### 2. Create Remaining Files

#### a. Move backup script to `scripts/`

```powershell
Move-Item backup-script/vaultwarden_backup.sh scripts/vaultwarden_backup.sh -Force
Remove-Item backup-script -Recurse -Force