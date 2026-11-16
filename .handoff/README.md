# Handoff — WideLlama workspace after Lap 0 (2026-11-16)

*For the next session — human or agent. Read this first, then `.vibe/`, then act.*

## TL;DR

Everything is **committed, pushed, and merged** across all three repos. No open PRs, no uncommitted work, no unpushed branches. Both `main` and `development` are aligned everywhere. The container is being stopped specifically to fix a **stale scaffold** — do not use the template root files for bring-up.

## Repo state (verified 2026-11-16)

| Repo | `main` | `development` | Notes |
|---|---|---|---|
| `WideLlama/widellama-workspace` (fork, this repo) | `2c8582c` | = main | Agent guide, GHW, restart docs |
| `WideLlama/widellama` (reference lab + product pilot) | `6e39439` | `4953bde` | ADRs up to 0015; schemas moved to `widellama.com` namespace |
| `WideLlama/widellama-product-specs` (spec source of truth) | `ebdbb20` | `97a5ce6` | Tag **`v0.1.0`** — audited, CI-gated |

Tags: `v0.1.0` (specs) only. `v1.0.0-base` (widellama) branch deleted, tag retained.

## Known-stale template files (do not use for bring-up)

`start.sh`, `start-container.sh`, `download_qwen.sh`, `Dockerfile`, root `README.md` (Codespaces badge flow), `.github/workflows/ci.yml` and `publish.yml` (placeholder/broken for this fork), root `opencode.json` (template default model `code-inference/model.gguf` @ `http://api:8000/v1`, and a **stale instructions path**: `nacedigital-landing-page/...` — does not exist; expect a load warning), `models/` (empty). Enablement is the user's call on rebuild.

Stale by the user's own read (2026-11-16):
> "These don't apply here. We should create a `.handoff` and `.vibe` subfolders applying VibeLeading skills… I'm going to need to restart myself now and enable the workspace properly."

## What this session did (commits/PRs; all merged)

Root workspace: AGENTS.md rewritten → review fixes → GHW adopt + all-repos note → specs-driven fixes → filesystem artifact docs → restart runbook.
Widellama: AGENTS.md (ADR-0008 + Vibe Leading), workflow reconciled to GHW, AppleDouble guard, `v1.0.0-base` deleted (tag kept), schema `$id`s → `widellama.com`.
Specs repo: created (private), full normative set extracted implementation-agnostic from widellama drafts, specv1 AUDIT (integrity/reliability PASS after R-1/R-2), `verify` CI live, tagged `v0.1.0`.

## Open decisions for the next session

1. **Enablement model** (the reason for the restart): how does the proper bring-up work? Replace/retire the stale root files.
2. **`opencode.json`** — stale `instructions` entry and template default model; rework with enablement.
3. **Specs `v0.2.0`** — tag after ADR-0015 + schemas P0.2 land (main is ahead of the tag).
4. **Root fork Actions** — leave off (publish.yml would push to GHCR); or enable with explicit opt-in.
5. **`verify` as branch protection** in specs repo (recommended).
6. **`v1.0.0-base` tag** — keep (archaeology), or delete (repo decision; `1cf63de` recoverable).
7. **DNS/TLS/registrar, email for `widellama.com`**, GitHub repo homepages, trademark/brand assets — external work, Pilot owns.
8. **Second human** for Org Geometry (`.vibe/ORG-GEOMETRY.md`) — triggered by first design partner.
9. **Hardware/model story** — does the rebuilt product even use `model.gguf`? The template assumed it; the product spec does not.
10. **`verify` script's `.github/workflows/`** — specs CI is live; widellama gates on `pytest`; fork Actions off.

## Next-session verification checklist

```bash
cd /workspace && git status && git log --oneline -3 && gh auth status
cd /workspace/widellama && git status && docker info
cd /workspace/widellama-product-specs && ./scripts/verify.sh --strict
ls /workspace/.agents/skills/*/ /workspace/.grok/skills/*/ /workspace/.hermes/skills/*/   # specv1 present?
```

If anything's red, fix it here before new work — no new work on a dirty base.

## The rules (unchanged, load-bearing)

- **Specs repo is the product source of truth.** Implementation waits on the spec.
- **GHW everywhere**: topic branches → PR → `development` → release PR → `main`; no rebase; no direct pushes to `main`/`development`.
- **`upstream` is never pushed to.**
- **Specs AUDIT before every MAJOR/MINOR spec release**; AUDIT never modifies spec folders.
- **Pilot decides MUST-level changes**; agents contribute, never approve.
- If something in this handoff is stale, update the handoff in the same commit that fixes the stale thing.
