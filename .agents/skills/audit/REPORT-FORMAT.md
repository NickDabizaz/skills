# Audit report format

Path: `.issues/audit/report.html`. `audit` writes it; the user reads it. One self-contained file: CSS and JS inline, no build step, no network dependency, opens by double-click, readable at phone and desktop widths.

## Language

The user's language throughout. Plain words: a technical term gets a one-clause explanation the first time it appears ("coupling, yaitu seberapa banyak satu bagian bergantung pada bagian lain"). Every finding shows code, never only prose: the reader should be able to point at the line and picture the change. The labels below are rendered in that language too.

## Sections, in order

1. **Header**: project name, date, scope audited, and a list of what was not audited with the reason.
2. **Health summary**: one row per theme (readability, structure and architecture, efficiency, current practice) with the count of findings by impact and one sentence on the state of that theme.
3. **Architecture map**: the folders and modules of the scope and the dependencies between them, as an inline SVG or a nested list, with one line per node on what it is for. Cycles and modules everything depends on are marked.
4. **Findings**: grouped by theme, ordered by impact then effort. Filters by theme and impact in plain JS.
5. **Suggested order**: the findings as a short sequence, high impact and low effort first, with one line on why each comes where it does.

## A finding

```
A-07 · <title in plain words>                      impact: high · effort: low
Theme: <one of the four>
Where: <file:line>, <file:line>, ...              (every location, not a sample)

What is wrong: <two or three sentences a beginner follows>
Why it matters: <what it costs now: bugs, slow changes, slow runtime>

Now:                                               Proposed:
<code as it is, trimmed to the point>              <the same code after the change>

Options:
A. <option> — Gain: <gain>. Cost: <cost, in plain words>.
B. <option> — Gain: ... Cost: ...
➡️ Recommended: <letter>, <reason>.

Reference: <book, chapter or principle; or a current source; or none>
```

Rules:

- Two or three options per finding, one recommended; an option's cost is stated as concretely as its gain (time, risk, what else has to change).
- Impact is what fixing changes for the user; effort is how much code moves. Both qualitative, no scores.
- A finding with no code to show is a theme-level remark, and lives in the health summary instead.
