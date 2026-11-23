---
log_id: 2026-11-22_01
date: 2026-11-22
type: WALKTHROUGH
status: executed
scope: [frontend]
source_artifact: README.md
conversation_id: 54cf6797-61c8-4bde-b990-329e30600557
---

# MuniLM Prototype Workspace & Repository Documentation Bootstrap

## 1. Summary of Deployed Portal Architecture (`350cfe0` -> `68c01e6` -> `0504766`)

1. **Organization Root Domain (`https://munilm.github.io/`):**
   - Migrated showcase repository to `MuniLM/munilm.github.io` with HTTPS enforced (`https_enforced: true`) and `.nojekyll` static serving.
   - Deployed the two-level **MuniLM Prototype Workspace** at `/` (`ACFR Extraction` [`Live`], `Official Statement XBRL` [`Offline`], `Internal Data Catalog` [`Offline`], `External Data Catalog` [`Offline`]) with the **Municipal ACFR-to-XBRL Workstations** hub at `/acfr-extraction/`.
   - Preserved top-level routes for all 5 encrypted city workstations (`/milwaukee-fy2025/`, `/boston-fy2025/`, `/tampa-fy2025/`, `/denver-water-fy2024/`, `/alpha-park-fy2025/`) and the encrypted executive & technical benchmark report (`/benchmark/`).
2. **Client-Side Cryptographic Vault Hardening:**
   - Enforced `PBKDF2-HMAC-SHA256` (`210,000` iter) + `AES-256-GCM` encryption across all city bundles and `/benchmark/`, verified via headless Node.js W3C WebCrypto round-trip and wrong-key rejection checks.
   - Added 32-byte AES-GCM `#portalVaultCanary` verification on `/` and `/acfr-extraction/` for `#key=...` invite links with immediate `history.replaceState` URL scrubbing, `<meta name="referrer" content="no-referrer" />`, and 1-click `Lock Vault`.
3. **Repository Documentation & Safety Guardrails:**
   - Added [`README.md`](../README.md), [`AGENT.md`](../AGENT.md), [`AGENTS.md`](../AGENTS.md), [`.gitignore`](../.gitignore), and [`logs/README.md`](README.md) establishing public-origin secret/PII hygiene, upstream `MuniLM/xbrl` compilation rules, and mandatory pre-push WebCrypto verification gates.
