# 04 — Terminal-First Technical Plan

## Recommended stack
- **Python 3** on Ubuntu, virtual environment and `requirements.txt`.
- **Rich** for terminal tables, panels, colors and optionally `Live` refresh. Start with a one-shot screen; add refresh after tests pass.
- Standard Python modules: `subprocess`, `datetime`, `pathlib`, `re`, `json`, `argparse`, `logging`, `shutil`.
- `psutil` for system health if available; otherwise use `/proc`, `uptime`, `free`, `df` with clearly documented parsing.
- `pytest` for tests. No web server required.

## File layout to implement
```text
Security_Dashboard/
  README.md                         # project guide (this documentation package)
  ...
  app/                              # new code you create
    security_monitor.py             # CLI entry point
    requirements.txt
    .gitignore
    monitor/
      __init__.py
      models.py                     # source, timestamp, status, data, errors
      system.py                     # uptime/load, RAM, disk
      ssh.py                        # bounded authentication summary
      fail2ban.py                   # jail status/bans
      firewall.py                   # UFW and local listeners
      events.py                     # normalized recent log events
      docker.py                     # minimal container status
      lynis.py                      # dated saved audit import
      display.py                    # Rich terminal dashboard
    fixtures/                       # explicitly synthetic example outputs
    tests/                          # parsing and unavailable-path tests
```
This is a **target structure**, not a claim those Python files already exist.

## Program flow
```text
Ubuntu shell: python3 security_monitor.py
     |
Read-only Python collectors --> normalize result schema --> Rich terminal view
       /   |    |     |                   |
    /proc auth  f2b  ufw/ss            timestamps/status
           logs      docker / saved Lynis report
```

## Result schema
Every collector returns something equivalent to:
```python
{
    "source": "fail2ban-client status sshd",
    "collected_at": "2026-11-19T16:00:00+00:00",
    "status": "ok",  # or unavailable, error, stale
    "data": {"currently_banned": 4, "total_banned": 95},
    "error": None,
    "mode": "live"  # or demo
}
```
The numbers above are **illustrative**, not current server data. Use `None` for unknown; zero only for a measured zero.

## Collection strategy
- Use fixed allowlisted command argument arrays, `subprocess.run(..., shell=False, timeout=...)`, output limits, and careful parsing.
- Do not run untrusted shell fragments or permit user-selected commands to be executed.
- Default to executing as a **non-root user**. Privileged auth/firewall/Fail2ban or Docker data should be supplied by minimal pre-generated snapshots or explicitly authorized one-off commands. Never grant blanket `NOPASSWD: ALL` or add monitoring process to `docker` group just for the demo.
- For events, collect bounded, parsed and redacted entries; avoid permanently storing complete raw logs.
- Docker: `docker ps` can require root-equivalent socket access; use an admin-generated minimal snapshot or show unavailable.
- Lynis: load saved audit score + audit date. Do not run an expensive audit at every refresh.
- Avoid processes that loop indefinitely or overwhelm a 1 GB server: start with manual refresh/one-shot snapshot, then optionally add 15–30 second interval.

## CLI features
- `python3 security_monitor.py` — single dashboard snapshot.
- `python3 security_monitor.py --demo` — **clearly labeled fixture data**, no live access.
- `python3 security_monitor.py --refresh 30` — optional bounded refresh when implemented.
- `python3 security_monitor.py --help` — documented flags.

These are **planned CLI commands**, not guaranteed to run until you implement them.

## Definition of done for each module
1. A parseable, bounded result on valid fixture input.
2. A clear `unavailable` result when command is missing/access is denied.
3. Source and timestamp attached.
4. One comparison against actual read-only OS command or honest recorded limitation.
5. Unit test for success and failure conditions.

## Optional web GUI
Only if the tested terminal monitor and paper are done; see `14_Optional_Web_GUI.md`. Extract shared collectors first, then build a separate read-only UI. Do **not** start a web server on a public interface.
