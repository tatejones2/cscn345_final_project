# 07 — Previous Server Hardening (Historical Context)

**Purpose:** Support the presentation introduction and paper background. This is not the newly built dashboard. Mark all observations by date and distinguish direct proof from recollection.

## Known, supplied/previously observed
| Item | Status and evidence to gather |
|---|---|
| Root SSH login | **User explicitly states disabled root login.** Verify effective `PermitRootLogin` and note when observed. |
| SSH key authentication | Previously described as enabled/required; verify effective password and pubkey settings. |
| Nondefault SSH port | Previously mentioned port `2222`; verify whether current. A changed port is not a replacement for authentication. |
| UFW firewall | Previously used; record current status and allowed rules without exposing IP restrictions. |
| Fail2ban SSH jail | Previously configured and monitored; record jail names, current settings and sample status. |
| Lynis | Historical **hardening index 67** from earlier audit, **not verified as current**, and not proof of comprehensive security. Search for original dated result. |
| Caddy reverse proxy in Docker | Previously observed serving web apps with TLS and security headers; verify current configuration before describing. |
| PostgreSQL in Docker | Previously observed; being up/healthy is an availability status, not a hardening measure by itself. |

## Safe verification checklist
- [ ] OS release and date
- [ ] `sudo sshd -T | grep -E '^(port|permitrootlogin|passwordauthentication|pubkeyauthentication) '` — note context/Match caveat
- [ ] `sudo ufw status` (redact addresses)
- [ ] `sudo fail2ban-client status` and specific verified jail
- [ ] Audit filename, date, Lynis hardening index
- [ ] Service exposure via `ss -tuln`
- [ ] Docker/Caddy presence (no need to expose site secrets)

## How to describe the sequence in your paper/slides
1. **Before this term project:** Existing DigitalOcean server was hardened over time using SSH restrictions, firewall controls, and intrusion prevention/monitoring.
2. **Problem motivating new work:** Those protections generate separate logs and command-line views; quickly summarizing the server's state is cumbersome.
3. **New term project:** Design and build a private dashboard to consolidate selected security and operational indicators.
4. **Evaluation:** Compare dashboard data with the authoritative source output, test private access, and note limitations.

## 60-second presentation script outline
"I already operated a hardened Ubuntu server. For example, I disabled root SSH login and had previously configured [insert controls you verified]. I used tools such as [verified items]. Instead of repeating the hardening as this semester's work, my project creates a new read-only security dashboard to consolidate information those systems already produce."

## Fill in verified hardening chronology
| Approx date | Control | What changed | Evidence source | Current verified? |
|---|---|---|---|---|
| TODO | Root SSH login disabled | TODO | `sshd -T`/config | TODO |
| TODO | UFW | TODO | rules/status | TODO |
| TODO | Fail2ban | TODO | jail config/status | TODO |
| TODO | Lynis | TODO | dated report | TODO |
