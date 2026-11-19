# 03 — Remaining Schedule: November 19–24, 2026

**Deadline: Tuesday, November 24, 2026; verify exact Canvas time.** This is a compressed plan. Begin the paper on the first day; freeze features early. Hours are rough planning estimates, not guarantees.

## Thu Nov 19 — Project skeleton + first output (2–4 h)
- [ ] Read scope and safety docs; inventory available Linux tools.
- [ ] Make Python project, venv, requirements, sample fixtures, gitignore.
- [ ] Implement common collector result schema and **system health**.
- [ ] Display first Rich table/panel; record commands and results.
- [ ] Draft paper intro + method notes.

## Fri Nov 20 — Security collectors (3–5 h)
- [ ] Add bounded SSH login counts with named window and permissions handling.
- [ ] Add Fail2ban per-jail totals/current bans (labeled accurately).
- [ ] Add UFW status and `ss` listener list.
- [ ] Verify 2–3 values against native commands; start tests.

## Sat Nov 21 — Remaining feature areas (3–5 h)
- [ ] Add event timeline from bounded sanitized entries.
- [ ] Add Docker status via safe minimal snapshot/import where required.
- [ ] Load latest dated Lynis report (not continuous scanning).
- [ ] Test missing/unavailable sources and timeout handling.
- [ ] **Feature freeze:** no architecture rework after today.

## Sun Nov 22 — Terminal polish + verification (3–5 h)
- [ ] Improve Rich layout, refresh behavior and demo mode labels.
- [ ] Run test suite and comparison matrix; save redacted screenshots.
- [ ] Test from Ubuntu shell; confirm no new public port is open.
- [ ] Draft results, discussion and limitations.

## Mon Nov 23 — Paper + presentation (3–5 h)
- [ ] Complete **5–7-page** APA report and source-code appendix.
- [ ] Complete 10–15-minute presentation and practice demo.
- [ ] If optional GUI is unfinished, omit it; working terminal tool is the deliverable.

## Tue Nov 24 — Submission (1–3 h buffer)
- [ ] Re-run from README and verify command output.
- [ ] Check code attachment/appendix, privacy, references, APA and page count.
- [ ] Export paper/slides and submit before Canvas cutoff.

## Triage if behind
1. Make system health + SSH + Fail2ban + UFW/ports **work and test them**.
2. Keep timeline/Docker/Lynis as optional cleanly unavailable or dated imported views.
3. Finish 5–7 pages and code appendix before working on optional GUI or keyboard navigation.
