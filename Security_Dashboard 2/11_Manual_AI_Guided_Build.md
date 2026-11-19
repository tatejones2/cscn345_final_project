# 11 — Manual Build With AI Tutoring (PRIMARY METHOD)

**You write the code yourself.** Use an AI tutor for one small step at a time: explanations, code sketches, review, debugging and tests. Never let it assume your server's settings or silently modify production services.

## Teaching rules for any AI assistant
Copy this into a chat:

> You are my programming tutor for CSCN 345. I am manually building a Python Linux Security Monitor that runs in the terminal using Rich. Teach one checkpoint at a time. Explain the purpose and Linux concepts, show the next small code step, and let me type it. Ask me to run tests and share sanitized error output. Do not take over the project, write multiple modules at once, or change my production server without permission. Prioritize safe read-only collection and the November 24 deadline. Paper: 5–7 pages with code appendix.

## Checkpoint 0 — Prepare working environment
- [ ] Choose local VS Code folder and SSH Linux test environment.
- [ ] Create `app/` directory, Python venv and `requirements.txt`.
- [ ] Decide on safe baseline permissions. Do not create a public app server.
- [ ] Ask AI: *Help me set up a minimal Python project with Rich and pytest; explain every file.*
- **Done when:** Python script can print `Security Monitor` in terminal and tests can run.

## Checkpoint 1 — Define normalized metrics
- [ ] Implement one reusable result object (`source`, `collected_at`, `status`, `data`, `error`, `mode`).
- [ ] Create success, missing-command and permission-denied fixtures.
- **Done when:** tests confirm missing data isn't silently converted to zero.

## Checkpoint 2 — Server health
- [ ] Collect uptime, load, memory and disk through authorized local reads.
- [ ] Render metrics in a Rich table/panel.
- [ ] Compare against `uptime`, `free -h`, `df -h /`.

## Checkpoint 3 — SSH authentication
- [ ] Parse bounded sample log lines in tests first.
- [ ] Add 24-hour count + clear `window_start`/`window_end`.
- [ ] Read actual logs **only where already authorized**; otherwise show unavailable.
- [ ] Do not classify every failed login as a confirmed attack.

## Checkpoint 4 — Fail2ban
- [ ] Parse example `fail2ban-client status <jail>` output.
- [ ] Display separate *currently banned* and *total banned* fields.
- [ ] Add unavailable state for permission denial/jail not found.

## Checkpoint 5 — Firewall and listening ports
- [ ] Parse `ufw status` and `ss -tuln` output from safe fixture samples.
- [ ] Do not conflate local listening ports with internet-reachable ports.

## Checkpoint 6 — Timeline, Docker, Lynis (secondary)
- [ ] Timeline: normalize 10–20 bounded timestamped events and redact sensitive fields.
- [ ] Docker: use minimal trusted snapshot/import; don't add app to docker group.
- [ ] Lynis: import saved dated audit result; don't run on refresh.
- [ ] If blocked, report unavailable and record why.

## Checkpoint 7 — Terminal UX
- [ ] Render all available metrics in one one-shot Rich dashboard.
- [ ] Show time, source, status, error and `DEMO` label.
- [ ] Optional refresh flag only after basic output works safely.

## Checkpoint 8 — Test and document
- [ ] Run unit tests; test unavailable and stale values.
- [ ] Verify selected live readings against native Linux commands.
- [ ] Save redacted evidence and write implementation/results notes for the paper.

## Checkpoint 9 — Finish before GUI
- [ ] Complete 5–7-page paper and source-code appendix.
- [ ] Practice 10–15-minute terminal demo and prepare fallback screenshot.
- [ ] Only then consider `14_Optional_Web_GUI.md`.

## Debugging prompt
> I am on Checkpoint __. This is the code I typed (redacted) and the exact error. Explain what caused it, give the smallest safe correction, and tell me how to verify it. Do not make unrelated changes.
