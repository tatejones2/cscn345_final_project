# 14 — Optional GUI Extension (AFTER the Main Project)

The **terminal application is the graded Linux programming project**. A GUI is optional and should **not** consume time needed for the working terminal tool, tests, source-code appendix, 5–7-page APA paper or presentation.

## Only start if
- [ ] Terminal monitor runs on Ubuntu and covers core metrics accurately.
- [ ] Missing permissions and stale data are handled correctly.
- [ ] Report is drafted and sufficient evidence has been saved.
- [ ] Presentation demo is ready.

## Design principle
Reuse your collector modules and result schema; do not rewrite business logic. A tiny Flask/FastAPI app can render **sanitized saved JSON snapshots** (not privileged shell execution) through a separate read-only interface. A static HTML snapshot is an even simpler option.

## Access
- Keep any local web listener on `127.0.0.1` and access through an authenticated SSH tunnel; no public reverse-proxy route.
- Never give HTTP processes raw Docker socket or broad sudo permissions.
- No command-execution, ban/unban, port management or other state-changing controls.
- Clearly label demo and historical data.

## What to demonstrate if built
A single page with the same seven metric sections, collection time, status and source. In the report, label it an *optional extension*, not the primary Linux-focused programming contribution.
