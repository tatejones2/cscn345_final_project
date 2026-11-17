# Day 1 — Create a new Droplet and record the baseline

**Goal:** Set up a safe, new Ubuntu server, observe its original configuration, and run Lynis **before making hardening changes**.

## 1. DigitalOcean control panel
- [ ] Create a new **Basic Ubuntu LTS Droplet** (1 GB RAM should usually suffice for these lightweight tools; 2 GB gives more margin).
- [ ] Select a region, label it clearly (e.g., `cscn345-hardening-lab`), and add your existing **public** SSH key. Never upload your private key.
- [ ] Enable provider account MFA and review spending and backup/snapshot costs.
- [ ] Apply a DigitalOcean **Cloud Firewall** with incoming SSH (TCP 22) from your trusted IP when practical. Default deny all other unsolicited inbound traffic; permit required outbound traffic for updates. Cloud firewall rules are external to the VM.
- [ ] Write down the OS release, Droplet size, creation date, and anonymized public IP for your private notes.

**Safe baseline nuance:** The provider may provision security defaults (e.g., SSH keys or Cloud Firewall) from the outset. Do not weaken the server to produce a dramatic 'before' result. Record these as *existing baseline protections*.

## 2. Connect from your Mac Terminal
```bash
ssh USER@SERVER_IP
```
`USER` is the account created on the Droplet (often `root` initially). `SERVER_IP` is the new Droplet IP. Verify host key fingerprint through an independent provider channel if possible, especially on first connection.

If you first connect as root, create a separate sudo user and install your SSH public key for that user **before** disabling direct root SSH. Follow DigitalOcean's official initial setup guide for the exact account/key steps, since images and cloud-init differ.

## 3. Record system facts
Run on the **Droplet**:
```bash
cat /etc/os-release
uname -r
whoami
id
sudo ss -tulpen
sudo ufw status verbose
sudo systemctl status ssh --no-pager
sudo sshd -T | grep -Ei '^(port|permitrootlogin|passwordauthentication|pubkeyauthentication|kbdinteractiveauthentication) '
sudo systemctl status fail2ban --no-pager
```
Some commands may show an inactive/missing service; that's useful baseline evidence. `sshd -T` shows effective configuration for general context, though `Match` rules can change effective settings for particular users/addresses.

## 4. Install and run Lynis
```bash
sudo apt update
sudo apt install lynis
sudo lynis audit system
```
Record the **Hardening index**, warnings and high-priority suggestions. Keep a screenshot. Lynis installation slightly changes the baseline; disclose that the baseline was captured after installing the audit tool.

For repeatable local copies of the audit results on the Droplet:
```bash
sudo cp /var/log/lynis.log /root/lynis-before.log
sudo cp /var/log/lynis-report.dat /root/lynis-before-report.dat
sudo grep -E '^hardening_index=' /root/lynis-before-report.dat
```

## 5. Write the paper NOW
- [ ] Add 1 paragraph: what you built and why you chose this project.
- [ ] Add the operating system/version, instance size and starting security settings.
- [ ] Fill `03_Evidence_Templates/Baseline_vs_Final.md` baseline column.
- [ ] Fill `03_Evidence_Templates/Daily_Research_Log.md` Day 1 entry.

**Stop condition:** You can connect to the new Droplet, have your initial audit, and have documented the original settings. Don't harden until this evidence is saved.
