# Day 4 — Verify controls and compare results

**Goal:** Gather repeatable proof that configurations changed, and collect a second Lynis audit.

## 1. Verification checklist
On the Droplet:
```bash
sudo sshd -t
sudo sshd -T | grep -Ei '^(port|permitrootlogin|passwordauthentication|pubkeyauthentication|kbdinteractiveauthentication) '
sudo ufw status verbose
sudo ss -tulpen
sudo fail2ban-client status sshd
sudo journalctl -u ssh --since '24 hours ago' --no-pager
cat /etc/apt/apt.conf.d/20auto-upgrades
```
Capture outputs with dates. A service can be listening yet blocked by firewalls; a process not listening may have little relevance to remote exposure. Avoid overstating results.

## 2. Final Lynis audit
```bash
sudo lynis audit system
sudo cp /var/log/lynis.log /root/lynis-after.log
sudo cp /var/log/lynis-report.dat /root/lynis-after-report.dat
sudo grep -E '^hardening_index=' /root/lynis-after-report.dat
```
Compare results with Day 1, ideally using the **same Lynis version**. If you upgraded the audit tool in between, disclose it. Lynis is a configuration-audit indicator, not a real-world breach-risk percentage.

## 3. Experiments to report
| Test | Method | What you can conclude |
|---|---|---|
| SSH key access | New non-root SSH login | Authorized key authentication works |
| SSH password login | Single password-only login attempt | Password method offered/refused at this time |
| Root SSH login | `sshd -T` + existing config review (avoid account guessing) | Server policy blocks direct root SSH |
| Host firewall | UFW rule inspection | Defined host filtering policy |
| Cloud firewall | Provider control panel inspection | Defined upstream filtering policy |
| Fail2ban | Jail status + log evidence | Tool active; actual detected events only if logged |
| Lynis | Compare baseline/final audit | Configuration score and recommendation differences |

Optional: in a **local-only VM test**, configure a password-enabled disposable SSH instance with Fail2ban and generate a few intentional incorrect logins to observe ban behavior. Keep those results labeled as a *separate VM test*, not evidence of an attack against the public Droplet.

## 4. Record findings
- [ ] Complete `03_Evidence_Templates/Baseline_vs_Final.md`.
- [ ] Complete `03_Evidence_Templates/Test_Results.md`.
- [ ] Identify **at least two limitations**, such as: only one server, short observation window, no real penetration testing, no guarantee against software vulnerabilities.
- [ ] Start the results section of your paper; do not invent numerical changes.
