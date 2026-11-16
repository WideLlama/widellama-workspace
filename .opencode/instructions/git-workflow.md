---
description: Git workflow — GHW skill is canonical; this file adds instance-specific SSH/auth
alwaysApply: true
---

# Git workflow

The canonical git workflow for this repo is the **`ghw` skill** (locked in `skills-lock.json`, installed under `.agents/skills/ghw`). It defines: topic branches (`feature/`/`fix/`/`bugfix/`) from `development`, PRs into `development` via UI/`gh pr create`, no rebase, sync procedure, release flow (`development` → `main` release PR, annotated SemVer tags; optional `-dev.N` integration tags).

Keep one source of truth: reference or link the skill — don't copy its rules into other files (`AGENTS.md`, `README.md`, docs). If the rules and the skill disagree, the skill wins; upstream the fix to the skill, not to a copy.

The bundled auto-PR workflow (`.github/workflows/open-pr-to-development.yml`) fires on push to exactly `feature/**`, `fix/**`, `bugfix/**`. Any other branch prefix pushes silently with no PR.

## SSH config workaround (Linux container, macOS host)

If `git push` fails with `Bad configuration option: usekeychain`, the host's `~/.ssh/config` contains macOS-only `UseKeychain` directives that OpenSSH on Linux doesn't understand.

This is handled automatically by `~/.profile` (see `AGENTS.md`), which sets `GIT_SSH_COMMAND` to filter out the offending lines.

## Auth — SSH only, never HTTPS

**This instance is pre-configured with SSH keys for `gh` and `git`. Never use HTTPS.**

- Remote URLs must use `git@github.com:` (SSH), never `https://github.com/`.
- `GH_TOKEN` must not be set or relied upon. If it contains stale credentials, unset it before running `gh` commands.
- Do not set `GH_TOKEN` from `~/.config/gh/hosts.yml` or any other source.
- If re-auth is needed, use the device flow with `--git-protocol ssh`:
  ```bash
  unset GH_TOKEN && gh auth login --git-protocol ssh --web
  ```
- `~/.ssh/` is on a read-only filesystem, so `UserKnownHostsFile` must point to `/tmp/`:
  ```bash
  export GIT_SSH_COMMAND="$GIT_SSH_COMMAND -o UserKnownHostsFile=/tmp/known_hosts"
  ```
