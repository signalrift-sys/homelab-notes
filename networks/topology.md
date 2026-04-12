# Network Topology

## Diagram

![Topology](./network_topology.png)

## Overview
This homelab is designed to enforce controlled outbound traffic, centralised DNS filtering and ensure privacy through VPN routing, while maintaining secure remote access and external monitoring visibility.

## Primary Traffic Flows
- LAN -> Adguard -> Mullvad -> Internet
- Remote access -> Tailscale -> Proxmox -> internal services

## Access Model
Remote access is handled via Tailscale, providing secure entry into the Proxmox host without exposing services publicly.

## Monitoring
External monitoring is handled via a VPS running Uptime Kuma and ntfy, ensuring alerting remains functional even if the homelab is offline.

## Failure Considerations
- Loss of Mullvad: outbound traffic fails or leaks depending on the firewall state.
- Loss of Adguard: DNS resolution fails for LAN clients.
- Loss of Tailscale: remote access is unavailable, but internal services remain unaffected.
- Homelab offline: detected via VPS monitoring and alerted through ntfy.
