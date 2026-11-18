# 03 — Schedule: Nov 18–24, 2026

**Today:** Wed Nov 18. **Deadline:** Tue Nov 24 (confirm Canvas time). **Six calendar days after today.** Allocate roughly 2–5 focused hours per day, with buffer. Start writing on Day 1.

## Wed Nov 18 — Scope + inventory + skeleton (2–3 h)
- [ ] Read guardrails, inventory services safely, confirm dev stack.
- [ ] Create Git repo and app skeleton; create first `/api/health` or fixture endpoint.
- [ ] Start methods section, record existing hardening context.
- **Evidence:** current OS, service overview, architecture sketch, initial commit.

## Thu Nov 19 — Collectors: health + SSH/Fail2ban (3–4 h)
- [ ] Build fixtures first, then read-only metrics adapter.
- [ ] Display explicit timestamp and SSH time window.
- [ ] Validate health and one Fail2ban reading against native commands.
- **Evidence:** command comparisons, screenshots, error handling.

## Fri Nov 20 — Firewall/ports + privacy (3–4 h)
- [ ] Add read-only UFW status and listening port list.
- [ ] Keep backend loopback-only; test SSH tunneling.
- [ ] Implement unavailable statuses for missing access.
- **Evidence:** loopback listening proof and source-versus-dashboard values.

## Sat Nov 21 — Timeline + Docker + Lynis snapshot (3–5 h)
- [ ] Add bounded event timeline with redaction.
- [ ] Add Docker container status via narrowly privileged collection.
- [ ] Import a dated Lynis report; show as snapshot rather than live.
- [ ] Freeze features at end of day; prioritize correctness over polish.
- **Evidence:** finished demo screenshots, test matrix.

## Sun Nov 22 — Validate and write report (3–5 h)
- [ ] Test source accuracy, missing data, stale data, non-public access.
- [ ] Draft introduction/background, design/methods, implementation and results.
- [ ] Collect citations from vendor documentation and credible security sources.

## Mon Nov 23 — Complete report + slides (3–5 h)
- [ ] Finish APA report 10–12 pages and references.
- [ ] Complete 10–15 minute slide deck; demonstrate verified results.
- [ ] Record limitations and unfinished P1 features explicitly.

## Tue Nov 24 — Final checks and submission (1–3 h)
- [ ] Test startup from README, export code and evidence.
- [ ] Proofread and check APA requirements and page length.
- [ ] Confirm demo is private, backup/export materials, submit well before Canvas closes.

## If behind schedule
1. Stop adding features.
2. Ensure health, SSH/Fail2ban, and UFW/ports accurately display.
3. Document P1 work honestly as incomplete or future scope.
4. Protect time for the paper (60% of grade) and presentation (40%).
