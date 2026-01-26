# Services

This section documents the core services in my homelab, listed in deployment
and dependency order. Each page explains **why** the service exists, **how**
it is deployed, and **what problem it solves**.

## Service Order

1. [Proxmox](proxmox.md)  
   Host.

2. [Tailscale](tailscale.md)  
   Secure remote access and control plane.

3. [AdGuard Home](adguardhome.md)  
   DNS filtering and visibility.

4. [Mullvad](mullvad.md)  
   Outbound traffic privacy and egress control.

5. [Uptime Kuma](uptime-kuma.md)  
   Service and reachability monitoring.

6. [ntfy](ntfy.md)  
   Alert delivery and notification fan-out.
