# 01 — Project Scope and Research Plan

## Project classification
**Linux-focused programming project** (not merely a Linux system exploration and not a web application). Build an original Python program that collects, parses, normalizes, and displays Linux security telemetry in the terminal. The handout specifies **5–7 pages and source code in the appendix** for this category. A 10–15-minute presentation is also required.

## Title
**Developing a Python-Based Linux Security Monitoring and Analysis Tool**

## Research question
How effectively can a custom, read-only Python terminal tool consolidate and accurately display security information from an already-hardened Ubuntu Linux server?

## Hypothesis
A modular terminal monitor can reduce the effort needed to inspect several security subsystems while preserving accurate source information and avoiding changes to the server's configuration. The project evaluates **visibility and correctness**, not whether monitoring guarantees security.

## Success criteria
- Python code written for and demonstrated on Linux; start from shell with `python3 security_monitor.py`.
- Implement working **P0**: system health, SSH event summary, Fail2ban status, UFW status and listening ports.
- Add **P1**: selected security timeline, Docker state, last dated Lynis audit, as time and permissions permit.
- Display `collected_at`, metric measurement windows, source, and `ok/unavailable/error/stale` status; distinguish real vs fixture data.
- Safely handle missing logs, missing command, restricted permissions, stopped services and empty results.
- Validate representative values against native Linux commands and record results.
- Source code, unit tests or test fixtures, README and 5–7-page APA paper with source code appendix.

## Scope limits
- No attack automation, brute forcing, active scans against third parties, changing bans, firewall administration, SSH policy edits or service restarts.
- No public web UI, cloud dashboard, PostgreSQL storage, Docker socket in an application, or heavyweight SIEM.
- Prior Linux hardening is **context** for results and presentation, not the original programming contribution.

## Method
1. Inventory accessible tools and operating-system services.
2. Define a uniform result schema and create example fixtures.
3. Write independent Python collectors using safe, fixed commands or read-only interfaces.
4. Add parsing, timeline normalization and an accessible Rich terminal output.
5. Test with fixtures, then validate against read-only native tools on Ubuntu.
6. Compare collection accuracy, completeness, latency, limitations and ease of use.
7. Document outcomes with redacted evidence, paper and presentation.

## Deliverables
Working Python project (code, requirements, tests, fixtures, usage guide), evidence log, APA report (5–7 pages plus appendix as applicable) and 10–15-minute presentation.
