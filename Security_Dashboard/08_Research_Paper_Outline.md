# 08 — APA Research Paper Guide (10–12 Pages)

**Assignment-grounded:** Describe the project, research method, what you implemented/tested, results (successes/failures), lessons learned, and recommendations. APA compliance is required. Submit applicable source code. Confirm whether page target includes title/references with the instructor; do not assume.

## Working title
*Design and Evaluation of a Read-Only Security Dashboard for a Hardened Ubuntu Server*

## Proposed structure (approximate body-length allocations)
1. **Introduction (1 page):** Why visibility matters; research question, purpose, scope.
2. **Background and related work (1.5–2 pages):** Linux hardening vs monitoring; SSH, Fail2ban, UFW, logs, Lynis, Docker and private administrative interfaces. Cite real credible sources.
3. **Existing environment and prior hardening (1 page):** Historical server context; explicitly separate pre-existing work from new project implementation.
4. **Method and design (2 pages):** architecture, tool choices, read-only privilege model, data model, sampling frequency, validation procedure and ethical constraints.
5. **Implementation (1.5–2 pages):** how collectors/API/UI were developed; troubleshooting; deployed/unused features.
6. **Testing and results (2 pages):** completed tests from `06_Evidence_and_Test_Log.md`, tables of source-versus-dashboard values, failed cases, private access validation.
7. **Discussion/limitations (1 page):** log ambiguities, stale data, privileges, coverage gaps, no guarantee of attack attribution; tradeoffs.
8. **Conclusion and future work (0.5–1 page):** supported findings and next steps.
9. **References** and (if useful) **Appendix** with code excerpts/screenshots, in accordance with instructor requirements.

## Suggested research hypothesis (testable, not a promised result)
A read-only dashboard can reduce the number of separate command-line views needed to review selected security indicators while maintaining agreement with their underlying sources.

## Evidence-driven writing rules
- Write **what you observed**, not what the software is supposed to do.
- Report a metric's time window and last collection time.
- Distinguish a firewall **rule/configuration** from proof that all attacks are stopped.
- Distinguish Fail2ban **Found** vs **Ban** and **currently** vs **total** banned.
- Keep the old Lynis index separate from a newly produced report; never imply historical values are live.
- Attribute borrowed explanations and security standards; do not invent citations.

## Draft-as-you-go prompts for an AI tutor
- "Using my notes below, ask for missing methodology facts; do not create procedures I didn't perform."
- "Help me turn this test log into a neutral results paragraph without changing the numbers."
- "Review my APA section structure and flag unsupported claims; don't invent sources."

## Sources to investigate and verify
- Ubuntu Server documentation on OpenSSH, firewall, security updates, logging.
- Fail2ban official documentation and manual pages.
- Lynis official documentation and report formats.
- Docker docs on daemon socket security and running containers.
- NIST guidance on security logging and monitoring, as background (only if substantively used).
