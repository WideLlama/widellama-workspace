# .vibe — Vibe Leading artifacts for this program

This folder holds the **Vibe Leading** context for the WideLlama program, authored for this workspace and committed so it survives the container rebuild. It is the written form of how the Pilot directs this work — read it before doing substantive work.

## Skills used (all locked in `skills-lock.json`, payloads git-ignored — reinstall from sources if wiped)

| Artifact | Skill | Source |
|---|---|---|
| `MISSION.md` | `mission-script` | `VibeLeading/mission-script` |
| `HUD.md` | `hud-setup` | `VibeLeading/hud-setup` |
| `ORG-GEOMETRY.md` | `org-geometry` | `VibeLeading/org-geometry` |
| `PIT-STOP.md` | `pit-stop-audit` | `VibeLeading/pit-stop-audit` |
| (in `05`→`07` folders of the specs repo and in `.opencode/instructions/`) | `ira-prompting` | `VibeLeading/ira-prompting` |

Not here: `ghw` (git workflow — canonical for this repo, see `.opencode/instructions/git-workflow.md`) and `specv1` (spec engine — in use in the specs repo).

## How to read

- `MISSION.md` — the Vibe: why WideLlama, why now, what "done" means, the non-negotiables.
- `HUD.md` — the Scoreboard: what we measure, thresholds, Circuit Delta targets; update after each Lap.
- `ORG-GEOMETRY.md` — the Diamond Squad for WideLlama as it stands today (solo Pilot + agent swarm) and the target shape.
- `PIT-STOP.md` — the Lap-end calibration: what just happened, what the scoreboard says, what the next Lap owes.

Maintenance ritual: refresh `PIT-STOP.md` and the HUD after each milestone; the Mission Script changes only with Pilot decision.
