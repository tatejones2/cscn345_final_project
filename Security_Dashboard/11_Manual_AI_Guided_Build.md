# 11 — Manual Build with AI Guidance (PRIMARY PATH)

You are the developer. AI is a tutor, reviewer, and debugger—not an autonomous agent changing your server. Ask for **one checkpoint at a time**; type/edit and run the code yourself, then paste sanitized errors for help.

## Copy/paste tutor prompt to start
> I am building the Security_Dashboard CSCN 345 project **manually**. Use `README.md`, `01_Project_Scope.md`, `04_Dashboard_Technical_Plan.md`, `05_Security_and_Privacy_Guardrails.md`, `11_Manual_AI_Guided_Build.md`, and `13_Metric_Definitions_and_Verification.md` as requirements. Act as a patient hands-on coding tutor. Give me **one checkpoint at a time** with exact files to create, short code samples, commands, and a way to verify success. Explain what each part does, let me implement it, and wait for my result before advancing. Do not assume my server configuration or run actions for me. Never request secrets or suggest exposing privileged server data to the internet. Begin with Checkpoint 1.

## Development stack default
- Python 3.11+ with `venv`, FastAPI, `uvicorn`, pytest.
- Plain HTML/CSS/JavaScript for the interface; use React/Vite only if you decide the additional setup is worth it.
- Fixtures: small synthetic JSON test files containing no real IPs.
- Local API binding: `127.0.0.1:8765`.

## Checkpoint 1 — Create repo and app structure
Make `security-dashboard/backend`, `frontend`, `fixtures`, `tests`, `docs`. Initialize Git; create `.gitignore` covering `.env`, `.venv`, `__pycache__`, raw logs, credentials, and snapshots. Create a `README.md` in the code repo with dependencies, setup, non-root running method and data limitations. **Verify:** clean Git status and no secrets tracked.

## Checkpoint 2 — Make API respond
Create a FastAPI app with a fixed `/api/health` returning JSON with `collected_at`, `source`, `status`, `data`. Start `uvicorn` bound to `127.0.0.1`. **Verify:** `curl http://127.0.0.1:8765/api/health` works locally; no public bind.

## Checkpoint 3 — Fixture-driven frontend
Make a simple page with title, status, update timestamp, and cards. Fetch fixture-backed endpoints; render unavailable as unavailable. Use `textContent` (not `innerHTML`) for untrusted log-derived strings. **Verify:** cards load from test fixtures; error fixture doesn't show 0.

## Checkpoint 4 — System metrics
Add read-only uptime, load, memory and disk metrics. Track `collected_at`. **Verify:** compare values with `uptime`, `free -h`, `df -h /` within a stated time difference. Document any unit conversions.

## Checkpoint 5 — SSH/Fail2ban
Develop **parsers from sanitized sample outputs** first. Clearly label last-24h SSH failures and the difference between currently and cumulatively banned. Connect to a local pre-generated snapshot; don't give API sudo. **Verify:** compare a sampled report with a corresponding source command at nearly same time.

## Checkpoint 6 — Firewall and listening ports
Display summarized UFW status and `ss -tuln` output. Be careful about local-only vs externally reachable listeners; firewall and cloud firewall can further restrict access. **Verify:** each listed socket matches an actual listener at collection time.

## Checkpoint 7 — Event timeline
Implement bounded (e.g. max 50) recent events with types, source, timestamp, summary and redaction. Use synthetic fixture first. **Verify:** sorted newest-first and no raw sensitive values/HTML injection.

## Checkpoint 8 — Docker + Lynis
Docker: display read-only snapshot listing name/state/health; **no Docker socket in API**. Lynis: import manually reviewed report summary with original audit date. **Verify:** Docker snapshot matches sampled `docker ps`; Lynis displays "last audited" instead of "live".

## Checkpoint 9 — Private live deployment
Do not modify existing app routes. Run API non-root and loopback-only; if necessary use a restricted collector writing sanitized snapshots. Access with SSH `-L` tunnel. **Verify:** local dashboard opens through tunnel, direct public access fails, existing websites still run normally.

## Checkpoint 10 — Tests and research evidence
Run functional/unit tests, unknown/unavailable state test, source comparisons, privacy test, screenshots, and fill `06_Evidence_and_Test_Log.md`. Freeze scope; write report from measured results.

## Questions to ask the AI at every checkpoint
1. What am I building and why?
2. Which file do I create/edit?
3. What does this command or code block do?
4. What success output should I see?
5. What should I record for the methodology/results section?

## When blocked
Tell the tutor: "I am on Checkpoint X. Here is the **redacted** command/code/error. Explain the cause and give me the smallest safe fix; do not move ahead." Do not copy production secrets, private SSH keys or entire live logs.
