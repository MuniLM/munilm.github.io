---
log_id: 2026-11-24_02
date: 2026-11-24
type: WALKTHROUGH
status: executed
scope: [frontend]
source_artifact: munilm_launch_walkthrough
conversation_id: 1cef3ce2-32a9-4654-a87d-495da4745fa1
---

# MuniLM Launch — Encrypted Investor Readiness & Roadshow Task Manager (`/launch/`)

## 1. Summary of Compiled Release

1. **Root Portal `MUNILM LAUNCH` Section (`/index.html` -> `./launch/`):**
   - Added the dedicated **`MUNILM LAUNCH`** section above `PROTOTYPE MODULES` on `/`, linking to `./launch/` while preserving `/acfr-extraction/`, `/benchmark/`, and all 5 canonical city workstation slugs.
2. **Client-Side Encrypted `/launch/` Workstation (`munilm_launch_v1`):**
   - Compiled `/launch/index.html` via `<XBRL_REPO_ROOT>/prototype/hitl_showcase/rebuild_all_live_showcases.py` using `PBKDF2-HMAC-SHA256` (`210,000` iter) + `AES-256-GCM` (`0` plaintext roadshow tasks, founder names, or metrics in public HTML/JS source), `<meta name="referrer" content="no-referrer" />`, `#key=...` invite fragment auto-unlock + `history.replaceState` scrubbing, and `Lock Vault` session clearing.
   - Included collapsible 5-phase & parent-task Gantt rollups, resizable task column, inline-editable tasks & subtasks (`%` progress, dates, assignees, titles), draggable & edge-resizable Gantt bars (`3W` / `6W` / `Full` horizons), sortable Table & Kanban views, AES-GCM encrypted `localStorage` persistence, and zero-dependency OpenXML `.xlsx` / `.json` export & import.

## 2. Pre-Deploy Security & WebCrypto Gate

- Passed headless Node.js W3C WebCrypto decryption, wrong-key rejection, and zero-plaintext-leak verification across `/`, `/acfr-extraction/`, `/benchmark/`, `/launch/`, and city workstation bundles (`[PORTAL_BENCHMARK_AND_LAUNCH_WEBCRYPTO_OK]`).
