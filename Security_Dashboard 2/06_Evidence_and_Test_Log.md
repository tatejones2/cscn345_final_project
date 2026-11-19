# 06 — Evidence and Test Log

Fill this in **during development**, not from memory afterward. Do not include secrets or raw IP lists.

## Session template
| Date/time (timezone) | Goal | Code changed | Commands / tests run | Result | Evidence filename | Next action |
|---|---|---|---|---|---|---|
| TODO | TODO | TODO | TODO | TODO | TODO | TODO |

## Verification matrix
| Feature | Fixture test result | Live Linux source/command | Collection timestamp + window | Observed data | Matches? | Limitations |
|---|---|---|---|---|---|---|
| System health | TODO | `uptime`, `free -h`, `df -h /` | TODO | TODO | TODO | TODO |
| SSH | TODO | journal/auth log, if permitted | TODO | TODO | TODO | TODO |
| Fail2ban | TODO | `fail2ban-client status <jail>` if authorized | TODO | TODO | TODO | TODO |
| UFW/ports | TODO | `ufw status`, `ss -tuln` | TODO | TODO | TODO | TODO |
| Timeline | TODO | bounded selected events | TODO | TODO | TODO | TODO |
| Lynis | TODO | dated saved report | TODO | TODO | TODO | TODO |
| Docker | TODO | minimal authorized container-status snapshot | TODO | TODO | TODO | TODO |

## Required tests
- [ ] Normal fixture data parses and renders.
- [ ] Command missing is reported as unavailable.
- [ ] Permission denied does not crash dashboard.
- [ ] Empty events count is not confused with inaccessible data.
- [ ] Missing/stale Lynis report clearly labeled.
- [ ] Docker permission denied does not trigger unsafe privilege escalation.
- [ ] Source timestamps and windows are displayed.
- [ ] `--demo` is visibly marked as demo, if implemented.
- [ ] Running the program does not change firewall rules, SSH settings or containers.
- [ ] No new public listening ports opened.

## Screenshot / evidence checklist
- [ ] Linux release and Python version (redacted)
- [ ] One-shot Rich terminal dashboard
- [ ] CLI error/unavailable state
- [ ] SSH + Fail2ban output comparisons (redacted)
- [ ] Firewall/port output comparison
- [ ] Dated Lynis summary if available
- [ ] Docker summary if available
- [ ] Test output / test matrix
- [ ] Presentation-safe prior hardening verification

## Results notes for paper
**What worked:** TODO

**What didn't work:** TODO

**Accuracy and measurement limitations:** TODO

**Security/privacy tradeoffs:** TODO

**Improvements with more time:** TODO
