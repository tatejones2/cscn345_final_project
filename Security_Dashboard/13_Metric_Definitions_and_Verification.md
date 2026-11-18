# 13 — Metric Definitions, Accuracy, and Verification

This is the reference for UI labels, report claims, and tests. Every number needs a source and measurement window.

| Dashboard label | Meaning | Likely source | Verification caveat |
|---|---|---|---|
| SSH failed logins (past 24 h) | Count of relevant failure records in bounded time period | journal or auth.log | Record formats vary; one attempt can produce multiple lines; don't call all failures attacks |
| SSH successful logins (past 24 h) | Count of matching accepted-auth records | journal/auth.log | SSH accepted auth may differ from shell sessions |
| Fail2ban currently banned | IPs currently banned by a named jail | `fail2ban-client status <jail>` | Per-jail; may not be unique across jails |
| Fail2ban total banned | Jail cumulative ban statistic | `fail2ban-client status <jail>` | Depends on process/jail lifecycle, not necessarily server lifetime |
| Firewall status | Whether UFW reports active | `ufw status` | Cloud Firewall may also apply; UFW active ≠ every path secure |
| Listening ports | Locally bound sockets at sample time | `ss -tuln` | Some on loopback or container interfaces; not proof of external reachability |
| CPU/load | Current or sampled CPU/load indicator | OS/proc/psutil | Load average is not CPU percentage; label appropriately |
| Memory/disk | Used/available bytes and percentages | `free`, `df`, proc/psutil | Containers may report host stats differently |
| Recent events | Selected, sanitized security-relevant log entries | journal/auth/f2b logs | Events are not necessarily verified incidents |
| Lynis hardening index | Number reported by a **specific dated** audit | saved Lynis report | Not a vulnerability count, not a real-time security score |
| Running Docker containers | Containers running at sample time | `docker ps` restricted snapshot | Health may be `none`, `starting`, `healthy`, `unhealthy`, or absent |

## Common UI mistakes to avoid
- Never report `0 SSH failures` when auth log permission is denied.
- Never use `Total banned` as a count of unique malicious humans.
- Never treat every port listed by `ss` as public-facing.
- Never claim a reverse proxy or Docker container is secured simply because it is `healthy`.
- Never show a past Lynis result without its audit timestamp.
- Never merge results from separate sample windows without explaining timestamps.

## Suggested mock-data scenarios to test without production attacks
1. Normal system with all sources present.
2. Fail2ban jail missing or stopped.
3. Auth log inaccessible.
4. Empty event timeline (valid observed zero events).
5. Lynis report missing (show not available).
6. Docker container unhealthy.
7. Snapshot too old (show stale).
8. Log text containing HTML/script-like content (render as literal text).

## Source-to-dashboard comparison method
1. Note wall-clock time and window (prefer UTC for logs).
2. Collect source value with narrowly scoped, authorized command.
3. Refresh dashboard, note `collected_at` and exact window.
4. Compare like-for-like units and definitions; record match/tolerance.
5. Attach redacted evidence and explain mismatches.

## Historical hardening: source hierarchy
**Highest confidence:** current effective config/status; **next:** original dated config/audit/report; **then:** past notes/recollection. Label all three appropriately. Explicitly verified user fact: root login was disabled, but current state still needs a configuration check.
