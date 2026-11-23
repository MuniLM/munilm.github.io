# AGENTS.md — AI Agent Entrypoint (`MuniLM/munilm.github.io`)

> **Canonical Agent Instructions:** Read **[`AGENT.md`](AGENT.md)** in full before modifying files, compiling static bundles, or pushing commits to `MuniLM/munilm.github.io`.

## Quick Non-Negotiable Rules
1. **Public GitHub Pages Repo:** Every file in this repository is publicly served at `https://munilm.github.io/`. Never commit vault keys, `.env` secrets, `--local-unencrypted` builds, raw ACFR workbooks/PDFs, or personal workstation paths.
2. **Compile From Upstream (`MuniLM/xbrl`):** Never hand-edit generated `index.html` bundles. Edit `prototype/hitl_showcase/` in `MuniLM/xbrl`, recompile via `rebuild_all_live_showcases.py`, and pass `verify_portal_and_brief.cjs` before pushing.
3. **Preserve Published Slugs & Security Headers:** Keep `/`, `/acfr-extraction/`, `/benchmark/`, and all 5 top-level city slugs intact with `<meta name="referrer" content="no-referrer" />` and `#portalVaultCanary` verification.

See **[`AGENT.md`](AGENT.md)** and **[`README.md`](README.md)** for full architecture, cryptographic specifications, and verification commands.
