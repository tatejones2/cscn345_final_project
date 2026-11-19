# 12 — AI Coding Agent Handoff (ALTERNATIVE ONLY)

This is a self-contained specification for **Claude Code or Codex** if you later choose an AI-assisted full implementation rather than manually authoring modules.

## Copy/paste instructions

> Implement an original **Linux-focused Python terminal security monitoring program** called **Security_Dashboard** for a CSCN 345 programming assignment. The primary interface must run in the Ubuntu/Linux terminal using **Rich**; do **not** make a web dashboard the main product. The user's submission requires a **5–7-page APA paper and source code in an appendix**, plus a 10–15-minute presentation. Deadline: **November 24, 2026**.
>
> The target is an **existing hardened DigitalOcean Ubuntu server** that runs real Docker-hosted apps. The user has previously disabled root SSH login; all other current security configuration details must be verified before claims. **Never alter firewall, SSH, Fail2ban, Caddy, PostgreSQL, Docker containers, websites or public exposure** without the user's separate explicit approval. No exploit/brute-force tests against the live host.
>
> Deliver a Python 3 project with a `security_monitor.py` CLI entry point, `requirements.txt`, README, separate collector modules, a uniform result data model, tests and fixtures. Required monitoring categories: (1) SSH accepted/failed logins in explicitly defined time windows, (2) Fail2ban jail state, current bans and cumulative bans, (3) UFW status and locally listening ports, (4) uptime/load/CPU if properly sampled, memory and disk, (5) sanitized recent security event timeline, (6) dated existing Lynis result, (7) Docker container status from a safe minimal snapshot or unavailable state. Priority: health, SSH, Fail2ban, UFW/ports first; then timeline, Docker, Lynis.
>
> Make it **read-only** and run by default as a non-root user. Use allowlisted fixed command argument arrays, `shell=False`, timeouts, bounded output and careful parsing. Do not grant broad sudo, add the monitor to docker group, mount `/var/run/docker.sock`, collect complete private logs, or expose new network services. If protected data is inaccessible, display `unavailable` and explain why; do not fabricate zeros. Synthetic fixtures must be clearly labeled `DEMO`.
>
> Every collector result must provide `collected_at` in timezone-aware ISO-8601, `source`, `status=ok|unavailable|error|stale`, `data`, `error`, and `mode=live|demo`. Include measurement windows for auth counts, timestamps for imported Lynis report and health status when known. Parse file/command output defensively. Unit-test normal, malformed, missing, permission-denied and stale scenarios. Display timestamps/errors in the Rich terminal view.
>
> CLI behavior: `python3 security_monitor.py` shows a one-shot terminal dashboard; optional `--demo` uses fixtures and is prominently labeled; optional `--refresh 30` runs a safe periodic refresh if implemented. Add `--help`. Do not require a browser, public port, database, React, FastAPI or backend service. Optional GUI must be separate and cannot block the main implementation.
>
> Produce clean, understandable code, documented setup on Ubuntu, a small tests suite, architecture explanation, sample sanitized output, and a test matrix. Also create **paper notes/outlines**, but do not invent results, screenshots, current scores or citations. Preserve user's opportunity to inspect and approve modifications; show diffs and commands before applying them when working against the existing server.

## Acceptance criteria
- [ ] CLI works on Ubuntu, non-root; stable display when sources missing.
- [ ] At least P0 monitored live or accurately marked as unavailable; remaining modules have documented status.
- [ ] Source comparison/test evidence documented; fixtures visibly not live.
- [ ] Tests run and README explains setup and demonstration.
- [ ] No changes to production infrastructure or public ports.
- [ ] No lengthy web UI built instead of the Linux terminal program.

## Human review before using result
Review every file, read the CLI setup instructions, run tests in a safe environment, and confirm no new service, cron job, sudoers rule or privileged account was added. Use the actual work/results for the paper.
