# 01 — Project Scope and Research Plan

## Project title
**Security_Dashboard: Designing a Private Linux Server Security Monitoring Dashboard**

## Classification against assignment
Linux-based software/project that you build. New contribution: dashboard source code, data integration, validation, and user interface. Existing hardening: prior system context. The handout calls for ~10–12 pages for a Linux project plus source code, and 10–15 minutes of presentation.

## Research question
How effectively can a lightweight, read-only dashboard consolidate security indicators from a previously hardened Linux server while maintaining data accuracy and limited access?

## Objectives
- Display seven requested categories; prioritize a useful, demonstrable subset if time is short.
- Show metric timestamps, source, and collection errors.
- Compare dashboard values against native Linux command output.
- Explain what earlier hardening measures protect the system, and what dashboard visibility adds.
- Restrict dashboard access to the owner.

## Feature priority
| Priority | Feature | Definition of done |
|---|---|---|
| P0 | Server health | Uptime, CPU/load, RAM/disk, timestamp, permission errors handled |
| P0 | SSH login attempts | Recent failed/successful login counts where logs support them; explicit time window |
| P0 | Fail2ban | Jail status, currently banned and cumulative bans labeled separately |
| P0 | UFW + ports | Firewall status + TCP listening ports with process names when permitted |
| P1 | Security timeline | 20–50 recent sanitized, time-stamped events; filter/type grouping |
| P1 | Docker | Container names, running state, health when reported; no docker.sock in browser |
| P1 | Lynis | Latest saved report score and date, documented audit import process |

**Minimum viable deliverable:** All four P0 views working correctly with screenshots and verification. Aim for all seven, but paper completion takes priority over polish. If a P1 feature is incomplete, say so in the report and demo.

## In scope
- Read-only views of existing server metrics, selected auth logs, Fail2ban status, UFW status, listening sockets, Docker summaries, and last Lynis report.
- Private access, logging of collection errors, source-to-widget validation, concise documentation.

## Out of scope
- Running attacks, brute-force demonstrations on the public server, changing SSH/firewall rules from the UI, automatic remediation, public SaaS access, SIEM-scale search/storage, threat scoring based on guesses, exposing raw database contents, and Docker management actions.

## Research method
1. Inventory the current server (non-disruptive).
2. Define data sources and consistent JSON schema.
3. Build local prototype with saved/synthetic fixture data.
4. Connect read-only collectors using least privilege.
5. Keep access private; test with SSH forwarding or an approved VPN.
6. Validate every metric with server commands and documented time windows.
7. Test missing data, errors, sensitive-data handling, and private access.
8. Evaluate visibility, reliability, limits, and future improvements.

## Success criteria
- [ ] P0 features show real, timestamped, verifiable data.
- [ ] Missing metrics are clearly distinguished from zero.
- [ ] App is not accessible to the unauthenticated public internet.
- [ ] No dashboard route can change host state.
- [ ] At least five documented verification tests pass, including an error/unavailable case.
- [ ] Paper and presentation accurately distinguish old hardening work from new dashboard work.
