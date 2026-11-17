# Methods Worksheet — write details as they happen

## Environment
- New Droplet name (genericized for paper):
- Date provisioned:
- Ubuntu version (`cat /etc/os-release`):
- Kernel (`uname -r`):
- Droplet RAM/CPU:
- SSH port:
- SSH client OS:
- Cloud Firewall inbound/outbound rule summary:
- Lynis version (`lynis show version`, or `lynis --version` if supported):

## Initial state
- Initial user account / sudo policy:
- Effective SSH policy:
- UFW policy:
- Listening ports:
- Fail2ban state:
- Automatic updates state:
- Lynis index:
- Key warnings/suggestions:

## Controls applied (record exact date and command/config path)
| Control | What changed | Config/command | How verified | Date |
|---|---|---|---|---|
| Non-root SSH key | | | | |
| Root SSH login | | | | |
| Password SSH login | | | | |
| UFW | | | | |
| Cloud Firewall | | | | |
| Fail2ban | | | | |
| Updates | | | | |

## Final state
- Lynis index:
- SSH policy:
- UFW and cloud firewall status:
- Fail2ban jail status:
- Actual authentication/log observations:
- Deviations/failures/troubleshooting:

## Ethics and limitations
- Public Droplet used for legitimate administration and passive monitoring.
- Any active repeated-login trials performed in local isolated VM only (if performed at all).
- No conclusion about 'complete security' or absence of malicious activity.
