# 12 — AI Agent Implementation Handoff (ALTERNATIVE PATH)

**Purpose:** Give this complete document to Claude Code, Codex, or another coding agent if you later decide to delegate construction. Prefer accompanying it with `README.md`, `04_Dashboard_Technical_Plan.md`, `05_Security_and_Privacy_Guardrails.md`, and `13_Metric_Definitions_and_Verification.md`.

## START OF COPYABLE AGENT INSTRUCTIONS
You are implementing a term-project application named **Security_Dashboard**. Build a **read-only, private Linux server security dashboard** for an **existing hardened DigitalOcean Ubuntu server**. **Do not alter the security configuration of the live host** and **do not connect to or deploy to production without explicit user approval**. Default to fixture data and local development.

### Non-negotiable operating rules
- **No autonomous access to remote servers** until the user explicitly approves the exact actions and access method.
- Never ask for or print SSH private keys, API tokens, passwords, database connection strings or secrets.
- Do not run intrusion attempts, brute-force tests or disruptive scans on the public server.
- No mutations to SSH, UFW, Fail2ban, Docker configuration, Caddy, PostgreSQL, websites or system packages without separate explicit approval.
- App and API are **read-only**; no endpoints for execution, restart, firewall modification, ban/unban or arbitrary filesystem browsing.
- The API runs as a non-root user and binds to `127.0.0.1`. Avoid public reverse proxy exposure.
- Do not put the Docker socket in the web app; do not grant the web app account docker group membership or passwordless arbitrary sudo.
- Use a least-privilege snapshot collection mechanism if privileged metrics are needed. If unavailable, return explicit `unavailable` states.
- All dynamic log strings must be sanitized, length-bounded, redacted and rendered as plain text.
- Never fake production metrics. Fixture data must visibly say `demo`.
- Maintain unit tests, safe defaults and reproducible setup docs.

### Product requirements
Seven feature areas: (1) SSH login attempts by clearly labeled time window; (2) Fail2ban jail status, current bans and cumulative bans; (3) UFW status/rule summary and listening ports; (4) server uptime/load/CPU/RAM/disk; (5) bounded recent security event timeline; (6) **dated** Lynis audit summary, not a live score; (7) Docker container state/health from a restricted snapshot, not the daemon socket.

Priority 0: server health, SSH, Fail2ban, UFW/ports. Priority 1: timeline, Docker, Lynis. Keep P0 fully functional and testable before P1 UI polish.

### Recommended stack
Backend: Python 3.11+, FastAPI, Uvicorn, pytest. Frontend: HTML/CSS/vanilla JS (React/Vite acceptable only if user approves). Snapshot files: JSON with `collected_at`, `source`, `status`, `data`, and safe error metadata. Keep fixtures/production adapters distinct. No heavy database required; do not access the app's existing PostgreSQL.

### Endpoints
`GET /api/health`, `/api/system`, `/api/ssh`, `/api/fail2ban`, `/api/firewall`, `/api/ports`, `/api/events`, `/api/lynis`, `/api/docker`. Include explicit schemas and bounded response sizes, `status: ok|unavailable|error|stale`, time windows, collected timestamps and source names. `null` is unavailable, `0` is measured zero. Prefer snapshots over privileged subprocesses.

### Required UI
Responsive dashboard with: title, last-updated indicator, data source/age and errors; metric cards for system and SSH/Fail2ban; firewall and ports details; event timeline; Docker status table; Lynis report with historical scan date. Display clearly when data is demo or stale; avoid claims that individual failed attempts are confirmed attacks.

### Source trust boundaries
- No user-controlled command execution, `shell=True`, arbitrary paths, SSRF, privilege escalation, or direct browser access to filesystem/logs.
- Docker metric collection may be performed by a trusted local administrative script that writes a minimal sanitized JSON snapshot to a protected file; it must not be callable from HTTP.
- Sensitive metrics may require manual imports or unavailable statuses. Do not automatically widen permissions.

### Expected repo layout
```text
security-dashboard/
  README.md
  .gitignore
  requirements.txt
  backend/   # app, schemas, snapshot readers, collectors
  frontend/  # UI assets
  fixtures/  # synthetic demo data only
  tests/     # parser, API, unavailable/stale, safety tests
  docs/      # architecture, deployment, verification, limitations
```

### Acceptance tests
1. Start server with `127.0.0.1` bind; no unauthenticated public service.
2. API routes return valid schema with source + UTC collection time and data status.
3. UI displays all seven categories or explicit unavailable; no invented zeros.
4. P0 metrics verified against fixture expected values and documented live source comparison procedure.
5. Missing/invalid/stale snapshot yields safe empty/error state, not success.
6. Event timeline enforces bounds and output escapes log payloads.
7. Docker socket is not exposed; application cannot mutate any host control.
8. Tests can run offline with fixtures.
9. Repo includes setup, test, private access, data collection, rollback and limitations instructions.
10. No API secrets or unredacted private logs are checked into Git.

### Execution plan
A. Inspect supplied project docs and create a checklist; ask only for essential unknowns, defaulting to fixture-only local development.
B. Build app skeleton and tests; show how to run locally.
C. Implement all seven UI sections using demo fixtures; label them `DEMO`.
D. Build safe snapshot-reader interfaces and optional sample collector scripts (not installed or executed on production).
E. Test schema validity, parsing, stale cases, redaction, XSS-safe display and loopback bind.
F. Produce a clear manual deployment plan, preserving existing server services.
G. Summarize files changed, tests run/results, untested production assumptions, and exact user approvals still needed.

### Context for report (do not turn into fabricated results)
This is a Linux build project with a 10–12-page APA report and 10–15-minute presentation. Existing hardening is historical context: user states root SSH login disabled; previously discussed UFW, SSH keys, Fail2ban, Lynis, Docker/Caddy/PostgreSQL but current state must be verified. Dashboard implementation is the new research contribution. Use `06_Evidence_and_Test_Log.md` to capture real testing; do not produce fictional data or sources.

## END OF COPYABLE AGENT INSTRUCTIONS

## What to tell the agent when you switch
"Implement this project locally with synthetic fixtures first. Do **not** connect to production or change my DigitalOcean Droplet. Pause at the point where live integration would require a deployment/security decision. Give me a file-by-file summary and run commands."
