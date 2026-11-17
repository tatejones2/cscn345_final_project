# CSCN 345 — Linux Server Hardening Project Guide

**Start here.** This folder is your step-by-step guide for completing the hands-on Linux server hardening project **and** its research paper in seven days.

**Project title:** *Linux Server Hardening: Preventing and Detecting Unauthorized Access*  
**Main question:** How do SSH hardening, firewall restrictions, security updates, and Fail2ban improve prevention and detection of unauthorized access on an Ubuntu server?  
**Environment:** A **new, separate DigitalOcean Ubuntu Droplet** (not your existing website server).  
**Final products:** A documented hands-on project, an APA-compliant **10–12-page research report**, and a **10–15-minute presentation plus Q&A** (check whether the presentation is due in the same seven-day window).

> **First rule:** Save evidence *before* changing security settings. You need a baseline to compare against your final configuration.

## 1. How to use this folder

1. Read this README, then [00_START_HERE.md](00_START_HERE.md) for the full scope and safety rules.
2. Open the guide for your current day in [`01_Daily_Guides/`](01_Daily_Guides/). Follow it in order, including its verification steps.
3. **As you work**, fill in the evidence templates in [`03_Evidence_Templates/`](03_Evidence_Templates/). Keep copies of command output and redacted screenshots in a separate `evidence/` folder you create locally.
4. Use the worksheets in [`02_Research_and_Paper/`](02_Research_and_Paper/) to describe your *actual* setup, methods, and results. Do not write expected outcomes as if they happened.
5. Consult [`04_References/Official_Documentation.md`](04_References/Official_Documentation.md) when you need technical references and sources for your paper.
6. Before finishing, check the [final completion checklist](#6-final-completion-checklist) below.

**If you fall behind:** Prioritize baseline + SSH + firewalls + Fail2ban + final audit + paper. Do not add optional tools or extra experiments.

## 2. Folder map

```text
Linux_Server_Hardening_Project/
├── README.md                         ← YOU ARE HERE
├── 00_START_HERE.md                  ← Project scope, safety, requirements
├── 01_Daily_Guides/
│   ├── Day_1_Create_and_Baseline.md
│   ├── Day_2_SSH_and_Firewalls.md
│   ├── Day_3_Fail2ban_and_Updates.md
│   ├── Day_4_Verify_and_Reaudit.md
│   ├── Day_5_Paper_First_Half.md
│   ├── Day_6_Paper_Second_Half.md
│   └── Day_7_Final_Check.md
├── 02_Research_and_Paper/
│   ├── Project_Proposal_Template.md
│   ├── Methods_Worksheet.md
│   └── Paper_Outline.md
├── 03_Evidence_Templates/
│   ├── Daily_Research_Log.md
│   ├── Baseline_vs_Final.md
│   ├── Test_Results.md
│   └── Evidence_File_Naming.md
└── 04_References/
    └── Official_Documentation.md
```

The Markdown files are **guides and templates**, not completed research or a finished paper. Fill them with the results you observe.

## 3. Seven-day route: what to open and what to finish

| Day | Open this guide | Your deliverable at the end of the day | Time budget |
|---|---|---|---|
| **1 — Baseline** | [Day 1](01_Daily_Guides/Day_1_Create_and_Baseline.md) | New Droplet; recorded initial SSH, ports, firewall and Lynis findings; first research-log entry | 2–3 h |
| **2 — Prevention** | [Day 2](01_Daily_Guides/Day_2_SSH_and_Firewalls.md) | Verified SSH key login, no direct root/password SSH login, correctly restricted UFW and cloud firewall | 3–4 h |
| **3 — Detection** | [Day 3](01_Daily_Guides/Day_3_Fail2ban_and_Updates.md) | Fail2ban running; reviewed logs; checked unattended security updates; saved evidence | 2–3 h |
| **4 — Compare** | [Day 4](01_Daily_Guides/Day_4_Verify_and_Reaudit.md) | Verified controls, second Lynis audit, completed comparison and test tables | 2–3 h |
| **5 — Paper part 1** | [Day 5](01_Daily_Guides/Day_5_Paper_First_Half.md) | Introduction, background, and methods drafted from real evidence | ~3 h |
| **6 — Paper part 2** | [Day 6](01_Daily_Guides/Day_6_Paper_Second_Half.md) | Results, discussion, limitations, conclusion, and references drafted | 3–4 h |
| **7 — Finish** | [Day 7](01_Daily_Guides/Day_7_Final_Check.md) | APA review, verified figures and citations, final submission; presentation prep as needed | 2–3 h + slides |

These are estimates, not guaranteed durations. **Write notes every day**, including Days 1–4, to avoid having to reconstruct your work later.

## 4. What to record while working

Keep these four files updated:

- [Daily_Research_Log.md](03_Evidence_Templates/Daily_Research_Log.md): what you attempted, when, commands/settings used, problems, and what you learned.
- [Baseline_vs_Final.md](03_Evidence_Templates/Baseline_vs_Final.md): initial versus final Lynis and security configuration findings. **Never invent scores.**
- [Test_Results.md](03_Evidence_Templates/Test_Results.md): what you verified, expected outcome, actual outcome, and evidence.
- [Evidence_File_Naming.md](03_Evidence_Templates/Evidence_File_Naming.md): naming convention for screenshots and saved output.

Suggested daily workflow: **read instructions → make change → verify change → save redacted evidence → log what happened → write 2–4 paper notes**.

**Evidence you should aim to collect:** initial/final Lynis output, effective SSH settings, UFW and DigitalOcean firewall rules, Fail2ban jail/service status, security-update configuration, and relevant authentication log observations. If you do not see login attempts or bans, report that accurately; do not manufacture an event.

## 5. Paper and presentation path

Start with [Paper_Outline.md](02_Research_and_Paper/Paper_Outline.md) and [Methods_Worksheet.md](02_Research_and_Paper/Methods_Worksheet.md). Your paper should explain **why** these controls matter, **exactly how** you configured and verified them, **what you measured**, **what actually happened**, and **what you learned**. Use [Official_Documentation.md](04_References/Official_Documentation.md) as a starting point for sources, and cite only what you use.

The assignment instructions specify an APA-compliant exploration report of approximately **10–12 pages**, a proposal of **up to 2 pages** (see [Project_Proposal_Template.md](02_Research_and_Paper/Project_Proposal_Template.md)), and a **10–15-minute presentation with Q&A**. The instructor's original milestone weeks may differ from your current deadline: **verify the exact dates and deliverables in Canvas**.

Suggested presentation flow: project question → server setup → baseline → prevention measures → Fail2ban/log monitoring → before/after results → limitations and lessons. Use redacted screenshots as backup if a live demo is inconvenient.

## 6. Final completion checklist

### Server and evidence
- [ ] Droplet is separate from existing production sites.
- [ ] Initial baseline and Lynis output were recorded **before hardening**.
- [ ] A non-root account can connect with SSH keys; a **new SSH session** was verified before disabling old login methods.
- [ ] Direct root and password SSH logins are disabled and verified.
- [ ] UFW and DigitalOcean Cloud Firewall restrictions are verified.
- [ ] Fail2ban status and authentication logs are recorded accurately.
- [ ] Automatic security update configuration is checked.
- [ ] Final Lynis audit and before/after comparison are complete.
- [ ] Test results distinguish **observed behavior** from expectations.

### Writing and submission
- [ ] The report covers introduction, background, methods, results, discussion, limitations, and conclusion.
- [ ] Screenshots/tables are labeled, readable, and redacted.
- [ ] Citations, references, and formatting are APA compliant.
- [ ] The report meets your instructor's page count and actual deadline.
- [ ] Presentation slides or demo are prepared if due.
- [ ] Any required proposal or other deliverable has been handled.
- [ ] Droplet is destroyed after evidence collection when no longer needed, to avoid ongoing charges (preserve research files first).

## 7. Safety and troubleshooting reminders

- **Do not lock yourself out:** keep an existing SSH session open while changing SSH/firewall rules; verify a second SSH login works before ending the first.
- Restrict SSH access to a trusted source IP when practical, and remember your public IP may change.
- Do **not** run password-guessing attacks, aggressive scans, or intentionally vulnerable public services on the Droplet. If controlled attack simulation is needed, use an **isolated local VM lab** instead and respect provider policies.
- Before sharing screenshots or log extracts, remove secrets and minimize public IP addresses and identifying information.
- An improved Lynis index means a better result on that audit, **not** proof that the host cannot be compromised.

**Next action:** Open **[Day 1 — Create and Baseline](01_Daily_Guides/Day_1_Create_and_Baseline.md)**, make your new Droplet, and capture the initial measurements before changing settings.
