# Org Geometry — WideLlama (Diamond Squad)

*Target state vs today. Do not claim staffing we don't have — the Diamond is planned, not implemented.*

## Current reality (2026-11-16)

- **Pilot:** Jean Machuca — the only decision authority (direction, capital = compute, merge calls).
- **Human specialists:** none appointed yet. Not 0-of-4 laziness — the program is pre-partner; a second human enters with a design partner or co-founder decision.
- **Agent swarm (the actual labor):** `specv1`, `ghw`, `ira-prompting`, `mission-script`, `hud-setup`, `org-geometry`, `pit-stop-audit` (locked in `skills-lock.json`).

**Current shape:** solo Pilot + agent swarm. The "Diamond" is aspirational, labeled as such.

## Target Diamond (when the org activates)

| Vertex | Role | Who | Lane (owns) |
|---|---|---|---|
| 1 | **Pilot** (the Double Tenaza — direction + capital) | Jean Machuca | Vision, specs-of-record decisions, release calls, external accountability |
| 2 | **Spec Lead** | (Pilot, or appointment) | `widellama-product-specs` integrity — specv1 AUDIT, release discipline, schema publication |
| 3 | **Infra/Gate Lead** | (appointment) | CI gates, branch protection, `widellama-tests`, delivery sanity |
| 4 | **Field/Adoption** | (appointment with first design partner) | Installation UX, onboarding bridge docs, partner feedback into the spec |
| 5 | **NPC agents** (swarm) | local skills + workers spawned by the product (later) | Grind: schema checks, dependency sweeps, audit runs, pack validation, test migration |

No human specialist works directly off the Pilot; the Master (or, today, the Pilot-as-Master-with-agents) routes work into lanes, closes against gates, and the traffic never bypasses the Pilot's sign-off on MUST-level changes.

## NPC agent roster (skills as agents, not as vibes)

| Agent | Trigger | Delegated authority |
|---|---|---|
| `specv1` | Spec authoring/audit | Produce AUDIT-REPORT.md; never modify spec folders |
| `ghw` | Any git op | Branch/PR/tag flow; never rebase; never force |
| `ira-prompting` | Writing agent instructions | Seven-technique pass + IRA rubric score before dispatch |
| `mission-script` | A new initiative | Draft the Vibe before any spec work starts |
| `hud-setup` | Telemetry design | Scoreboard edits only; never change targets silently |
| `pit-stop-audit` | Lap-end | Calibration notes; Pilot reviews before anything else |

## Rules

1. Agents MUST NOT approve their own output past a gate.
2. The Pilot MUST decide all MUST-level spec changes; agents tee up the change, Pilot disposes.
3. No new agent lane without a gate and an owning outcome (no "assistant agents" for vanity).
4. When a second human is appointed, backfill this file before granting repo write access.
