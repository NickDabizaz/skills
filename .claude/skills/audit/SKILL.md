---
name: audit
description: "Read a whole codebase (or one area of it) and report where it can improve: readability, structure and architecture, efficiency, current practice for its stack. Writes an HTML report in the user's language and a spec write-tickets can split."
argument-hint: "[path or area to limit the audit to]"
disable-model-invocation: true
---

Auditing produces a report and a spec; it never changes code. Facts are yours to find; the user is asked nothing until the report exists. Mode per [MODES.md](../implementing/MODES.md).

## Map

Read `CLAUDE.md` / `AGENTS.md`, `CONTEXT.md`, and `README` where present. Then build the map: folder tree, entry points, which modules import which, stack from the config files, file sizes, churn (`git log --stat`). The argument limits the map to that path. Done when every top-level folder of the scope is placed: what it is for and what depends on it.

## Read

Whole files, in this order: the largest modules, the most imported, the most changed. Done when every module on the map is read, or listed in the report as not audited.

## Judge

Four themes, in the user's interest: readability, structure and architecture, efficiency, current practice for the stack. The classics (Clean Code, The Pragmatic Programmer, Design Patterns, Code Complete, SICP, The Mythical Man-Month) and current sources are references to cite when a finding matches one; the codebase is judged against what would make it easier to change, less likely to break, and faster to run, never against a checklist. A finding is worth reporting when fixing it changes one of those three; anything a formatter or linter would fix is noise. Cut across files: a pattern repeated in five places is one finding with five locations.

Each finding gets an id (`A-01`, `A-02`, ...), a theme, an impact and an effort (high, medium, low), and the fields of [REPORT-FORMAT.md](REPORT-FORMAT.md).

## Write

Folder `.workspace/audit/`. Files there already: read, then overwrite; ids restart at `A-01`. Legacy: when `.workspace/` is not ignored, add it to `.git/info/exclude`.

1. `report.html` per [REPORT-FORMAT.md](REPORT-FORMAT.md), in the user's language.
2. `spec.md` per [SPEC-FORMAT.md](../discuss-with-docs/SPEC-FORMAT.md): goal is the audit's scope; one decision per theme naming the target state; one plan step per finding, its done-condition the proposed state, the finding's files named (the step is about them); one acceptance criterion per finding; out of scope lists what was not audited. Every id in the report is in the spec.

If the harness can show HTML to the user directly (Claude Code: the Artifact tool), show `report.html` as well; the files on disk are the deliverable. The folder stays until `implement` closes its last ticket; run `/audit` again for a fresh report.

## Done when

Both files exist and every finding in the report is one step and one criterion in the spec. Then one question, discuss-style: run `/write-tickets .workspace/audit/spec.md` now (recommended when the user came to improve, not only to look), or read the report first. Stop.
