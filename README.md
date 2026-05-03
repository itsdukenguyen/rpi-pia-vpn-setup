# Vaultwarden on TrueNAS Scale - Home Lab Setup

![Vaultwarden](https://img.shields.io/badge/Vaultwarden-000000?style=for-the-badge&logo=bitwarden&logoColor=white)
![TrueNAS Scale](https://img.shields.io/badge/TrueNAS-Scale-00A3E0?style=for-the-badge&logo=truenas)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

Complete guide for installing, configuring, and maintaining **Vaultwarden** (Bitwarden-compatible password manager) on my **TrueNAS Scale** server.

**Last Updated:** April 30, 2026

## Quick Links

- **[Setup Checklist](SETUP-CHECKLIST.md)**
- **[EdgeRouter-4 Firewall Rules](edge-router-firewall-rules.md)**
- **[VLAN Overview](docs/vlan-overview.md)**
- **[Backup Script](scripts/vaultwarden_backup.sh)**

## Screenshots

<div align="center">
  <img src="screenshots/01-vaultwarden-storage-config.png" width="600" alt="Storage Configuration">
  <img src="screenshots/03-nginx-proxy-host-01.png" width="600" alt="Nginx Proxy Host">
  <img src="screenshots/04-vaultwarden-admin-ui-03.png" width="600" alt="SMTP Settings">
</div>

## Overview

- **Server**: TrueNAS Scale @ `192.168.10.101`
- **Public URL**: [https://vaultwarden-nguyen.duckdns.org](https://vaultwarden-nguyen.duckdns.org)
- **Backup**: Daily encrypted GPG backups with 30-day retention
- **Access**: Nginx Proxy Manager + Let's Encrypt

## Repository Structure

- `docs/` — Network & VLAN documentation
- `scripts/` — Automation scripts
- `screenshots/` — Visual setup references
- `SETUP-CHECKLIST.md` — Step-by-step installation guide
- `edge-router-firewall-rules.md` — All ER-4 firewall rules