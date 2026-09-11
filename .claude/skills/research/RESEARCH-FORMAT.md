# Research format

Path: `.workspace/<issue-name>/research.md`. `research` writes it; the user reads it. `discuss-with-docs` turns it into `spec.md` ([SPEC-FORMAT.md](../discuss-with-docs/SPEC-FORMAT.md)), and `write-tickets` splits it, reading the mode line for the ticket type.

```md
# <The question, as the user asked it>

Mode: technology | problem · Date: <YYYY-MM-DD>

An answer has to settle: <what>.

## Constraints

- **Pinned**: <name@version>, <name@version>, ...
- **<Constraint>**: <what it requires>.

## Sources swept

- **<Kind of source>**: <what it gave>. Not reached: <what, and why>.

## Candidates

- **<Name>** — chosen | shortlisted | ruled out: <reason>.

## Candidate: <name>

- **<Field>**: <finding>. [<source>, v<version>, <date>]

## Proof

- **Claim**: <the one the recommendation rests on>.
- **Spike**: `<command>` → <its real output, trimmed>.
- **Verdict**: holds | fails | unverified: <reason, and what was tried>.

## Recommendation

<Candidate>, because <reason>. This changes if <what>.

## Still open

- <What `/discuss-with-docs` has to settle>
```

Rules:

- Every claim carries its source, version and date in brackets. The date is the source's own publish or update date, `retrieved <date>` when it carries none. A line short of all three does not belong in the file.
- Version claims are stated against what **Pinned** names, never against the latest release.
- One `## Candidate: <name>` section per candidate taken forward, in the order they stand. Technology mode fills: what it is, what it runs on, docs, integration, sharp edges, licence, health. Problem mode fills: what the source reports, whether it matches our symptom, what would prove it here.
- Ruled out is append-only: a candidate leaves the shortlist by moving there with its reason, never by disappearing.
- A claim whose verdict is `fails` moves its candidate to ruled out, the spike output as its reason; the recommendation cannot name it.
- The recommendation introduces no fact: everything it rests on is already a cited line above it.
- The user's language throughout. Technical terms, API names and quoted sources stay as they are.
