---
name: review
description: "Review a diff on three axes: Spec (does it match the agreed plan and, in an own project, is each criterion tested), Standards (is it consistent with the repo's conventions and the surrounding code), and Logic & Security (bugs, unhandled edge cases, affected callers, vulnerabilities); a fourth, UI/UX (states, feedback, design rules and patterns, duplicated surfaces, accessibility basics), when the diff touches UI. Use when implement finishes, or when the user asks to review changes, a branch, or a PR."
---

Review the changes against the plan and the codebase, then report. Review reports; fixing belongs to implement or the user. Mode per [MODES.md](../implementing/MODES.md).

## Inputs

- **Diff**: what the user or implement points at. Default: uncommitted changes plus commits ahead of the default branch. An empty diff stops the review here.
- **Plan**: the ticket and spec given, else the `.issues/*/spec.md` matching the work, else the plan agreed in the conversation. With no plan, the Spec axis reports "no plan available" and the other two axes still run.
- **Standards**: `CLAUDE.md` / `AGENTS.md`, `CONTEXT.md`, any documented coding standards, and the code neighbouring each change, in the mode's priority: documented conventions first, then what the existing code already does.
- **Design**: `DESIGN.md` where it exists ([DESIGN-FORMAT.md](../setup-new-project/DESIGN-FORMAT.md)), otherwise the components and theme already in the code; and the plan's UX flow.

## The axes

Three axes always; UI/UX joins them when the diff changes anything the user sees (templates, components, styles, copy). Run each axis over the whole diff. If the harness supports sub-agents, run the axes in parallel so none colours another; otherwise run them one after another.

**Spec**: does the diff do what the plan says? Report requirements missing or partial, behaviour nobody asked for, and requirements that look done but are wrong. Quote the plan line for each. Own project with `tests: acceptance`: each acceptance criterion has a test that passes with the change and fails without it; a criterion without one is a finding. Legacy, or `tests: none`: the absence of new tests is never a finding.

**Standards**: does the diff look like it belongs in this codebase? Report naming, structure, error handling, or test style that differs from neighbouring code; documented conventions broken; and existing helpers or patterns reinvented instead of reused. Skip anything a linter or formatter already enforces.

**Logic & Security**: does the diff hold up? Report wrong logic; unhandled edge cases (empty, null, boundary, concurrent, failure paths); callers of a changed function, type, endpoint, or schema that the diff leaves unadjusted; input crossing a trust boundary without validation; injection; secrets or sensitive data exposed; missing auth or permission checks; resources never released.

**UI/UX**: does the diff hold up for the user? Report a screen in the UX flow missing an empty, loading, error, or success state; an action with no visible feedback; an interactive control missing its hover, focus-visible, active, disabled, or loading state; motion or elevation that is not a `DESIGN.md` token; tokens, components, or Patterns the diff departs from (legacy: neighbouring components); a component built where an existing one fits, and two components carrying one entity's fields; a control without a label, a focus state, or readable contrast.

Report only what is worth a fix. A nitpick the user would ignore is noise.

## Report

Order findings by severity: critical, then major, then minor. Each finding:

```
[<severity>] <file>:<line> — <what is wrong>
Why: <consequence>
Fix: <the concrete change>
```

Group findings under `## Spec`, `## Standards`, `## Logic & Security`, and `## UI/UX` when that axis ran. Keep the axes separate: a change can pass one and fail another, and merging them lets one axis hide the other.

End with one line per axis (count and worst finding) and a verdict: **PASS** when there are no findings, otherwise **NEEDS FIXES**.
