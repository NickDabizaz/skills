---
name: find-shortcuts
description: "Scan the repo for shortcut markers implement left behind and report them as a ledger, flagging any with no clear revisit trigger. Use when the user asks about tech debt, what was deferred or simplified, what's safe to revisit, wants a pre-release check, or after a large implement-all batch closes."
---

Every marker names its own trigger; this only collects and flags the ones that don't. Read [SHORTCUT-FORMAT.md](../implementing/SHORTCUT-FORMAT.md) for the marker's shape.

## Scan

`grep -rn 'shortcut:' .`, skipping `.git`, build output, and dependency folders (`node_modules`, `vendor`, `.venv`, and their equivalents). Each hit is one ledger row.

## Report

One row per marker, grouped by file:

`<file>:<line> — <what was cut short>. revisit when: <the trigger>.`

A marker with nothing after "revisit when" gets `no-trigger` appended — that one is likely to rot into a permanent shortcut nobody chose.

End with `<N> shortcuts, <M> with no trigger.` None found: `No shortcuts marked.`

## Done when

Every marker in the repo is one row. Reads and reports only; fixing or removing a shortcut is implement's job, on a ticket the user decides is worth it.
