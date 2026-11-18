# 02 — Information to Collect (Safe Server Inventory)

The AI tutor needs **facts**, not credentials. Paste redacted **outputs** or summarize findings; do not paste public IP, private key, API token, `.env`, auth cookies, email addresses, complete ban-IP lists, or raw logs with personal data.

## Already known (historical; verify current state)
- Existing DigitalOcean server, likely Ubuntu; previous Docker deployment with Caddy and PostgreSQL.
- User explicitly confirmed **root SSH login is disabled**.
- Prior discussion suggests SSH key login, customized SSH port **2222** (verify current), UFW, Fail2ban SSH jail, Docker, PostgreSQL and a previous Lynis score **67** (old, not current).
- PostgreSQL container `postgres:16-alpine` was previously observed healthy; Caddy reverse proxy previously used. Neither fact implies they are still configured the same way.

## Information still needed
| Question | Fill in |
|---|---|
| Ubuntu release (`cat /etc/os-release`) | TODO |
| Current SSH port (inspect `sudo sshd -T` output; redact other details) | TODO |
| Is UFW active (`sudo ufw status`)? | TODO |
| SSH Fail2ban jail name/status (`sudo fail2ban-client status`) | TODO |
| Where do SSH logs appear (`journalctl -u ssh` or `/var/log/auth.log`)? | TODO |
| How are apps deployed: Compose, Docker CLI, systemd? | TODO |
| Do you want local Mac development with SSH tunnel? (Recommended: yes) | TODO |
| Current Lynis report exists and is dated? | TODO |
| Docker permission model (can an unprivileged account read `docker ps`?) | TODO |
| App language preference: Python + FastAPI + basic HTML/JS, or existing React stack? | TODO |
| Paper due time in Canvas on Nov 24 | TODO |

## Safe discovery commands (run individually; inspect before sharing)
```bash
cat /etc/os-release
uname -r
uptime
free -h
df -h /
ss -tuln
sudo ufw status
sudo fail2ban-client status
sudo systemctl is-active ssh
sudo systemctl is-active fail2ban
docker ps --format 'table {{.Names}}	{{.Status}}	{{.Image}}'
```
- `sudo sshd -T | grep -E '^(port|permitrootlogin|passwordauthentication|pubkeyauthentication) '` is useful for effective SSH config but confirm any `Match`-specific behavior separately.
- `sudo journalctl -u ssh --since '1 hour ago' --no-pager | tail -n 15` may contain IPs/usernames; redact before sharing.
- `sudo fail2ban-client status sshd` only if your jail is actually called `sshd`.
- `sudo lynis show report` may not give a prior completed audit; find a dated existing report instead of running a fresh audit without recording the date.

## Decisions for the tutor
- [ ] I will type/edit and understand my own code; AI offers one checkpoint at a time.
- [ ] I will initially build and test locally with fixture data.
- [ ] My production dashboard will listen only on `127.0.0.1`, accessed by SSH port forwarding; or I will document an equivalently private authenticated solution.
- [ ] I will not modify the existing Caddy/Docker/website configuration unless there is a demonstrated need and safe rollback.
