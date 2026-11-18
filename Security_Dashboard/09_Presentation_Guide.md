# 09 — 10–15 Minute Presentation Guide

## Suggested 9-slide outline
1. **Title and research question** (0:45)
2. **Existing hardened server** — what was already completed, verified details (1:30)
3. **The problem** — security data spread across commands/logs (1:00)
4. **New project goals and seven dashboard features** (1:00)
5. **Architecture and privacy model** — non-root, read-only, tunnel (1:30)
6. **Implementation approach** — collector/API/UI, manual AI-guided coding (1:30)
7. **Live/private demo or screenshots** — health, SSH/Fail2ban, firewall/ports, Docker, events, Lynis (3:00)
8. **Validation table and troubleshooting** — 2–3 actual checked metrics (1:30)
9. **Findings, limitations, and future work** (1:00)

## Prior hardening slide — show clearly
- Root SSH login disabled (**explicitly stated**; verify on current host before claiming current state).
- Previously discussed SSH keys, UFW, Fail2ban and past Lynis audit; only show controls with verified configuration/evidence.
- Label historical hardening **before the project**, and the dashboard **built during the project**.

## Demo script
1. Open dashboard through private SSH tunnel.
2. Show last refresh and source/error status.
3. Show 2–3 key cards, then Docker and a bounded timeline if done.
4. Compare one card with redacted terminal command output.
5. Point out the Lynis audit **date** and what that score does not prove.
6. Explain one design limitation or issue encountered.

## Questions to prepare for
- What stops an outsider from opening the dashboard?
- Why is it read-only?
- How are metrics gathered without dangerous permissions?
- What is the difference between failed login attempts and attacks?
- What parts did you write yourself vs use AI assistance for?
- Why isn't Lynis a real-time security score?
- What would you improve with two more weeks?

## Pre-demo checklist
- [ ] Redact IPs/usernames/secrets in screenshots.
- [ ] Rehearse and time to 10–15 minutes.
- [ ] Have screenshots as fallback for failed network connection.
- [ ] Avoid live system changes for the sake of demonstrating a ban.
