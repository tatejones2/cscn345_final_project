# 13 — Metric Definitions and Verification

These definitions apply to both the Python collectors and the paper.

| Label | Definition | Suggested Linux source | Caveat |
|---|---|---|---|
| SSH failed logins (last 24h) | Count of matching failed authentication records in explicit window | `journalctl` or auth.log | One attempt can generate multiple records; failures ≠ attacks |
| SSH accepted logins (last 24h) | Count of accepted-auth records in explicit window | journal or auth.log | Accepted auth not necessarily interactive shell session |
| Fail2ban currently banned | Current banned IP count for named jail | `fail2ban-client status <jail>` | Per jail; not unique attackers |
| Fail2ban total banned | Cumulative bans in jail's reported scope | same | May reset based on lifecycle |
| UFW | Enabled/disabled plus selected rules | `ufw status` | Cloud Firewall is separate |
| Listening ports | Locally bound TCP/UDP sockets | `ss -tuln` | Does not prove internet reachability |
| CPU percentage | CPU time sampled over an interval | psutil or /proc | Do not label load average as CPU percent |
| Memory/disk | Used and available bytes, utilization | psutil, `free`, `df` | Check units and filesystem |
| Recent security events | Small selected log timeline | journal / Fail2ban logs | Event ≠ confirmed compromise |
| Lynis index | Hardening index from **specific dated audit** | existing saved report | Not live and not a security guarantee |
| Docker status | Running state/health at collection | minimal authorized snapshot | `docker` permission may be root-equivalent |

## Validation process
1. Record clock/time zone and measurement window.
2. Run authorized source command, redact output.
3. Run Python collector and note timestamp/source.
4. Compare same window and same units, investigate discrepancies.
5. Record `match`, `known difference`, `unavailable` or `error` in `06_Evidence_and_Test_Log.md`.

## Required edge cases
- No journal permission: `unavailable`, **not** 0.
- No events in an accessible interval: measured 0 is valid.
- Fail2ban missing or jail stopped: `unavailable` or clear stopped status.
- Lynis report missing: not available; never show old score as live.
- Docker not accessible: unavailable; no privilege escalation.
- Partial command output: parser error but remaining dashboard loads.
- Demo fixture used: **DEMO** flag in every relevant view.
