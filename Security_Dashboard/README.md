# Security_Dashboard — CSCN 345 Term Project

**Primary workflow:** You write and run the code yourself, with an AI tutor guiding you one step at a time. **Alternative:** An AI coding agent can build the project from `12_AI_Agent_Build_Spec.md` if you change your mind.

**Due:** Tuesday, **November 24, 2026**. This plan begins **Wednesday, November 18**, leaving six calendar dates before the due date. Check Canvas for the exact submission time. Complete a usable dashboard by Nov 21 so the paper is not rushed.

## What this project is
Build a **private, read-only security dashboard** for your **already-hardened DigitalOcean Linux server**. The dashboard makes security activity and system status visible; the paper evaluates its design, implementation, accuracy, usefulness, and limitations. Explain earlier server hardening as **background**, not work newly performed for this assignment.

**Research question:** How effectively can a lightweight, read-only dashboard centralize security-related information on an existing hardened Linux server?

## Required deliverables
1. Working dashboard and source code (source code should be included because this is a built Linux-based project).
2. APA-compliant final research report, **10–12 pages** for a Linux-based build/project under the provided assignment sheet (confirm any instructor-specific update).
3. **10–15-minute** presentation plus Q&A, if due as part of this submission or later per course scheduling.
4. Evidence: screenshots, logged test outcomes, measured figures, and original source references.

## Quick navigation (read in this order)
| File | When to use it |
|---|---|
| `01_Project_Scope.md` | Lock scope, feature priorities, success criteria |
| `02_Information_Needed.md` | Collect safe facts about the live server and choose the development setup |
| `03_Seven_Day_Plan.md` | Follow the revised Nov 18–24 schedule |
| `04_Dashboard_Technical_Plan.md` | Choose architecture, data contracts, and collectors |
| `05_Security_and_Privacy_Guardrails.md` | Read **before** connecting an app to your production server |
| `11_Manual_AI_Guided_Build.md` | **Primary path:** step-by-step manual coding and AI tutor prompts |
| `12_AI_Agent_Build_Spec.md` | **Alternative path:** self-contained implementation instructions for Claude Code/Codex |
| `13_Metric_Definitions_and_Verification.md` | Make each displayed metric accurate and testable |
| `06_Evidence_and_Test_Log.md` | Log work, test cases, screenshots as you go |
| `07_Prior_Server_Hardening.md` | Document historical hardening for slides/paper |
| `08_Research_Paper_Outline.md` | Write the research report |
| `09_Presentation_Guide.md` | Build and rehearse slides |
| `10_Submission_Checklist.md` | Final quality, safety and submission review |

## Agreed dashboard features (seven)
1. SSH login attempts
2. Fail2ban monitoring
3. Firewall and listening ports
4. Server health
5. Security event timeline
6. Lynis audit results
7. Docker container monitoring

**Scope control:** Implement live system health, SSH/Fail2ban, firewall/ports first. Add timeline and Docker next. Show Lynis as the **most recent saved audit** with its run date, not as a continuously changing live score. If a data source is unavailable, show `Unavailable` or `Not configured`; never invent zero counts.

## First actions
1. Read `05_Security_and_Privacy_Guardrails.md`.
2. Fill in `02_Information_Needed.md` **without secrets, raw private logs or public IPs**.
3. Decide whether to code locally on your Mac (preferred) and how the dashboard will be kept private (SSH port-forward is the simplest initial choice).
4. Ask the AI tutor to guide you through **Checkpoint 1** in `11_Manual_AI_Guided_Build.md`.
5. Record the result in `06_Evidence_and_Test_Log.md`.

## Stop conditions
- Do not change working SSH settings or firewall rules just to make a dashboard work.
- Do not publish a log-reading API, bind it to `0.0.0.0`, mount the Docker socket, or grant the web app unrestricted sudo.
- Do not run invasive tests against the production Droplet; use passive observation, comparisons against authoritative local commands, and synthetic fixture logs.
- Never claim security events were 'attacks' unless independently substantiated.
