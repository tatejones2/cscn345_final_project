# CSCN 345 — Linux Server Hardening Project

**Time available:** 7 days. **Approach:** A new, dedicated DigitalOcean Ubuntu Droplet; defense + detection; report as you go.

## Your goal
Research question: **How do SSH hardening, host/cloud firewall restrictions, security updates, and Fail2ban improve the prevention and detection of unauthorized access on an Ubuntu server?**

Hypothesis: Implementing the selected controls will reduce unnecessary access paths and improve detection of repeated SSH failures compared with the original configuration. *This is a hypothesis, not a result.*

## Read in this order
1. `01_Daily_Guides/Day_1_Create_and_Baseline.md`
2. `01_Daily_Guides/Day_2_SSH_and_Firewalls.md`
3. `01_Daily_Guides/Day_3_Fail2ban_and_Updates.md`
4. `01_Daily_Guides/Day_4_Verify_and_Reaudit.md`
5. `01_Daily_Guides/Day_5_Paper_First_Half.md`
6. `01_Daily_Guides/Day_6_Paper_Second_Half.md`
7. `01_Daily_Guides/Day_7_Final_Check.md`

Use `02_Research_and_Paper/` for the proposal, methodology and paper outline. Fill out templates in `03_Evidence_Templates/` throughout the project. See `04_References/` for technical sources.

## Scope — do not expand this unless everything is finished
- **Prevention:** key-only SSH, no direct root SSH login, UFW and DigitalOcean Cloud Firewall, automatic security updates.
- **Detection:** Fail2ban for SSH + authentication logs.
- **Measurement:** Lynis hardening index and warnings; effective SSH settings; listening ports; firewall status; Fail2ban status and real log events.
- **Not included:** Wazuh, web applications, malware samples, port scanning strangers, credential attacks against your public Droplet, or auditd. Do not host intentionally vulnerable public services.

## Critical rules
- Use a **new, separate Droplet**; do not risk your existing website server.
- Set a spending limit/budget reminder. A Droplet incurs cost while it exists; snapshots/backups may add cost.
- **Never disable working SSH access until a second terminal proves the new login works.** Keep an active session open while changing SSH/UFW.
- Limit your Cloud Firewall SSH source to your trusted public IP if practical. If your IP changes, update the rule before connecting.
- Never paste private SSH keys, secrets, complete public IP information tied to your identity, or unredacted logs into the paper.
- Perform **active attack simulations only in an isolated local VM lab**; use the public Droplet for standard administration, configuration checks, and passive observation.
- A Lynis score is **not** a measure of resistance to all attacks. Describe specific controls and observed behaviors.

## Assignment requirements (from provided instructor document)
- Choose a Linux-focused project, conduct the work, record activities/results, write an **APA-compliant** research report about overview/method/results/lessons learned, and present for **10–15 minutes plus Q&A**.
- Exploration projects: **about 10–12 pages**.
- Instructor sheet: proposal **up to 2 pages by week 3**, final report in **week 11**, presentation at semester end. Your current 7-day deadline overrides planning pace, but check **Canvas** for actual due dates.
- Grade weight: **paper 60%**, **presentation 40%**.

## Target schedule
| Day | Output | Estimated time |
|---|---|---|
| 1 | New Droplet, baseline evidence | 2–3 h |
| 2 | SSH + firewall protections | 3–4 h |
| 3 | Fail2ban + updates + log observations | 2–3 h |
| 4 | Verification + second Lynis audit | 2–3 h |
| 5 | First half of research paper | ~3 h |
| 6 | Results, discussion, references | 3–4 h |
| 7 | APA review, submission; slides if required | 2–3 h + presentation time |

**Work on the paper every day.** Copy factual observations to the templates immediately, with dates and screenshots.
