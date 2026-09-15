# Shortcut markers

A comment left where a real constraint forced a corner cut on purpose — not a bug, not a TODO, a decision made and recorded. Written once, at the cut, in whatever comment syntax the file uses:

```
<comment-prefix> shortcut: <what was cut short>, revisit when <the trigger>
```

Both halves are required. Without a trigger, a deliberate cut can't be told apart from one nobody will ever come back to.

Examples:

```
// shortcut: single global lock instead of per-account locks, revisit when write throughput becomes measurable
# shortcut: linear scan instead of an index, revisit when this list passes a few thousand rows
-- shortcut: fixed page size of 50, revisit when a caller needs to page past it
```

`find-shortcuts` reads every marker in the repo; one with no clear trigger is flagged there as likely to rot into a permanent shortcut nobody chose.
