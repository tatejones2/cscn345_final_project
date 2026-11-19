# 08 — APA Research Paper Outline (5–7 Pages)

**Assignment classification:** Linux-focused **programming** project. The handout says **approximately 5–7 pages with source code in the appendix**. Include overview, methodology, execution, results, successes/failures, lessons learned and recommendations. Confirm with the professor whether title, references and appendices count toward the 5–7 pages.

## Suggested title
**Development and Evaluation of a Python-Based Linux Server Security Monitoring Tool**

## Draft structure (approximately 6 pages of narrative)
| Section | Target narrative length | What to include |
|---|---:|---|
| Introduction and question | 0.5 page | Why monitoring multiple Linux security sources matters; research question |
| Background/context | 0.75 page | SSH, Fail2ban, UFW, audit logs, Linux monitoring; historical hardening distinguished |
| Design and methods | 1.25 pages | Ubuntu environment, Python/Rich architecture, data sources, schema, safe permission strategy, tests |
| Implementation | 1–1.25 pages | Modules written, parsing, terminal UI, errors, demo vs live data |
| Results and evaluation | 1–1.25 pages | Comparison table against native commands, successful and unavailable features, accuracy and sample timing |
| Discussion, limitations, conclusion | 1–1.25 pages | Privacy/privilege tradeoffs, observed benefits, failures, next steps |
| **Narrative total** | **~5.75–6.25 pages** | Adjust layout to 5–7 pages |

## Appendix and references
- **Appendix A:** Source code (assignment expressly requests source code in appendix for programming-project option). Also submit the full source files separately if Canvas supports attachments; ask instructor about lengthy source appendices if needed.
- **Appendix B (optional):** Redacted screenshots / test matrix if permitted.
- **References:** APA citations for official Python, Ubuntu, Fail2ban, Rich and other sources **you actually used**. Avoid fabricated references.

## Writing tips
- Write in past tense when describing **completed** work and label planned or unfinished features honestly.
- Distinguish measured values from demo/sample values.
- Each result should link to evidence gathered in `06_Evidence_and_Test_Log.md`.
- Do not call the tool an intrusion prevention system; it primarily **monitors and summarizes** existing security controls.
- Describe historical root-login hardening only as background; the original contribution is Python code.

## Results table template
| Feature | Data source | Expected | Observed | Test outcome / limitation |
|---|---|---|---|---|
| SSH failed logins | logs | Count in stated interval | TODO | TODO |
| Fail2ban | jail status | Current / total bans | TODO | TODO |
| UFW | ufw status | Status and rules | TODO | TODO |
| Server health | psutil / system | Uptime, memory, disk | TODO | TODO |

## Before submitting
Check APA formatting and the instructor's exact page-count interpretation. Verify that code in the appendix matches the code actually submitted and demonstrated.
