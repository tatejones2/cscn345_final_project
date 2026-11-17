# Day 2 — Prevent unauthorized access (SSH and firewalls)

**Goal:** Require SSH keys, block direct root SSH logins, and restrict inbound network traffic. **Keep your existing working SSH session open until the new session is confirmed.**

## 1. Confirm a sudo user has working SSH key login
From a **second Mac terminal**:
```bash
ssh USER@SERVER_IP
```
On the Droplet verify:
```bash
whoami
sudo -v
```
**Do not proceed** unless this is a **non-root** account with sudo rights, the key works, and you can open a brand new login session. Check the DigitalOcean recovery console instructions in advance; it is not a substitute for verifying your SSH setup.

## 2. Capture effective SSH settings
```bash
sudo sshd -T | grep -Ei '^(permitrootlogin|passwordauthentication|pubkeyauthentication|kbdinteractiveauthentication) '
sudo grep -RniE '^(PasswordAuthentication|PermitRootLogin|PubkeyAuthentication|KbdInteractiveAuthentication)' /etc/ssh/sshd_config /etc/ssh/sshd_config.d/
```
Ubuntu reads drop-in configuration under `/etc/ssh/sshd_config.d/`. **First matching value may win**, so examine existing files and effective results rather than assuming a new filename overrides them.

## 3. Edit SSH config carefully
Use `sudo nano` to edit the applicable earlier drop-in (or existing active setting) and implement **effective** values:
```text
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
KbdInteractiveAuthentication no
```
A separate custom file such as `/etc/ssh/sshd_config.d/00-project-hardening.conf` is reasonable **only if** it actually takes precedence over your existing drop-ins; check with `sshd -T`. Do not edit cloud-init-managed files blindly.

Validate and reload:
```bash
sudo sshd -t
sudo systemctl reload ssh
sudo sshd -T | grep -Ei '^(permitrootlogin|passwordauthentication|pubkeyauthentication|kbdinteractiveauthentication) '
```
Then **open yet another new terminal** and confirm normal key-based login still works. If not, undo the change from the still-open original session.

**Research test:** On your **own Mac**, try a login forcing password authentication *without your SSH key*:
```bash
ssh -o PubkeyAuthentication=no -o PreferredAuthentications=password USER@SERVER_IP
```
Expected: the server refuses password authentication. Do not repeat attempts or conduct password guessing. Capture the single result and check the effective SSH config.

## 4. UFW on the Droplet
First allow your SSH port and verify the rule before enabling UFW:
```bash
sudo ufw allow 22/tcp
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw enable
sudo ufw status verbose
```
If you deliberately use a **different** SSH port, replace `22/tcp` with your verified current port **before** enabling the firewall. A source-restricted rule is preferable where your IP is stable; see `sudo ufw help` and Ubuntu's UFW guide.

In DigitalOcean, ensure the **Cloud Firewall** allows the same intended SSH traffic. A cloud firewall rule that blocks SSH takes precedence before packets reach UFW. Avoid opening HTTP/HTTPS or unused ports simply for demonstration.

## 5. Record evidence
- [ ] Non-root key-based SSH succeeds from a new terminal.
- [ ] SSH password-only attempt is refused.
- [ ] `sshd -T` confirms intended effective settings.
- [ ] `sudo ufw status verbose` shows intended rule(s).
- [ ] DigitalOcean Cloud Firewall screenshot documents external policy.
- [ ] Fill Day 2 research log and paper methodology notes.

**Scope warning:** Do not do a public port scan or brute-force experiment just to fill your paper. A review of `ss -tulpen` and firewall configurations is sufficient for a focused project; optional connection tests must be limited to your own infrastructure under provider rules.
