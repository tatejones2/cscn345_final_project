# CSCN 345 — Project Proposal Template (maximum 2 pages)

**Proposed title:** Linux Server Hardening: Preventing and Detecting Unauthorized Access

**Student:** [Your name]  
**Course / section:** CSCN 345  
**Date:** [Date]

## Project overview
[Describe why server hardening matters and that you will use a new, dedicated Ubuntu DigitalOcean Droplet. State what you will and will not attempt.]

## Research question and hypothesis
**Research question:** How do SSH hardening, host/cloud firewall restrictions, security updates, and Fail2ban improve the prevention and detection of unauthorized access on an Ubuntu server?

**Hypothesis:** [Your hypothesis, as a prediction, not a claimed result.]

## Method
1. Record the original Ubuntu version, SSH policy, UFW policy, exposed services, and initial Lynis audit.
2. Apply SSH key-only authentication, prohibit direct root SSH login, set incoming firewall rules, enable security updates.
3. Configure Fail2ban and inspect authentication logs for detection events.
4. Verify settings and login behavior, run final Lynis audit, compare findings.
5. Discuss strengths, limitations and security recommendations; keep active attack simulations off the public provider infrastructure.

## Tools and resources
DigitalOcean Ubuntu Droplet, Mac Terminal/OpenSSH, UFW, Fail2ban, Lynis, Ubuntu package updates, DigitalOcean Cloud Firewall, journalctl.

## Expected deliverables
- A configured Ubuntu server with documented preventive/detective controls.
- Baseline-versus-final results, configuration verification evidence, logs, and screenshots.
- An APA-compliant approximately **10–12-page exploration report**.
- A **10–15-minute presentation**, plus Q&A.

## Timeline
[Add your actual 7-day schedule and Canvas due date.]

## Risk management
[Describe second-terminal SSH verification, recovery access, separate public Droplet, controlled scope, sanitization of logs, and local VM testing for active simulations.]

**Instructor approval:** [Date/status — check whether original week-3 proposal deadline has passed and whether approval is still required.]
