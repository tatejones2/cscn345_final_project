# Security_Dashboard — Linux Security Monitor

**CSCN 345 Linux-focused programming project** | **Due: Tuesday, November 24, 2026** (confirm time in Canvas)

## Start here

You are **writing a Python program for Linux** that gathers, analyzes, and presents server-security information **inside the terminal**. The main deliverable is a working Linux terminal monitoring tool, **not a website**. A simple web GUI is a **stretch goal only** and must not delay testing, the paper, or submission.

Use your **existing hardened DigitalOcean Ubuntu server** as the data source. The project reads security information and **does not reconfigure production security controls**. Existing server hardening belongs in your background/presentation, not as newly completed project work.

**Your requested features:** SSH login attempts; Fail2ban status; UFW/firewall and ports; system health; security event timeline; dated Lynis results; Docker container monitoring.

**Paper:** **5–7 pages** for the *Linux-focused programming project* option, with **source code in the appendix**, per the assignment handout. Confirm whether the instructor counts title, reference, or appendix pages toward that total. **Presentation:** 10–15 minutes plus Q&A, per the handout.

## What to build

Run `python3 security_monitor.py` from a terminal on Linux. The program displays a read-only overview with clear source/timestamp labels, gracefully handles missing permissions, and can refresh manually or at a safe interval. **Python + Rich** is the default (simpler than Textual). Use Textual only if core features and tests are already finished. There is no need for a web server, database, public port, or Docker deployment.

**Build priority:** (P0) system health, SSH, Fail2ban, firewall/ports; (P1) security timeline, Docker, Lynis. Include the structure for all seven, but correctness + a complete paper outrank visual polish. Clearly mark any unfinished or unavailable feature.

## Recommended reading and working order

1. `01_Project_Scope.md` — research question, definition of done, boundaries
2. `02_Information_Needed.md` — inventory without exposing credentials
3. `05_Security_and_Privacy_Guardrails.md` — **before touching the live server**
4. `03_Seven_Day_Plan.md` — November 19–24 schedule
5. `04_Dashboard_Technical_Plan.md` — Python modules, adapters, command rules
6. `11_Manual_AI_Guided_Build.md` — **primary route**: you type the code; AI guides and checks
7. `13_Metric_Definitions_and_Verification.md` — metric definitions, validation
8. `06_Evidence_and_Test_Log.md` — capture research evidence throughout
9. `07_Prior_Server_Hardening.md` — verify previous protections for presentation
10. `08_Research_Paper_Outline.md` — **5–7-page** paper and source-code appendix
11. `09_Presentation_Guide.md` — 10–15-minute talk with terminal demo
12. `10_Submission_Checklist.md` — final review

**Alternative:** `12_AI_Agent_Build_Spec.md` is a stand-alone handoff for Claude Code or Codex if you decide to delegate implementation later. `14_Optional_Web_GUI.md` describes the *nonessential* GUI extension.

## First practical actions

- Make a working directory/repository locally; do not place application secrets in Git.
- Verify the server's Linux release and current service availability, using the commands in `02_Information_Needed.md`.
- Create the Python skeleton, tests and sample fixture files **before** adding live privileged data collection.
- Keep the program read-only. Never grant the monitoring app unlimited sudo or Docker socket access.
- Write a few lines in your evidence log **every session**, and reserve November 23–24 for the paper, validation and submission.

## Project outputs

- Python source and dependency list
- Running terminal monitor, tested on Ubuntu
- Test fixtures and documented test results, including missing-permission behavior
- Research paper (APA, 5–7 pages) with code in appendix
- Presentation and evidence/screenshots

## Security note

The server is already production-facing. **Do not** loosen firewall rules, enable root login, change SSH authentication, brute-force the server, or expose a monitoring endpoint. If live data is inaccessible, report `unavailable` and use clearly labeled demo fixtures for the class presentation. Never report fake values as live data.
