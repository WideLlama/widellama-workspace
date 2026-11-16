# HUD — the WideLlama Scoreboard

*Telemetry, not opinions. 15-minute scan per Lap. Baselines recorded honestly; unknowns say "n/m" (not measured), never a guessed number.*

## IRA thresholds (agent-output quality — what the Pilot sees)

| Signal | WARN | FAIL | Notes |
|---|---|---|---|
| Tasks returned matching the Pilot's intent (IRA sampling per Lap, n≥10) | < 80% | < 60% | Score with the IRA rubric; sample real agent outputs, not self-reports |
| Agent PRs merged without rework-after-merge per Lap | > 1 | > 2 | Merged ≠ done if it comes back broken |
| Spec deviations introduced by agents (post-merge AUDIT findings attributable to agents) | 1 | ≥ 2 | Zero-tolerance class — spec wins or ADR required |

## Circuit Delta (target improvement per Lap)

| Metric | Baseline (Lap 0, 2026-11-16) | Target next Lap |
|---|---|---|
| Spec AUDIT findings open | 0 blocking (all 2026-11-16 findings remediated) | 0 |
| Verified-green PRs merged this Lap | ~14 (2026-11-16: promotions across all three repos) | ≥ 1 promotion in every active repo |
| Repos with `development` integration line + GHW flow | 3 of 3 | 3 of 3 — enforce everywhere |
| Docs/spec drift found in AUDIT | 5 (2 blocking + 3 advisory) | ≤ 2, all advisory |
| Tokens per merged PR | n/m | n/m — instrument before optimizing |
| Time from spec change → merged, tagged | n/m | measure in Lap 1 |

## Scoreboard rows that actually matter right now

| Row | Status | Read as |
|---|---|---|
| Specs repo released | `v0.1.0` (audit PASS) | Healthy |
| Reference lab gate | `pytest` green on every promotion | Healthy |
| CI in specs repo | `verify` required-looking but not yet branch-protected | Watch — enable protection |
| Release-to-`main` promotions | all via PR | Healthy — never by hotfix |
| Actions on fork (`widellama-workspace`) | disabled; auto-PR inert | Known gap — manual PRs |
| `v0.2.0` spec release | undecided; waiting on Pilot call | Pending Pilot decision |

## What replaces the status meeting

The scoreboard. Any time the Pilot asks "how's it going", the answer is: open `PIT-STOP.md`, read the table, ask what's off. If a Lap ends without touching this file, the Lap didn't run.
