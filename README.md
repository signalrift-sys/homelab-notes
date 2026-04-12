# Security-Focused Homelab Architecture

Security-focused homelab architecture designed to enforce controlled outbound traffic, centralised DNS filtering and resilient monitoring.

Built as a practical system to explore real-world networking, privacy and failure handling. 

## What This Demonstrates
- Network segmentation and controlled traffic routing.
- VPN-enforced outbound connectivity.
- Centralised DNS filtering and visibility.
- Secure remote access via Tailscale with minimal exposure.
- External monitoring and alerting with failover capability.
- Consideration of failure scenarios and system resilience.

No real IPs, domains or sensitive configs are included. All examples are redacted and conceptual.

## Design Principles
- Privacy-first by default.
- Minimal exposed surface.
- Observable failure over silent failure (all failures are detectable and alertable).
- Resilience through external monitoring and fallback paths.
- Simplicity over unnecessary complexity.

## System Summary
- The homelab is built around an isolated network (10.10.10.0/24), with all outbound traffic routed through a dedicated Mullvad VPN gateway VM.
- DNS is centralised via Adguard, providing visibility and filtering.
- Remote access is handled via Tailscale, avoiding direct exposure to the internet and overcoming limitations of consumer-grade routers.
- Monitoring is split between internal and external systems to remove simgle points of failure, with alerting via Uptime Kuma and ntfy.
- No client has direct internet access; all traffic is controlled, observable and routed through defimed paths.

## Design Evolution
- Initial monitoring was internal only, which created blindspots during outages.
- This led to the addition of a VPS-based monitoring and alerting system to provide external visibility.

## Next Steps/Planned Improvements
- Implement DNS fallback via VPS-based Adguard.
- Expand monitoring coverage (VPN health, routing integrity).
- Continue refining whitelist and outbound restrictions.

## Planned Structure
- `network/` – topology, subnets, traffic flow
- `security/` – whitelist model, monitoring, backups
- `services/` – Mullvad VM, AdGuard, Tailscale, ntfy, Uptime Kuma



