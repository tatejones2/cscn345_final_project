# 07 — Previously Completed Server Hardening (Presentation Background)

## Important distinction
These steps were performed **before this programming assignment**. Discuss them as the reason you have valuable security data to monitor; do not represent them as newly implemented in the term project.

## Historical hardening inventory
| Control | Current confidence | Evidence to collect safely |
|---|---|---|
| Root SSH login disabled | **User explicitly confirmed previously**; verify current value | `sudo sshd -T | grep '^permitrootlogin '` (global effective config) |
| SSH key authentication | Discussed previously; **verify** | `sudo sshd -T | grep -E '^(pubkeyauthentication|passwordauthentication) '` |
| Customized SSH port | Historical mention, may have been 2222; **verify** | `sudo sshd -T | grep '^port '` |
| UFW firewall rules | Discussed previously; **verify** | `sudo ufw status` (redact sensitive details) |
| Fail2ban sshd jail | Discussed previously; **verify** | `sudo fail2ban-client status`; inspect selected jail |
| Lynis audit | Previous reported hardening index **67**; historical only | saved report with date, not a newly inferred live score |
| Docker + Caddy | Previously observed in server setup; **verify** | safe aggregate container information, if authorized |

## Presentation narrative (roughly 1–2 minutes)
1. Explain that the server was previously hardened using SSH access controls, a firewall, and Fail2ban.
2. Show **verified current configuration** for 1–2 controls and historical Lynis findings with a visible audit date if available.
3. Explain the remaining problem: to review security activity you previously had to run multiple commands and inspect several logs.
4. Introduce the **new work**: your Python security-monitoring program centralizes and interprets that information in the terminal.

## Avoid exaggerated claims
- A Lynis index is not a guarantee of security or vulnerability count.
- Every failed login is not necessarily an attack.
- A running Docker container does not guarantee that its software is secure.
- Only present a setting as currently active after checking it.

## Verification notes
Date: TODO

Commands reviewed: TODO

What is verified now: TODO

What remains historical/unverified: TODO
