---
log_id: 2026-11-24_01
date: 2026-11-24
type: PLAN
status: approved
scope: [frontend]
source_artifact: munilm_launch_plan
conversation_id: 1cef3ce2-32a9-4654-a87d-495da4745fa1
---

# MuniLM Launch — Investor Readiness & Roadshow Task Manager (`/launch/`)

## 1. Approved Scope & Security Architecture

1. **Root Portal Section (`/` -> `./launch/`):**
   - Render a dedicated **`MUNILM LAUNCH`** section above `PROTOTYPE MODULES` on `/` linking to `./launch/`, while keeping all existing routes (`/acfr-extraction/`, `/benchmark/`, and the 5 canonical city slugs) intact.
2. **Client-Side Cryptographic Vault (`PBKDF2-SHA256` + `AES-256-GCM`):**
   - Compile `/launch/index.html` from `<XBRL_REPO_ROOT>/prototype/hitl_showcase/launch_task_manager.py` via `rebuild_all_live_showcases.py` with `<meta name="referrer" content="no-referrer" />`, `#key=...` invite fragment verification + URL scrubbing, `Lock Vault` support, and zero-plaintext `#encryptedBundlePayload` envelopes.
   - Encrypt local browser customizations at rest in `localStorage` under the active vault key.
3. **Interactive Roadshow Gantt, Table, Kanban & Spreadsheet Sync:**
   - Combine collapsible Phase & parent-task rows, resizable task column, inline-editable tasks & subtasks, draggable & edge-resizable Gantt bars (`3W` / `6W` / `Full` zoom), sortable Table & Kanban views, deterministic health rollups (`On Track` / `At Risk` / `Off Track`), assignee workload filters, and zero-dependency `.xlsx` / `.json` snapshot export & import.
