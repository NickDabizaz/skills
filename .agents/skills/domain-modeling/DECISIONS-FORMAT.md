# DECISIONS.md format

Path: repo root, gitignored, own project only ([MODES.md](../implementing/MODES.md)); its presence changes no mode. `domain-modeling` appends to it; nothing reads it back except a human skimming history.

```md
# Decisions

## <Decision title> — <date>

**Context**: <the fork in the road, or the term that forced it>
**Decision**: <what was chosen>
**Why**: <the reason, and what was ruled out>
**Trade-off**: <what this costs, on purpose>
```

Rules:

- Append-only, oldest first. A past entry's **Decision** is never edited; a reversal is a new entry that names the one it reverses.
- Worth an entry only when all three hold: hard to reverse, would surprise someone new to the repo, and carries a real trade-off. Missing one, it's a normal decision and needs nothing here.
