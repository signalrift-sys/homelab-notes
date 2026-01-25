# Homelab Notes (Security Focused)

High level documentation for a privacy-focused, security-first homelab.

This repo contains:
- Sanitised network topology notes
- Service architecture descriptions
- Security controls and monitoring plans
- Backup and disaster recovery strategy

No real IPs, domains or sensitive configs are included. All examples are redacted and conceptual.

## Design Principles

- Privacy-first by default
- Minimal exposed surface
- Observable failure over silent failure
- Portatbility

## Structure
- `network/` – topology, subnets, flow diagrams
- `security/` – whitelist model, backups, monitoring
- `services/` – Mullvad VM, AdGuard DNS, Tailscale, ntfy, Uptime Kuma


