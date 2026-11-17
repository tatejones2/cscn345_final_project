# Research Paper Outline (APA; exploration project ~10–12 pages)

> This is a structure, not a prewritten paper. Fill it with verified observations and citations. Confirm instructor preferences on page count and APA formatting.

## Suggested title
Linux Server Hardening: Preventing and Detecting Unauthorized Access

## 1. Introduction (~1 page)
- Problem: public Linux hosts receive unsolicited network traffic; administrators need preventive and detective layers.
- Research question and hypothesis.
- Specific scope and expected contribution.

## 2. Background / literature (~2 pages)
- Ubuntu server and threat surface.
- OpenSSH public-key authentication and remote-access risks.
- Host UFW vs provider Cloud Firewall.
- Fail2ban as detection with temporary blocking; limitation of failure logs once password auth is disabled.
- Lynis as configuration auditing, not proof of immunity.

## 3. Methods (~2 pages)
- Droplet specifications, Ubuntu release, date/time window.
- Baseline collection commands and audit version.
- Sequence of controls implemented; maintain operational access.
- Test/verification procedures; risk controls and restrictions.

## 4. Implementation and results (~2–3 pages)
- Table of initial/final SSH policy, UFW and cloud firewall, update status, Fail2ban status.
- Lynis score and key recommendations before/after.
- Sanitized examples of observed authentication events, if any.
- Screenshots with figure captions and exact dates.

## 5. Discussion (~1 page)
- What prevention succeeded? What detection could you actually verify?
- Which changes improved security vs simply changed tool scores?
- Usability/troubleshooting trade-offs.

## 6. Limitations / lessons / conclusion (~1–2 pages)
- One public host, 7-day window, no controlled online attacks, possible baseline already hardened.
- Personal skills learned; security recommendations; future work.

## References
- APA references including Ubuntu/DigitalOcean/Lynis documentation and any research papers.
- Only cite sources actually used, verifying attribution and date.

## Tables/Figures to plan
- Table 1: Lab environment and baseline.
- Table 2: Before/after control verification.
- Table 3: Test observations, expected vs actual.
- Figure 1: System diagram.
- Figure 2: Lynis audit comparison.
