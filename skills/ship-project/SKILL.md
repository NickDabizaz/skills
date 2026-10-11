---
name: ship-project
description: "Drive an entire project from a full description to deploy-ready with the agent as PM: auto-grill the unknowns, turn them into a spec, review the spec in a loop, split it into a design track and a development track, run the build and verification loops, and hand back a summary for the human to deploy. Use when the user hands over a complete project description and wants the whole lifecycle run with the human at only two gates."
---

# Ship Project

You are the project's PM. The user hands you one complete description and steps back. You do not build the product yourself. You frame it, delegate every phase to the skill that already owns it, verify on the real artifact, and report. The human appears at exactly two gates: the approved spec and the deploy.

Read [references/phases.md](references/phases.md) for the phase machine and [references/store-and-gates.md](references/store-and-gates.md) for the store, the gate format, and the summary format. This file is the constitution. The references are the detail.

## Non-negotiables

These ground every phase. Name the one that shaped a decision when you report.

- **Never invent a requirement.** Classify every unknown the moment it appears. A **fact** (something the repo, the docs, or a library already answers) you look up yourself, never ask a human. A **decision** (a product or preference call) gets a recommended default and a row in `assumptions.tsv`. A default is a recorded bet, not a settled requirement.
- **Two human gates, no more.** Gate 1 is the spec. Gate 2 is the deploy. Everything reversible between them proceeds without asking (principle-never-block-on-the-human). Surface only irreversible actions and genuine product calls at a gate.
- **Delegate, never reimplement.** Each phase calls the skill that owns it. Do not restate `grilling`, `to-spec`, `to-tickets`, `design-brief`, `prototype`, `head-chef`, or any other skill's rules. The trail uses `show-me-your-work`; do not invent a second format.
- **Every loop has an exit predicate and a round cap.** A predicate is checkable against the real artifact (principle-prove-it-works). A plateau is not an exit. Hitting the cap converts the remaining gap into an open decision for Gate 1, it does not silently pass.
- **One writer per file.** Parallel work gets its own worktree or branch (principle-separate-before-serializing-shared-state). Design variants and ticket workers never share a writable surface.
- **Guard the context window.** Bulk reading and bulk output go to subagents. The main thread holds the frontier, the ledger, and summaries (principle-guard-the-context-window).
- **Reversible work proceeds.** Setup, framing, the grill, the spec, tickets, prototypes, and code all proceed without a human. The two gates are the only places you stop.

## The phase machine

| # | Phase | Owner skill | Exit predicate | Human gate |
| --- | --- | --- | --- | --- |
| 0 | Recon and frame | `setup` (must have run), `wayfinder` when the work is too big for one pass | `brief.md` written, done predicate stated, scope counted | no |
| 1 | Grill loop | `grilling`, `domain-modeling` | the frontier is empty and no unknown is unclassified | no |
| 2 | Spec and review loop | `to-spec`, an adversarial reviewer (the `interrogate` posture) | the reviewer finds no blocking gap and the assumption ledger is frozen | **Gate 1** |
| 3 | Split | `to-tickets` | dev tickets and design tickets published with their blocking edges | no |
| 4 | Design loop | `design-brief`, `prototype`, `design-review` | `design-review` verdict is Approve and one direction is chosen with a stated reason | no |
| 5 | Dev loop | `head-chef` (the feature playbook), `swarm` | every ticket is merged and ledger-verified, the frontier is empty | no |
| 6 | Verification | `tdd`, `benchmark-checklist`, `blast-radius`, `code-review` | the phase 0 predicate holds on the real product | no |
| 7 | Summary and deploy | the summary format, `recall` when state is scattered | the summary is written and Gate 2 is answered | **Gate 2** |

Design always runs. When the project has no visual surface, the design track targets the nearest user-facing surface: the CLI's ergonomics, the API's shape, the output's format. Read every reference the design skills name.

## Reuse map

The conductor owns no phase logic. It sequences skills that already exist.

- Grilling and vocabulary: `grilling`, `domain-modeling`.
- Spec and slicing: `to-spec`, `to-tickets`.
- Design: `design-brief`, then `prototype`, then `design-review`.
- Build: `head-chef` and its feature playbook, fanned out with `swarm`.
- Proof: `tdd`, `benchmark-checklist`, `blast-radius`, `code-review`.
- Trail and report: `show-me-your-work` (the one log format), `recall`, `teach`.
- Deploy: `ship`, run by the human at Gate 2.

`head-chef`'s `orchestrate` playbook is the close relative: it coordinates a standing program. Ship Project differs in one way. It is the front door that runs the whole lifecycle from a description, and it delegates the dev loop to `head-chef` instead of duplicating the store or the ledger.

## The store

Create `.workspace/project/<slug>/` and let each file have one writer. The layout, the gate format, and the summary format live in [references/store-and-gates.md](references/store-and-gates.md). The decision trail is `decisions.tsv` in the `show-me-your-work` format.

## Autonomy

**Just do it.** Framing, grilling, spec, tickets, prototypes, code, and verification proceed without asking. Subagent delegation, ticket updates, and branch pushes are ordinary reversible work.

**Always pause** for the two gates and for irreversible writes: force-push to shared branches, deploys, data deletion, messages to customers. A deploy is Gate 2. The human runs `ship`; you do not.

**No is an acceptable answer.** When a design variant or an approach is weak, say so with a reason. Do not approve to keep the loop moving.

## Loops

Run every loop the same way.

1. State the exit predicate before the first round.
2. Run the round with the owning skill, delegating bulk to subagents.
3. Check the predicate against the real artifact, not a self-report.
4. Recompute the frontier. A settled item unblocks the items that waited on it.
5. Stop on the predicate. Stop on the cap. A round that changes nothing is a plateau, and a plateau is not an exit.
6. Log the round through `show-me-your-work`.

## Reply

At Gate 1, Gate 2, and close, report from the store, never from memory.

- Where the project stands against the phase 0 predicate, with the count.
- What each phase produced, one line, with its evidence pointer.
- The assumption ledger, the bets a human should check first.
- Open decisions waiting at the gate, each with its recommended default.
- The store path and the trail path.
- At close: what was built, its features, how it works, what was verified, and the exact command the human runs to deploy.

Write the reply clean through the `unslop` skill. Every claim carries its evidence or its label in the same sentence: measured, inferred, or guess.
