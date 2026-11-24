# AGENT.md — Operational Rules & Security Guardrails for AI Agents (`MuniLM/munilm.github.io`)

All autonomous coding, documentation, QA, and deployment agents operating on `MuniLM/munilm.github.io` MUST obey the following invariants without exception.

---

## 1. Repository Role & Source-of-Truth Topology

1. **Compiled Static Artifact Repo (Not Primary Source):**
   - `MuniLM/munilm.github.io` is the **public GitHub Pages deployment target** serving `https://munilm.github.io/`.
   - **Never hand-edit** compiled HTML, inline JavaScript, or ciphertext envelopes inside `index.html`, `acfr-extraction/index.html`, `benchmark/index.html`, or `<city-slug>/index.html`. Any manual edit will be overwritten on the next compile and risks breaking AES-GCM integrity or introducing plaintext leaks.
2. **Upstream Compiler Source of Truth (`MuniLM/xbrl`):**
   - All template, UI, and payload changes must be made in the private upstream `MuniLM/xbrl` repository under `prototype/hitl_showcase/`:
     - `build_hitl_showcase.py` — Root `/`, `/acfr-extraction/`, `/benchmark/`, and city workstation compiler + `AES-256-GCM` encryptor.
     - `benchmark_report_builder.py` — Read-only scorecard compiler for `/benchmark/`.
     - `rebuild_all_live_showcases.py` — Batch rebuilder across all 5 canonical city slugs + `/benchmark/` + `/` + `/acfr-extraction/`.
     - `templates/hitl_ui_template.html` & `templates/hitl_app.js` — Interactive split-screen PDF $\leftrightarrow$ Inline XBRL workstation UI.
     - `verify_portal_and_brief.cjs` — Node.js W3C WebCrypto decryption, canary, and zero-plaintext-leak test runner.

---

## 2. Public-Origin Security & Zero-Plaintext Invariants (CRITICAL)

Because `MuniLM/munilm.github.io` has **`PUBLIC`** GitHub visibility and `.nojekyll` enabled (meaning every committed file is publicly downloadable over HTTPS):

1. **Zero Secrets or Invite Keys:**
   - **NEVER** commit, log, echo to terminal stdout, or paste into commit messages/PRs/`logs/*.md` the `MUNILM_TEAM_VAULT_KEY`, any `#key=...` invite URL containing a real passphrase, OAuth secrets, API keys, or `.env` files. Always use `<YOUR_INVITE_KEY>` or `<KEY_FILE_PATH>` placeholders in documentation.
2. **Zero Unencrypted Builds (`--local-unencrypted` Prohibition):**
   - **NEVER** run `build_hitl_showcase.py --local-unencrypted` targeting this repository, and **NEVER** copy raw `showcase_bundle.json`, `.xlsx`, `.ixbrl.html`, `.xml`, `.mapping_trace.json`, or source ACFR `.pdf` files into this repository.
   - All protected payloads must reside solely inside `<script id="encryptedBundlePayload" type="application/json">` encrypted via `PBKDF2-HMAC-SHA256` (`210,000` iterations) + `AES-256-GCM`.
3. **Zero Local Workstation PII:**
   - **NEVER** commit developer-specific local filesystem paths (e.g., `C:\Users\<username>\...` or `/Users/<username>/...`), internal hostnames, or private scratch directory paths into `README.md`, `AGENT.md`, `logs/*.md`, or HTML comments. Use portable `<XBRL_REPO_ROOT>` and `<PAGES_REPO_ROOT>` placeholders.
4. **Mandatory Browser Security Headers & Controls:**
   - Every HTML page in this repository MUST include `<meta name="referrer" content="no-referrer" />` inside `<head>`.
   - Root `/index.html` and `/acfr-extraction/index.html` MUST verify `#key=...` URL fragments against `#portalVaultCanary` *before* writing `munilm_team_vault_key_v1` to `localStorage`, and MUST scrub `#key=...` immediately via `history.replaceState`.
   - Every topbar MUST retain a working `Lock Vault` action that clears `munilm_team_vault_key_v1` from `localStorage`.

---

## 3. URL & Route Stability Contract

External partners, researchers, and investors hold deep links into this domain. Agents MUST preserve backward compatibility across all published routes:

- `/` — Top-level **MuniLM Prototype Workspace** featuring `MuniLM Launch` (`./launch/`) plus the 4 prototype cards (`ACFR Extraction` [`Live`], `Official Statement XBRL` [`Offline`], `Internal Data Catalog` [`Offline`], `External Data Catalog` [`Offline`]).
- `/launch/` — Vault-encrypted **MuniLM Launch (Investor Readiness & Roadshow Task Manager)**.
- `/acfr-extraction/` — **Municipal ACFR-to-XBRL Workstations** sub-page.
- `/benchmark/` — Vault-encrypted **Executive & Technical Benchmark Report**.
- `/milwaukee-fy2025/`, `/boston-fy2025/`, `/tampa-fy2025/`, `/denver-water-fy2024/`, `/alpha-park-fy2025/` — Canonical city workstation slugs (do not rename or nest under `/acfr-extraction/` without explicit redirect pages).

---

## 4. Mandatory Pre-Push Verification Checklist

Before running `git commit` or `git push` in `MuniLM/munilm.github.io`, an agent MUST execute all four checks:

1. **Upstream Unit & Scorecard Integrity Suite (in `<XBRL_REPO_ROOT>`):**
   ```powershell
   python -m pytest <XBRL_REPO_ROOT>/tests -q
   ```
2. **Encrypted Full-Site Rebuild:**
   ```powershell
   python <XBRL_REPO_ROOT>/prototype/hitl_showcase/rebuild_all_live_showcases.py `
     --site-root <PAGES_REPO_ROOT> `
     --vault-key-file <KEY_FILE_PATH>
   ```
3. **Headless W3C WebCrypto & Zero-Plaintext-Leak Gate:**
   ```powershell
   $env:MUNILM_TEAM_VAULT_KEY = (Get-Content -Raw <KEY_FILE_PATH>).Trim()
   node <XBRL_REPO_ROOT>/prototype/hitl_showcase/verify_portal_and_brief.cjs <PAGES_REPO_ROOT>
   Remove-Item Env:\MUNILM_TEAM_VAULT_KEY
   ```
4. **Public Diff & Pages Deployment Verification:**
   - Inspect `git status --short` and scan staged Markdown/JSON files to confirm zero local user paths, zero `unencrypted_brief` keys, and zero secrets.
   - After `git push origin main`, verify GitHub Pages reports `"status": "built"` and `"https_enforced": true`:
     ```powershell
     gh api repos/MuniLM/munilm.github.io/pages --jq "{status:.status, https:.https_enforced, url:.html_url}"
     ```

---

## 5. Multi-Agent Concurrency & Institutional Logs (`logs/`)

1. **Single-Writer Check:** Always run `git status -s` before compiling into `<PAGES_REPO_ROOT>`. If another agent has an active build or uncommitted state in progress, coordinate before overwriting compiled bundles.
2. **Institutional Logs (`logs/`):** Substantive architectural plans (`PLAN`), security audits (`AUDIT`), and major portal releases (`WALKTHROUGH`) tracked in this repo follow the `YYYY-MM-DD_<seq>_<TYPE>_<scope>_<topic-slug>.md` naming convention and YAML frontmatter index in [`logs/README.md`](logs/README.md)—subject to all public-repository secret and PII redaction rules in Section 2 above.
