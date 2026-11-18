# 04 — Technical Architecture and Implementation

## Recommended approach for manual learning
- Develop on Mac using VS Code, Git and **Python FastAPI** backend with plain HTML/CSS/JavaScript for the UI. This minimizes framework setup; React/Vite is an acceptable swap if preferred.
- Keep app source in a local `security-dashboard/` repo.
- Use an explicit **data adapter** (`fixtures` first, `live` later). This separates UI debugging from production access.
- For production, favor an **unprivileged read-only collector** writing selected sanitized JSON to a local protected file. The API reads that file; it does **not** need root access or a mounted Docker socket.
- Start backend on `127.0.0.1` only; view it via SSH tunnel. No new public DNS route required.

## Architecture
```text
Mac browser ---SSH authenticated tunnel---> Droplet 127.0.0.1:8765
                                             |
                                     dashboard API/UI (non-root)
                                             |
                                    sanitized JSON snapshots
                                             ^
                           narrowly scoped local collectors
                         (system, auth, f2b, ufw, docker, lynis)
```
Alternative during initial development: run UI/API locally on Mac with fixtures; only deploy after testing.

## Data model — all responses include
`collected_at` ISO-8601 timestamp (UTC), `source`, `status` (`ok`, `unavailable`, `error`, `stale`), `error_message` (safe summary), and `data` (shape specific to metric). Store source timestamps if events are timestamped independently. `null` means unavailable; `0` means observed zero.

## Suggested read-only routes
| Route | Example fields |
|---|---|
| `/api/health` | current snapshot age, collector status |
| `/api/system` | uptime seconds, load averages, RAM/disk utilization |
| `/api/ssh` | `window_start/end`, failed attempts count, accepted sessions when available |
| `/api/fail2ban` | jail name, currently banned, total banned, sampled time |
| `/api/firewall` | UFW active status, summarized inbound policy, sampled time |
| `/api/ports` | local address, protocol, port, process only if allowed |
| `/api/events` | bounded sanitized timeline items with `timestamp/type/summary/source` |
| `/api/lynis` | hardening index, scanned at, imported report filename |
| `/api/docker` | container name, state, reported health, collected at |

## Collectors and privilege boundaries
- System: `/proc`, `uptime`, `free`, `df`, or Python `psutil`.
- SSH: bounded journal or auth.log queries depending on Ubuntu configuration; preserve time window.
- Fail2ban: `fail2ban-client status <verified_jail>`; execute via a fixed allowlist only if a limited privileged helper is explicitly justified.
- UFW: `ufw status` requires rights on many systems; use pre-generated snapshot instead of giving the API sudo.
- Ports: `ss -tuln` generally usable without privileges; process details may be missing.
- Docker: `docker ps` requires socket access; **membership in docker group is root-equivalent**. Do not grant it to the dashboard user; a separate trusted local snapshot collector is safer.
- Lynis: import a dated, reviewed audit summary, not a web-triggered Lynis scan.
- Timeline: bound results (e.g. last 50), redact sensitive identifiers and full payloads.

## UI sketch
Top: title, last refresh, data freshness warning. Cards: SSH failed attempts (last 24h), currently banned, UFW status, CPU/RAM, Lynis snapshot score with audit date, running containers. Below: ports table, Docker status table, event timeline, explanation of source/limits.

## Manual development sequence
1. Create project directories `backend/`, `frontend/`, `fixtures/`, `tests/`, `docs/`.
2. Build fixture JSON and read-only routes; start loopback-only server.
3. Build static UI populated from routes.
4. Implement system collector and parser tests.
5. Implement auth, Fail2ban and UFW snapshot readers.
6. Add events, Docker, Lynis snapshot.
7. Add timestamp freshness, errors, safe logging, access tests.
8. Validate all cards and document deploy/rollback.

## No-go patterns
No API accepting arbitrary shell commands. No `shell=True` with user data. No browser-side credentials. No `chmod 777` on logs. No exposing Docker socket or database. No unauthenticated public dashboard. No simulated values presented as production facts.
