# Mission Script — WideLlama

*Written form of the Vibe. Directive, not poetry: the Pilot sets the direction; the Master and the agent swarm execute inside it. Updated only by Pilot decision.*

> **Run serious multi-agent work on your own infrastructure — planned, metered, auditable — and prove it in public by shipping the specs, the audits, and the receipts.**

## The three truths

1. **Specs before code.** The product rebuild doesn't begin from the pilot's convenience; it begins from `widellama-product-specs`, the source of truth. ADRs bind; requirements trace; audits gate.
2. **Local-first, always.** WideLlama stays an on-prem / VPC product. Cloud is an explicit, audited opt-in — never a default, never silently implied, never for the wireframe demo only.
3. **Evidence beats enthusiasm.** No claim ships without an audit trail: schema validation, spec AUDIT reports, PR gates, tags you can verify. If we said it, we can show it.

## What the workspace is for

This repository is the home turf for WideLlama's build: the product specs repo, the reference lab, and the WideLlama organization's process. It is scaffolding with sharp edges — GHW git workflow across three repos, the spec as contract, the agent swarm as labor, the Pilot as the only decision authority.

## Definition of done (rolling)

A Lap is complete when: (1) the specs repo passes `verify --strict` and specv1 `AUDIT`, (2) the reference lab is green on `pytest`, (3) every requirement carries an ID a buyer's security review can check, (4) nothing merged without a PR and a gate.

## Non-negotiables

- The Pilot (Jean Machuca) owns every MUST-level change. Agents contribute, never approve.
- `upstream` (`jeanmachuca/aiworkspace`) is never pushed to — it is scaffolding archaeology.
- Production domain `widellama.com` — all schema identities, docs, and messaging converge on it (ADR-0015).
- Nothing merges straight to `main`; `development` is the integration line; tags mark promotions.

## The Vibe in one line

**A disciplined race: local-first, specs-locked, audit-gated — executed like there's an inspection on the other side every step.**
