---
name: implement-all
description: "Build every open ticket of one spec: in parallel where nothing blocks, one branch each, merged into a target branch, reviewed as a whole against the spec."
argument-hint: "[path to .workspace/<issue-name>/spec.md] [target branch]"
disable-model-invocation: true
---

Own projects, plus an audit spec in a legacy repo ([MODES.md](../implementing/MODES.md)). One spec per run. No open ticket for it: stop and tell the user to run `/write-tickets`.

## Setup

1. **Target branch**: the argument, else one question with options (the current branch, the default branch, a new integration branch) and a recommendation.
2. **Spec**: the `.workspace/<issue-name>/spec.md` the argument names; else, when exactly one spec folder in `.workspace/` has open tickets, that one; else ask. The final review needs it.
3. **Graph**: read every open ticket of that spec (`.workspace/<issue-name>/tickets/`, or `gh issue list --label issue:<issue-name>`) and its `blocked-by`. A cycle stops here and goes to the user.

## Loop

Until no open ticket remains:

1. **Ready set**: open tickets whose blockers are all `done`.
2. **Build**: each ready ticket on its own branch `ticket/<id>-<slug>` cut from the target, by calling the Skill tool with "implementing" on that ticket, ending with one commit when its review passes. If the harness offers sub-agents with worktree isolation (Claude Code: the Agent tool with `isolation: "worktree"`), run the ready set in parallel, one agent per ticket, each told to do exactly that and that this run owns final integration verification. A worktree lacks the gitignored files: copy `CONTEXT.md`, `DESIGN.md`, `DECISIONS.md`, `CLAUDE.md` / `AGENTS.md` where present, and `.workspace/` into it before the build, and copy the ticket file (boxes, status) and verification evidence back after. Include referenced assets outside these paths and verify baseline paths resolve before starting. Shared design or baseline changes must be reconciled on the target and propagated to dependent tickets before continuing. Otherwise build them one after another in this checkout. A build that stops on a question brings the question to the user, then resumes.
3. **Merge** finished branches into the target in ticket-id order. A conflict: call the Skill tool with "resolve-merge-conflicts", then continue.
4. Recompute the ready set.

## Finish

1. For UI with a baseline, read [FIDELITY.md](../prototype/FIDELITY.md) and verify the merged result; evidence from separate ticket branches does not prove the integrated UI. Call the Skill tool with "review" on the target branch's whole diff against the spec and current evidence. Findings: fix on the target branch, review again, three rounds at most. UNVERIFIED: obtain the missing evidence before claiming completion.
2. PASS: confirm every ticket is done (GitHub: every issue closed); retain the spec, tickets, kickoff documents, baselines, and evidence per [MODES.md](../implementing/MODES.md). Delete the ticket branches.
3. Report: tickets built in merge order, conflicts and how each was decided, verification, how many tickets closed without a manual sign-off ([implementing](../implementing/SKILL.md)), anything still open.
