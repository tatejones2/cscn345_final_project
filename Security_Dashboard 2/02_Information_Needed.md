# 02 — Safe Server Inventory

**Do not share credentials, public IP address, keys, API tokens, raw authentication logs, or entire IP ban lists.** Redact usernames/IPs, domain and private infrastructure details in screenshots.

## Known history (not verified as current)
- DigitalOcean Linux server; Docker-hosted apps, Caddy reverse proxy and PostgreSQL were previously discussed.
- You stated **root SSH login was disabled**.
- Previously discussed UFW, Fail2ban SSH jail, SSH key authentication and an earlier Lynis hardening index of **67**. That score is historical, not a current measurement.
- Prior SSH port may have been customized; verify rather than assuming.

## Collect these facts
| Item | Value / evidence |
|---|---|
| Linux distribution + release | TODO |
| Python version | TODO |
| Current SSH port and root-login rule | TODO |
| Auth logs: journal or auth.log | TODO |
| Fail2ban installed, jail name | TODO |
| UFW installed/active | TODO |
| Docker available and permission level | TODO |
| Lynis report path, scan date and score | TODO |
| Available runtime user and minimum safe permissions | TODO |
| Canvas deadline time / presentation date | TODO |

## Safe read-only inventory commands
Run separately; **inspect output before copying or sharing**.
```bash
cat /etc/os-release
python3 --version
uname -r
uptime
free -h
df -h /
ss -tuln
sudo ufw status
sudo fail2ban-client status
systemctl is-active ssh
systemctl is-active fail2ban
docker ps --format 'table {{.Names}}	{{.Status}}'
```

`sudo sshd -T | grep -E '^(port|permitrootlogin|passwordauthentication|pubkeyauthentication) '` checks effective global SSH settings (per-client `Match` rules may differ). For Linux auth data, first check `sudo journalctl -u ssh --since '1 hour ago' --no-pager`; never paste raw IP addresses without redaction.

## Decisions already made
- **Main UI:** terminal, Python + Rich.
- **Development:** you manually write code with step-by-step AI assistance.
- **Optional alternative:** coding-agent handoff document.
- **Optional stretch goal:** separate lightweight web GUI after core deliverables.
- **Runtime:** existing DigitalOcean Ubuntu server; no additional public endpoints.
