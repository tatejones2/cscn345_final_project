# 09 — Presentation Guide (10–15 Minutes + Q&A)

## Suggested flow
1. **Title / motivation (1 min)** — Python-based Linux security monitor.
2. **Existing server background (1–2 min)** — earlier hardening: root SSH login disabled; mention previously configured UFW/Fail2ban only after verification.
3. **Research question and design (1–2 min)** — terminal-first, read-only, Linux-focused program; why Python + Rich.
4. **Code architecture (2 min)** — modules, source data, parsing, data schema and unavailable status.
5. **Live terminal demo (3–4 min)** — run `python3 security_monitor.py`; show health, SSH, Fail2ban, UFW/ports; show additional features if working. Identify demo data when applicable.
6. **Tests and results (1–2 min)** — compare readings to native command sources; demonstrate missing-permission handling.
7. **Lessons / limitations / next steps (1–2 min)** — permissions, log variability, Docker privilege, optional GUI.

## Demo safety
- Practice a local pre-recorded/screenshot fallback if SSH is unreliable.
- Avoid public IP addresses, usernames, secret tokens, complete raw logs and uncontrolled commands on screen.
- Run as a normal user; keep your existing apps and firewall unchanged.
- Do not depend on live suspicious traffic or start brute-force tests during the presentation.

## One-sentence takeaway
> I built an original Python program that consolidates several native Linux security indicators into a read-only terminal interface, and I verified its output against the underlying tools.

## Supporting visuals
- Terminal monitor screenshot
- Simple collector-to-terminal architecture diagram
- Test comparison table
- Before-existing-controls diagram (historical, not new work)
- Optional web GUI **only if completed**, clearly described as an extension
