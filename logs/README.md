# MuniLM Showcase Portal Engineering & Deployment Logs (`logs/`)

Institutional engineering memory for `MuniLM/munilm.github.io` (`https://munilm.github.io/`)—tracking substantive `RESEARCH`, `AUDIT`, `PLAN`, `ADR`, and `WALKTHROUGH` logs in Git.

> **Public Repository Hygiene:** `MuniLM/munilm.github.io` is a public GitHub Pages repository. Never include vault passphrases, invite keys, OAuth/API credentials, local workstation usernames/paths, or gated unencrypted benchmark data in `logs/*.md`.

## 1. File Naming Convention
```text
YYYY-MM-DD_<seq>_<TYPE>_<scope>_<topic-slug>.md
```
- `YYYY-MM-DD`: ISO-8601 date.
- `<seq>`: Two-digit daily sequence (`01`, `02`, ...) ordered chronologically within that date.
- `<TYPE>`: Controlled uppercase enum: `RESEARCH` | `AUDIT` | `PLAN` | `ADR` | `WALKTHROUGH`.
- `<scope>`: Lowercase target slice (`all`, `frontend`, `security`, `portal`, `benchmark`).
- `<topic-slug>`: Concise 3–6 word `kebab-case` summary (no spaces).

## 2. Mandatory YAML Frontmatter Header
```yaml
---
log_id: YYYY-MM-DD_01
date: YYYY-MM-DD
type: RESEARCH | AUDIT | PLAN | ADR | WALKTHROUGH
status: draft | pending-approval | approved | executed | superseded
scope: [frontend]
source_artifact: <original_artifact_filename_if_exported>
conversation_id: <agent_conversation_uuid_if_applicable>
---
```

## 3. Chronological Log Index

| Date & Seq | Type | Scope | File | Summary |
| :--- | :---: | :---: | :--- | :--- |
| `2026-11-22_01` | `WALKTHROUGH` | `frontend` | [`2026-11-22_01_WALKTHROUGH_frontend_munilm-pages-portal-and-documentation-bootstrap.md`](2026-11-22_01_WALKTHROUGH_frontend_munilm-pages-portal-and-documentation-bootstrap.md) | Documented two-level MuniLM Prototype Workspace (`/`, `/acfr-extraction/`, `/benchmark/`, and 5 encrypted city workstations @ `0504766`) and added `README.md`, `AGENT.md`, `AGENTS.md`, `.gitignore`, and `logs/README.md`. |
| `2026-11-24_01` | `PLAN` | `frontend` | [`2026-11-24_01_PLAN_frontend_munilm-launch-investor-roadshow-task-manager.md`](2026-11-24_01_PLAN_frontend_munilm-launch-investor-roadshow-task-manager.md) | Approved plan adding vault-encrypted `MuniLM Launch` (`/launch/`) Investor Readiness & Roadshow Task Manager (Gantt + work-day math + Table/Kanban + `.xlsx`/`.json` sync) above Prototype Modules on `/`. |
| `2026-11-24_02` | `WALKTHROUGH` | `frontend` | [`2026-11-24_02_WALKTHROUGH_frontend_munilm-launch-investor-roadshow-task-manager.md`](2026-11-24_02_WALKTHROUGH_frontend_munilm-launch-investor-roadshow-task-manager.md) | Compiled vault-encrypted `/launch/` (`munilm_launch_v1`, `21` tasks across 5 phases) and root `MUNILM LAUNCH` card, passing W3C WebCrypto decryption, wrong-key rejection, and zero-plaintext-leak checks. |
