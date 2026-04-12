# Incident Report — VPN Gateway Bypass

## Summary
Traffic from the private subnet (10.10.10.0/24) was not exiting via the Mullvad VPN gateway as designed. Systems appeared partially functional, but outbound traffic bypassed the VPN and exited via the LAN gateway.

## Impact
- Traffic exited via ISP (UK IP) instead of VPN
- Privacy objective failed (unencrypted ISP-visible traffic)
- Partial functionality masked the issue, delaying root cause identification

## Environment
- Proxmox host (192.168.0.100)
- Mullvad VM (10.10.10.2) acting as VPN gateway
- AdGuard LXC (10.10.10.10)
- Private subnet: 10.10.10.0/24
- LAN subnet: 192.168.0.0/24

## Initial Hypothesis
Investigation initially focused on:
- Mullvad VPN connectivity and tunnel state
- DNS resolution failures within AdGuard LXC
- NAT and forwarding rules on the Mullvad VM

This was based on the assumption that the VPN gateway or DNS layer had failed.

## Investigation Path
1. **DNS Failure Identified**
   - AdGuard LXC unable to resolve domains
   - Found `/etc/resolv.conf` pointing to Tailscale DNS (100.100.100.100)
   - Corrected to use local resolver (127.0.0.1)
   - DNS restored

2. **Routing Verification**
   - Direct IP connectivity confirmed (`curl http://1.1.1.1`)
   - traceroute showed traffic reaching Mullvad internal network (10.128.x.x)
   - Indicated Mullvad VM routing and NAT were functional

3. **External IP Validation**
   - External IP checks returned ISP (UK) address
   - Contradicted earlier findings
   - Confirmed traffic was not consistently exiting via VPN

4. **Host-Level Inspection**
   - Checked routing table on Proxmox host
   - Found default route:

     default via 192.168.0.1 dev vmbr0

   - Revealed that outbound traffic was bypassing the Mullvad VM entirely

## Root Cause
The Proxmox host default route was configured to use the LAN gateway (192.168.0.1) instead of the Mullvad VM (10.10.10.2).

As a result, forwarded traffic bypassed the VPN gateway and exited directly via the ISP.

## Resolution
- Updated Proxmox host default route:

  ip route replace default via 10.10.10.2 dev vmbr10

- Added NAT rule on Mullvad VM:

  nft add rule ip nat postrouting ip saddr 10.10.10.0/24 oifname "wg0-mullvad" masquerade

- Corrected DNS inside AdGuard LXC:

  echo "nameserver 127.0.0.1" > /etc/resolv.conf

## Validation
- curl ifconfig.me (AdGuard LXC) returned Mullvad IP
- traceroute confirmed traffic path via Mullvad network
- DNS resolution functioning through AdGuard
- End-to-end traffic confirmed via VPN

## Lessons Learned
- Default route on the host determines actual traffic path, not service state
- DNS success does not confirm correct traffic routing
- Partial system functionality can mask critical routing issues
- Always validate VPN setups using external IP checks
- Debugging should move from service-level assumptions to host-level verification

## Key Takeaway
Correct VPN operation depends on routing, not connection status.

If the host default route bypasses the VPN gateway, traffic will leak regardless of tunnel state.
