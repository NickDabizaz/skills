---
name: writing-for-agents
description: "Writing documents an agent reads. Use when creating or editing a skill, or editing CLAUDE.md, AGENTS.md, CONTEXT.md, or DESIGN.md."
---

Reference for any document an agent reads: a skill, `CLAUDE.md` / `AGENTS.md`, `CONTEXT.md`, a spec, a prompt. The packaging differs; the writing does not. The reader has already read everything, so explanation is waste and precision is the whole job. The default move is deletion.

When the document is a skill, read [SKILL-MECHANICS.md](SKILL-MECHANICS.md) for frontmatter, invocation, Codex metadata, and the layout every skill in this set follows.

## The two loads

Every line and pointer spends one of two budgets:

- **Context load**: material loaded every turn whether or not it fires (a `CLAUDE.md` line, a skill description). Paid by the agent, always.
- **Cognitive load**: the human remembering which documents exist and when to reach for each. Paid by the human. Not a cost to minimise: it is the price of human control. Spend it where judgement matters.

Material behind a pointer costs only the pointer's line until it fires. Anything relevant in one run out of ten pays context load the other nine. Every split-or-inline, point-or-push decision is this trade in a different place.

## Context pointers

A **context pointer** is a line held in context that names material outside it and says when to reach for it: a skill description, a `CLAUDE.md` line naming a doc. The pointer's wording, not its target, decides whether the agent reaches through it. A must-have target behind a weak pointer is a bug in the pointer: sharpen the wording first; inline only if sharpening fails.

A pointer states what the material is and lists the **branches** that trigger it (a branch is a distinct case the document handles). It is always loaded, so it is pruned harder than any body: front-load the leading word, one trigger per branch, no synonyms restating one branch, no identity the body already carries.

## Information hierarchy

A document mixes **steps** (what the agent does, in order) and **reference** (rules and facts consulted on demand). Each piece sits on one rung:

1. **In-file step**: the primary tier.
2. **In-file reference**: consulted on demand; a flat set of rules is fine here.
3. **Disclosed reference**: a separate file behind a pointer, loaded only when it fires.

**Progressive disclosure** is the move down the ladder so the top stays legible. The test is branching: inline what every branch needs; push behind a pointer what only some branches reach. Keep pointers one level deep: a file that points at a file that points at the answer gets skimmed, not read.

**Co-location**: keep a concept's definition, rules, and caveats under one heading. Scattering fragments one meaning across many places, and the reader either reassembles it or misses it.

**Sprawl** is the failure here: too long even when every line is live. Cure it with the ladder, and split by branch or by sequence.

## Completion criteria

Every step ends on the condition that says it is done. Two properties make it a lever:

- **Clarity**: can the agent tell done from not-done? "Understanding reached" invites **premature completion**; "no open decision would change what gets built" does not. Sharpen the bound before anything else.
- **Demand**: how much the criterion requires. "Every modified file accounted for" forces legwork that "produce a list" does not.

The strongest criteria are checkable and exhaustive.

## Leading words

A **leading word** is a compact concept the model already holds (*tight*, *red*, *tracer bullet*, *relentless*) that the agent thinks with while running the document. Repeated as a token, never as a sentence, it anchors a region of behaviour for the fewest tokens. It works twice: in the body, the same behaviour every time it appears; in a pointer, the same word across prompts and docs makes the agent reach the material reliably.

Hunt for restatements a leading word retires: "fast, deterministic, low-overhead" is *tight*. A word too weak to beat the default (*be thorough*) is a no-op; the fix is a stronger word (*relentless*), not more sentences.

**Negation** is the trap beside this lever: a prohibition drags the banned behaviour into context and makes it more available. State the positive target. Keep a prohibition only as a hard guardrail you cannot phrase positively, and pair it with the positive.

## Pruning

- **Single source of truth**: each meaning lives in one place. **Duplication** costs tokens and maintenance, and inflates a meaning's rank on the ladder.
- **The environment is a source of truth**: `package.json` scripts, configs, `--help` output. A document restating them is a cache that goes stale. Cache only what cannot be looked up: the unwritten convention, the reason behind a choice, the gotcha.
- **Relevance**: does the line still bear on what the document does? Stale layers nobody removes are **sediment**.
- **The no-op test**, sentence by sentence: would the agent behave differently without this line? If not, delete the whole sentence, never trim it. The test is behavioural, not aesthetic: settle a disagreement by running the document, not by arguing.

## This skill set

This reference owns the documents of the set: the core skills `brainstorm`, `discuss`, `discuss-with-docs`, `investigate`, `audit`, `implement`, `implement-all`, `review`; the shared loops `discussing`, `implementing`, and `designing`; the supporting skills `setup-new-project`, `setup-project`, `write-tickets`, `resolve-conflicts`; `CLAUDE.md` / `AGENTS.md`; `CONTEXT.md`; `DESIGN.md`; and every supporting skill added beside them.

- **Naming**: lowercase, hyphens, no reserved words. A core skill is one bare verb (`discuss`); a variant of it adds a suffix (`discuss-with-docs`). A shared loop or reference that several skills call is a gerund (`discussing`). A supporting skill is verb plus object (`write-tests`, `resolve-conflicts`). A name says what the skill does, never where it belongs or who made it.
- **Chain**: `discuss` or `discuss-with-docs → write-tickets → implement or implement-all → review`, with `brainstorm` as the entry when there is no direction yet, `investigate` as the entry for bugs, `audit` as the entry for improving what exists, and `setup-new-project` or `setup-project` run once per own project. A supporting skill hangs off one step of the chain and is reached from it by calling the Skill tool, or by the user typing it. Its description says which.
- **Modes**: a skill that behaves differently in an own project and in legacy points at `MODES.md` for the difference; it never restates the table.
- **One meaning, one home**: a rule two skills need lives in one model-invoked skill they both call (`discussing` behind the discuss entry points, `implementing` behind the implement ones), or in one plain file both point at (`MODES.md`, `TICKET-FORMAT.md`). Never in both.
- **Router**: `ask-me` is the one skill the user has to remember; it names every other user-facing skill and when to reach for it. A skill added, renamed, or removed changes its routes table in the same edit.
- **Editing pass**: read the document, name the failure mode first (duplication, sediment, sprawl, no-op, weak pointer, premature completion, negation), then fix that one. Done when the document works and no failure mode is left to name.
