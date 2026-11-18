# 05 — Security and Privacy Guardrails (Read Before Deploying)

This server already hosts real services. The dashboard must **not weaken the existing protections**.

## Access
- Keep dashboard private using **SSH local forwarding** as first choice. Example *after* a backend has been safely started on the server:
```bash
ssh -p <VERIFIED_SSH_PORT> -L 8765:127.0.0.1:8765 <YOUR_USER>@<YOUR_SERVER>
```
Then browse `http://127.0.0.1:8765` on the Mac. Replace placeholders privately; do not paste credentials or your public address into documentation.
- Bind backend to `127.0.0.1`, not `0.0.0.0`. Verify with `ss -tuln` and an off-host connectivity test; a loopback-only app is not publicly reachable by itself.
- Do not expose it through public Caddy routes or publish container ports as `0.0.0.0:8765:8765`.

## Permissions
- Run API as a dedicated non-root user.
- Prefer periodic privileged **local data-collection snapshots** with minimal file read ACLs and sanitized JSON. The API user should have no general sudo privileges.
- Never let HTTP requests run `sudo`, `docker exec`, `ufw`, `fail2ban-client`, `journalctl`, or a shell command on demand.
- The Docker socket grants very powerful host access. Do not mount `/var/run/docker.sock` in the dashboard web process or add its account to the docker group.
- Do not touch PostgreSQL credentials or the sites behind Caddy.

## Data handling
- Store aggregates where possible, not full IPs/usernames. If IPs are included for research, mask/truncate and restrict retention.
- Limit event count and age. Sanitize log text as untrusted input and escape in the UI.
- Never place `.env`, secrets, private SSH keys, Docker credentials, or unredacted authentication logs in the repo or report.
- Keep a `collected_at` field and separate `unavailable` from observed zero.

## Production precautions
- Take a DigitalOcean snapshot/backup if feasible, and make a rollback plan. Avoid system changes just for the dashboard.
- Do **not** simulate attacks or intentionally weaken your live Droplet. Use fixture log data or your isolated Ubuntu VM for negative cases.
- Keep resource usage bounded: collectors should have timeouts, max output lines, and reasonable refresh intervals (e.g. 30–60 seconds UI refresh, 1–5 minutes snapshots).
- If permissions block a metric, show it as unavailable; don't broaden privileges hurriedly.

## Release gate
- [ ] Only loopback/private access verified.
- [ ] No mutating routes or command execution from browser.
- [ ] No wide sudo, Docker socket, privileged mounts, or exposed secrets.
- [ ] Auth logs redacted in UI and research screenshots.
- [ ] Existing website/containers unaffected; documented rollback.
