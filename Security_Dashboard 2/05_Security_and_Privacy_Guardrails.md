# 05 — Production Server Safety Rules

You are collecting from a live DigitalOcean host that also runs real services. **Do not disrupt those services for a class project.**

## Non-negotiable constraints
- The monitor is **read-only**: no changing SSH/UFW/Fail2ban, no container restarts, no ban/unban, no arbitrary command console.
- Keep existing SSH configuration, Caddy, Docker containers, database and websites unchanged without explicit, separate approval.
- No public endpoint is necessary: the terminal program runs over your existing SSH session.
- Run as a non-root user; **do not** use `sudo python3 security_monitor.py` as the solution to every permission problem.
- `docker` group / Docker daemon socket may confer root-equivalent control; do not grant this to the app merely to display a container count.
- Avoid broad passwordless sudo or weakening authentication to enable easier testing.
- Read logs sparingly, bound the last N lines / time window, redact addresses/usernames in evidence.
- Never commit secrets, keys, tokens, `.env`, journal dumps, complete ban lists or sensitive log exports.
- External test traffic or brute forcing should not be sent to the production Droplet; use synthetic fixtures or an isolated local VM.

## Practical privilege plan
Start with health + local listening sockets under ordinary permissions. For protected sources, prefer:
1. Read-only admin-run capture of **only required aggregated counts** saved to permissions-controlled JSON.
2. A documented `unavailable` state when permissions do not permit safe collection.
3. Narrowly scoped access after explicitly reviewing the security implications; never general sudo/Docker daemon privilege for app convenience.

## Failure behavior
- Command absent: say `unavailable`.
- Permission denied: say `unavailable`, with safe reason, no fabricated count.
- Timeout/parser error: say `error`, without crashing the rest of the dashboard.
- Stale imported report: show audit age and date.
- Synthetic sample: show **DEMO DATA**, never disguise it as production.

## Data sharing
Before putting server output in any AI chat or in slides, redact actual usernames, external IP addresses, private addresses, domain secrets, personally identifying log fields and exact service details not needed for the assignment.
