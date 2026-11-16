# AI Workspace

**Root is scaffolding, not code.** This repo (`WideLlama/widellama-workspace`, a fork of `jeanmachuca/aiworkspace` via `upstream`) provides shared structure for AI-assisted work. There is no root application, build, or test suite — don't invent one.

## Layout

- **Each subfolder is a standalone git repo** with its own tooling and conventions; its own `AGENTS.md` is expected but not universal (`widellama/` doesn't have one). `.gitignore` uses `/*/`; only `/.github/` and `/.opencode/` are tracked at root.
- **Root tooling is pre-commit only** (`pip install -r dev-requirements.txt && pre-commit install`). Hooks: trailing-whitespace / end-of-file-fixer (auto-fix on commit), `check-yaml`, `check-added-large-files` (max 500 KB).
- Root commands that exist: `pre-commit run --all-files` (verification), `./start.sh` (install+launch local inference server — manual, needs Docker and an interactive TTY, captures the terminal), `./start-container.sh` (build+run the workspace container with Docker socket mounted), `./download_qwen.sh` (fetch Qwen2.5-Coder-3B-Instruct Q4_K_M into `./models/model.gguf` and the `aiworkspace_model_data` volume).
- CI: `open-pr-to-development.yml` (auto-PR on push to `feature/**`, `fix/**`, `bugfix/**`) and `main-pr-source.yml` (PRs to `main` must come from `development`) are functional. `ci.yml` is a placeholder (echo-only jobs). `publish.yml` is a complete GHCR workflow — on push to `main` and on `v*` tags it builds and pushes the root `Dockerfile` to `ghcr.io/${{ github.repository }}` (no test stage).

## Instruction files and opencode.json

- `opencode.json` `instructions` array auto-loads `AGENTS.md` and `.opencode/instructions/git-workflow.md` in every session. Do not duplicate git-workflow content into `AGENTS.md`.
- **Gotcha:** the array also references `nacedigital-landing-page/.opencode/instructions/secrets.md`, which does **not** exist in this repo — expect a missing-instruction warning/error; the reference is stale.
- The `ghw` skill is the **canonical git workflow** (topic branches from `development`, PRs, no rebase, sync, SemVer tags). `.opencode/instructions/git-workflow.md` is a thin pointer to it plus instance-specific SSH/auth — `docs/git-workflow.md` was removed as a stale duplicate. Don't reintroduce copies; reference the skill.
- Default model is local inference: `code-inference/model.gguf` at `http://api:8000/v1` (16k context). It only works if the local server is running (`./start.sh`); switch models with `/model`. Cloud aliases in `opencode.json`: `big-pickle`, `deepseek-v4-flash-free`, `mimo-v2.5-free`, `nemotron-3-ultra-free`.
- Skills live in `.agents/`, `.claude/`, `.grok/`, `.hermes/` (GHW + SPECv1 + the Vibe Leading suite — adopted as the workspace methodology, see **Vibe Leading**) — all git-ignored (`/*/`), so payloads are installed locally, never committed; root `skills-lock.json` is the only tracked record. `.opencode/` contains only `instructions/`. SPECv1 is missing from `.grok/` and `.hermes/`.

## Subfolder repos

- **`widellama/`** is the one existing project: standalone repo `WideLlama/widellama` (origin uses **HTTPS**, unlike everywhere else — do not "fix" it without asking). Product: local-first multi-agent orchestration lab (Ollama + OpenClaw + llama-model + Python pilot). Its `CONTRIBUTING.md` mandates **no host installs** — nothing runs outside Docker; tests via `docker compose` / `scripts/widellama-pytest.sh` (ADR-0008). Product docs in `widellama/docs/widellama/` (start with `README.md` there). It has **no `AGENTS.md` of its own** — only this file applies when working from root.
- When starting a new project, create the subfolder as its own repo with its own `AGENTS.md`; root ignores it by default.

## Git workflow

The `ghw` skill is canonical; `.opencode/instructions/git-workflow.md` (auto-loaded) is a thin pointer to it plus instance SSH/auth. Summary: topic branches from `development` (`feature/`/`fix/`/`bugfix/` — auto-PR covers exactly these), no rebase, PRs into `development`, `development` → `main` via release PR. Applies to subfolder repos too; subfolders must not override it. All three WideLlama org repos — `widellama-workspace`, `widellama`, `widellama-product-specs` — carry `development` and follow GHW end-to-end: topic branch → PR → `development`, then `development` → `main` release PR with a SemVer tag. Root remotes: `origin` = fork (`WideLlama/widellama-workspace`), `upstream` = template (`jeanmachuca/aiworkspace`) — scaffolding reference; **never push to `upstream`**. `origin/development` is this repo's integration line; `main` accepts PRs only from `development` (`main-pr-source.yml`).

## Vibe Leading (methodology)

This workspace adopts the **Vibe Leading** framework for directing AI-assisted work. Skills — locked in `skills-lock.json`, auto-available, use them when the task matches the trigger:

- `mission-script` — write/calibrate strategic intent (the Vibe, as a spec) handed to agents or a deliverable.
- `hud-setup` — define/calibrate the Scoreboard HUD (IRA thresholds, Circuit Delta) replacing status meetings with telemetry.
- `org-geometry` — design the Diamond Squad (Pilot + specialists + AI swarm) and NPC agent roles.
- `ira-prompting` — the seven IRA techniques for writing agent instructions; score prompt quality with the IRA rubric.
- `pit-stop-audit` — calibration rituals at Lap end / month-end / kickoff (Pit Stop, Vibe Audit, Pilot's Final Checklist).

They guide *how work is directed and reviewed*, not code conventions. Use them proactively when a task involves intent, telemetry, team/agent structure, prompt quality, or audits — not just when the user names them.

## Auth

**SSH only — never HTTPS.** Remotes must be `git@github.com:`. `GH_TOKEN` must not be set or relied upon (may be stale); if re-auth is needed: `unset GH_TOKEN && gh auth login --git-protocol ssh --web`. Host `~/.ssh/config` may contain macOS-only `UseKeychain` lines — `~/.profile` filters them via `GIT_SSH_COMMAND`; if you see `Bad configuration option: usekeychain`, that's why. `~/.ssh/` is read-only — `UserKnownHostsFile` must point at `/tmp/`.

## Temp files

Prefer `/tmp/opencode`. It may be root-owned and unwritable — fall back to a temp subdirectory under `/workspace` rather than other system temp dirs.

**Filesystem artifact:** this overlay filesystem creates AppleDouble `._*` files on writes. Delete them on sight; never commit them (root and widellama `.gitignore` carry `*._*`). Scripts may have lost their exec bit in git — use `git update-index --chmod=+x`. `.git/objects/pack/._pack-*` paths produce `non-monotonic index` warnings on every git command — harmless; do **not** hand-delete anything under `.git/`.

## Verification

At root the only check is `pre-commit run --all-files`. For subfolders, use whatever that repo defines (e.g. widellama: pytest inside Docker, never on the host).
