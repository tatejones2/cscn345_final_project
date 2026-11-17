# Security Test Results

Each row must represent an actual check, with its actual outcome. Label tests conducted in a **local VM** distinctly from checks on the **public Droplet**.

| Test ID | Location | Purpose | Method | Expected | Actual observed | Proof | Pass/Fail/Unknown |
|---|---|---|---|---|---|---|---|
| T1 | Droplet | Authorized SSH access | New key-based session | Connect succeeds | | | |
| T2 | Droplet | SSH password prevention | Single password-only connection attempt | Password not offered | | | |
| T3 | Droplet | Root SSH policy | Effective config review | Root login disabled | | | |
| T4 | Droplet | Inbound host restriction | UFW config/status review | Default incoming deny, SSH allowed | | | |
| T5 | Droplet | External network policy | Cloud Firewall settings review | Only intended incoming rules | | | |
| T6 | Droplet | Fail2ban monitoring | Jail state + log review | sshd jail exists | | | |
| T7 | Droplet | Audit change | Lynis before/after | Changes recorded, direction unknown | | | |
| T8 (optional) | Isolated local VM | Repeated failures detection | Intentionally incorrect login attempts to own lab-only VM | Fail2ban detects failures, then possible ban | | | |

## Observed suspicious activity
- Observation window and timezone:
- Log source (`journalctl`, fail2ban logfile):
- Count/description (only if actually observed):
- Any ambiguity about automated vs benign traffic:

## Interpretation
- What was **prevented**:
- What was **detected**:
- What **was not tested**:
