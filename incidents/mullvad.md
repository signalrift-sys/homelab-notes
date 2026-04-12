# Incident Report: Mullvad Routing Failure

## Summary
Loss of outbound connectivity due to Mullvad VM failure, resulting in DNS resolution issues and loss of internet access for LAN clients.

---

## Impact
- No internet access for LAN clients
- DNS failures observed via AdGuard alerts
- Remote access still available via Tailscale
- Monitoring alerts triggered, but root cause not immediately clear

---

## Timeline
- T0: DNS failure alerts observed in monitoring
- T+X min: Confirmed no outbound internet connectivity
- T+X min: Verified AdGuard reachable but unable to resolve external queries
- T+X min: Identified Mullvad VM not routing traffic correctly
- T+X min: Attempted service restart, resulting in further instability
- T+X min: Attempted VM rollback tp previous snapshot, unsuccessful
- T+X min: Manual intervention restored connectivity

---

## Root Cause
Mullvad VM lost routing capability, likely due to VPN daemon or network configuration failure. This prevented outbound traffic from leaving the private network.

---

## Contributing Factors
- Monitoring detected symptoms (DNS failure) but not root cause (VPN failure)
- Lack of direct alerting on Mullvad tunnel status
- Troubleshooting actions introduced additional instability

---

## Resolution
- Restarted Mullvad VM and associated services
- Restored routing via Mullvad tunnel
- Verified DNS resolution via AdGuard

---

## Lessons Learned
- DNS failure alerts are indirect indicators of upstream issues
- VPN tunnel health requires direct monitoring
- Changes during incident response should be controlled and minimal
- Further documentation required

---

## Improvements / Actions
- Add direct Mullvad tunnel monitoring
- Improve alert clarity (distinguish DNS vs routing failures)
- Consider fallback DNS or secondary routing path
- Document recovery steps for faster resolution

---
