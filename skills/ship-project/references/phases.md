# Phases

The conductor works top to bottom. Each entry gives the input, the steps, the exit predicate, the round cap, and what to do when it stalls. Follow the owner skill for the phase. This file only sequences it.

## Phase 0: Recon and frame

Input: the user's project description and the repository.

1. Confirm `setup` has run for this repo. If it has not, run it first. It records the tracker, the triage vocabulary, and the execution defaults the later phases read.
2. Read the repo state: manifests, source tree, existing docs, test setup, design tokens.
3. Write `brief.md`: the project in the user's words, the goal, and what is out of scope.
4. State the done predicate as something checkable on the real artifact, for example "the app builds, the checkout flow completes, and the suite is green". Count the scope: rough tickets, rough effort, expected surfaces.
5. When the work is clearly too big for one pass, sketch the decision map with `wayfinder` before grilling.

Exit: `brief.md` exists, the predicate is falsifiable, the scope is counted.

Cap: none. Stop only when framed.

Failure: if `setup` cannot run, record it as a gate and continue with local Markdown defaults.

## Phase 1: Grill loop

Input: `brief.md` and the repo.

1. Run `grilling` as the PM. Work the design tree in rounds, asking the whole frontier each round.
2. Classify every question before answering it.
   - Fact: dispatch a subagent to find it. Never put it to the human or to a proxy.
   - Decision: hand it to a user-proxy subagent that answers from the description, the repo, and the domain docs. The proxy returns a recommended answer and a confidence. Record it as a row in `assumptions.tsv`, not as a settled requirement.
3. When a decision has no basis in the description at all, mark it open with a recommended default and let it wait for Gate 1. Do not manufacture a requirement.
4. Keep the vocabulary consistent through `domain-modeling`, which also writes the glossary and the ADRs.

Exit: the frontier is empty and every unknown has a class and a resolution.

Cap: stop after N rounds (default 5) or the first round that adds no new question. Convert what remains into open decisions.

Failure: if the proxy contradicts the description, the description wins. Log the conflict as an open decision.

## Phase 2: Spec and review loop

Input: the settled grill and the assumption ledger.

1. Run `to-spec` to synthesize the conversation into `spec.md`. Do not interview the human.
2. Spawn an adversarial reviewer on a different model family from the one that wrote the spec. It attacks the spec: untestable user stories, contradictions, missing states, decisions with no basis, seams that do not match the repo. This is the `interrogate` posture, scoped to the spec.
3. Findings that are gaps return to the grill frontier and feed a new round. Findings that are decisions become open decisions.
4. Re-run `to-spec` after each pass. Freeze the assumption ledger when the reviewer finds no blocking gap.

Exit: no blocking gap survives a full review pass and the ledger is frozen.

Cap: 3 passes. Remaining gaps become open decisions at Gate 1.

Gate 1: present the spec, the assumption ledger, and the open decisions, each with its recommended default. Proceed on the defaults when the human does not answer. Record the human's corrections as settled decisions.

Failure: a spec the reviewer keeps rejecting is a premise problem. Take the premise itself to Gate 1 rather than looping.

## Phase 3: Split

Input: the approved spec.

1. Run `to-tickets`. Produce tracer-bullet tickets, vertical, each with its blocking edges.
2. Tag each ticket as design or development. Design tickets precede the dev tickets that depend on them.
3. Publish to the configured tracker in dependency order.
4. Build the frontier: the tickets whose blockers are all done.

Exit: every slice is a ticket with edges, and the frontier is computable.

Failure: granularity the spec cannot settle goes back to Phase 2 as a spec gap.

## Phase 4: Design loop

Input: the design tickets and the spec.

This runs for every project, visual or not. With no visual surface, the surface is the CLI, the API, or the output format.

1. Run `design-brief`. Read the spec, the project tokens, and the design guidelines first. The brief covers screens and states, layout, content, interactions, visual direction, motion intent, and the accessibility path. Use [animation-vocabulary.md](../../design-brief/references/animation-vocabulary.md) for motion terms.
2. Run `prototype` in explore mode: three to five genuinely different variants on named axes, each in its own worktree, fanned out with `swarm`. Every variant meets the craft bar on its own. Read the prototype references: [recipes.md](../../prototype/references/recipes.md), [library-picks.md](../../prototype/references/library-picks.md), and [picker.md](../../prototype/references/picker.md).
3. Run `design-review` on the brief and the variants. Read [standards.md](../../design-review/references/standards.md) and [catalog.md](../../design-review/references/catalog.md). Fix and re-review until the verdict is Approve.
4. Choose one variant, or the one direction when the brief was specific. State the reason. Surface the choice at Gate 2 so the human can override it.
5. Promote the chosen direction. Delete the prototype surface unless the spec asks to keep it.

Exit: `design-review` returns Approve and one direction is chosen with a written reason.

Cap: N rounds per brief (default 3). A brief that cannot reach Approve escalates to Gate 1.

Failure: if every variant loses, the brief is the problem, not the variants. Return to the brief.

## Phase 5: Dev loop

Input: the dev ticket frontier and the chosen design.

1. Work the frontier. Any ticket whose blockers are all done is ready.
2. Run each ticket through `head-chef`'s feature playbook. One ticket, one fresh subagent, one worktree or branch. Fan out independent tickets with `swarm`; keep one writer per worktree.
3. Each ticket ends in working code on its branch, verified on the real surface, reviewed by `code-review`, and shaped into a PR by `pr`. The ledger gets a verdict row keyed by ticket, PR, and head SHA.
4. Respect the edges. A blocked ticket waits. Never start it early to keep a worker busy.
5. Recompute the frontier after each merge. Relay upstream results into the downstream briefs, because workers cannot see siblings.

Exit: every ticket is merged and ledger-verified and the frontier is empty.

Cap: per ticket, the `autonomous-run` discipline. A plateau is not done. Two failed retries abandon the ticket and replan around it.

Failure: a ticket that cannot verify is a bug in the ticket or the spec, not a reason to lower the bar. Route it back one phase.

## Phase 6: Verification

Input: the merged work and the phase 0 predicate.

1. Drive the real product end to end, not the harness. Where a test fits, write it first and watch it fail (`tdd`).
2. Run `blast-radius` for what the change could break beyond the diff.
3. Run `benchmark-checklist` before trusting or reporting any measured number.
4. Spawn a verifier on a different model family from the builders for the end-to-end pass. CI green is an input to a verdict, not a verdict.

Exit: the phase 0 predicate holds on the real product, with evidence.

Cap: one verification pass plus one fix pass. An unmet predicate after the fix pass goes to Gate 2 as an open item, never as a silent pass.

Failure: a predicate that was wrong goes back to Phase 0 and is restated honestly.

## Phase 7: Summary and deploy

Input: the store, the ledger, and the trail.

1. Write the summary in the format in [store-and-gates.md](store-and-gates.md). From the store, not from memory.
2. Use `recall` if the state is scattered across sessions. Use `teach` if the human wants to understand a subsystem.
3. Open Gate 2. The human runs `ship`. You do not deploy.

Exit: the summary is delivered and Gate 2 is answered.

Failure: none. This is the hand-back.
