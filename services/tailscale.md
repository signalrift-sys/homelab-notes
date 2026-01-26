# Tailscale

## Role in Architecture
Primary authenticated access layer into the homelab. All administrative access assumes Tailscale is functioning.

## Trust Model
Tailscale is trusted for device identity and encrypted transport. It is not trusted for authorisation decisions beyond network reachability.

## Threats Addressed
- Remote access exposure
- Port forwarding risk
- Credential sprawl

## Design Decisions
Why Tailscale was chosen over alternatives.

## Failure Modes
What happens if Tailscale is unavailable.

## Trade-offs
Centralisation vs convenience.
