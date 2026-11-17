# Day 3 — Detect suspicious activity and enable updates

**Goal:** Use Fail2ban + logs for detection; confirm unattended security updates are configured.

## 1. Install Fail2ban and unattended-upgrades
```bash
sudo apt update
sudo apt install fail2ban unattended-upgrades
```
Read the installed Fail2ban configuration before editing; Ubuntu releases differ in log backends and `banaction`. Do **not** edit `jail.conf` directly.

## 2. Create a small local jail override
```bash
sudo nano /etc/fail2ban/jail.d/sshd-project.local
```
Paste:
```ini
[sshd]
enabled = true
port = ssh
maxretry = 5
findtime = 10m
bantime = 1h
```
These values are for your report, not universal best settings. **Do not blindly set `backend`, `logpath`, or `banaction`**: validate compatibility with your actual system and Ubuntu's journald/syslog arrangement.

Then:
```bash
sudo systemctl enable --now fail2ban
sudo fail2ban-client status
sudo fail2ban-client status sshd
sudo journalctl -u fail2ban -n 40 --no-pager
```
If the service fails or the jail is absent, inspect the journal and configuration before proceeding. Distinguish between 'installed and running', 'jail configured', and 'actual events detected'.

## 3. Inspect SSH and Fail2ban logs
```bash
sudo journalctl -u ssh --since '24 hours ago' --no-pager
sudo journalctl -u fail2ban --since '24 hours ago' --no-pager
sudo fail2ban-client status sshd
```
Depending on configuration, Fail2ban may also write `/var/log/fail2ban.log`; only use it if it exists.

**Important research nuance:** After SSH password authentication is disabled, the public service may not show the same repeated password-failure signatures as a deliberately password-enabled test VM. The absence of bans is **not proof of failure**, nor does a ban count prove the server is invulnerable. Explain what your live configuration can actually detect.

## 4. Security updates
```bash
sudo systemctl status unattended-upgrades --no-pager
cat /etc/apt/apt.conf.d/20auto-upgrades
sudo apt list --upgradable
```
If the auto-upgrades file isn't present or updates aren't enabled, follow Ubuntu documentation to configure them; check `sudo dpkg-reconfigure unattended-upgrades` as an interactive option. Verify actual APT configuration rather than relying only on service status. Apply normal available security updates during a maintenance window and reboot **only if required**, after confirming recovery access.

## 5. Evidence
- [ ] Screenshot of Fail2ban jail status.
- [ ] Screenshot or sanitized excerpt from authentication logs (real observations only).
- [ ] Document whether any attempts/bans were observed during your timeframe.
- [ ] Screenshot of automatic-update configuration.
- [ ] Add 1–2 paper paragraphs: how detection works and how it differs from prevention.

**No manufactured 'attacks' on the public Droplet.** If you need repeatable failed-login and ban demonstrations, do that in a **separate local VM lab**, with permission and isolation, not in your DigitalOcean environment.
