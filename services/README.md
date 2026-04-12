# Services

- Draft version - structure in place, content being refined.

Each service is documented with its role, trust assumptions and the problems it is designed to solve.

These services are intentionally separated to enforce clear roles, reduce complexity and improve observability and control.

## Core Services

1. [Tailscale](tailscale.md)  
   Secure remote access and private control plane, avoiding direct exposure to the internet.

2. [AdGuard Home](adguardhome.md)  
   Centralised DNS filtering, visibility and control over client resolutiion.

3. [Mullvad](mullvad.md)  
   Enforced outbound routing, providing privacy and controlled egress.

4. [Uptime Kuma](uptime-kuma.md)  
   Internal and external service monitoring with reachability validation.

5. [ntfy](ntfy.md)  
   Alert delivery system for out-of-band notifications.
