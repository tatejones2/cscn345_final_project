# 06 — Evidence, Research Notes, and Test Log

**Do not fabricate values or tests.** Attach screenshots separately in a local `evidence/` directory; redact sensitive material.

## Daily experiment log template
### Date/time:
- Objective:
- Change made (code/config):
- Why:
- Command or test performed:
- Expected result:
- Actual result:
- Screenshot/file name:
- Issue encountered and fix:
- Remaining question:

## Verification matrix (fill after testing)
| ID | Feature | Ground-truth source | Dashboard value | Timestamp/window | Match? | Evidence |
|---|---|---|---|---|---|---|
| T01 | Uptime | `uptime`/`/proc/uptime` | TODO | TODO | TODO | TODO |
| T02 | RAM/disk | `free -h`, `df -h /` | TODO | TODO | TODO | TODO |
| T03 | SSH failures | bounded journal/auth log query | TODO | TODO | TODO | TODO |
| T04 | Fail2ban | `fail2ban-client status <jail>` | TODO | TODO | TODO | TODO |
| T05 | UFW status | `sudo ufw status` | TODO | TODO | TODO | TODO |
| T06 | Listening ports | `ss -tuln` | TODO | TODO | TODO | TODO |
| T07 | Docker containers | `docker ps --format ...` | TODO | TODO | TODO | TODO |
| T08 | Lynis snapshot | dated source report | TODO | TODO | TODO | TODO |
| T09 | Event timeline | bounded sanitized source events | TODO | TODO | TODO | TODO |
| T10 | Missing source | fixture with unavailable data | Should say unavailable | TODO | TODO | TODO |
| T11 | Private access | backend listener/off-host check | loopback only | TODO | TODO | TODO |

## Compare visibility before and after
**Before dashboard:** Which native commands were required? How many distinct command views? What made inspection cumbersome? **After:** Which views are centralized? Was information accurate? What still required a terminal? Do not invent a speed improvement without measuring it.

## Screenshots to capture
- [ ] Terminal source command with date (redacted).
- [ ] Matching dashboard card and refresh time.
- [ ] SSH and Fail2ban view.
- [ ] Firewall/ports and server-health view.
- [ ] Timeline, Docker, latest Lynis snapshot.
- [ ] Backend listening only on loopback.
- [ ] Unavailable/error case (safe fixture).
- [ ] Git commit history/source code structure.
