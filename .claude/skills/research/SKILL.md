---
name: research
description: "Answer a question the repo cannot: fan agents out to documentation, source and community, prove the claim the answer rests on with a real spike, and write .workspace/<issue-name>/research.md."
argument-hint: "<the library or technology to weigh up, or the problem you are stuck on>"
disable-model-invocation: true
---

Researching produces findings and a recommendation; it never changes code. `investigate` proves a cause inside the repo; this goes outside once that evidence is spent. Finding the answers is your job; the user answers only which candidates are worth the dig, and where the findings go.

A claim travels with its source, the version it applies to, and its date, and is checked against the versions this repo pins; short of all three it is hearsay, and hearsay never reaches the report.

This runs on web search and fetch, documentation lookup, and sub-agents (Claude Code: `WebSearch` and `WebFetch`, context7, the Agent tool). With no way to reach the web, say so plainly and stop, writing nothing.

## Frame

Read the argument, `CLAUDE.md` / `AGENTS.md` and `CONTEXT.md` where present, then the manifests and lockfiles for what this repo pins. The argument sets the mode: a technology or library names the first, a symptom or error the second; ambiguous is one question, discuss-style ([discussing](../discussing/SKILL.md)). A **candidate** is a library or approach in the first mode, a cause or a fix in the second; what the repo already runs is a candidate in both. Both modes run the phases below unchanged; only the question and the route differ.

Done when the question is one sentence, the mode is set, and the versions any answer has to hold for are listed as `name@version`, with the constraints beside them: runtime, licence, what it runs alongside.

## Scout

Wave one, wide and shallow: four agents at once, one per kind of source — the official documentation and its version matrix; the source repository, its issue tracker, changelog and releases; the community; and this codebase, for fit. Problem mode sends the same four after the symptom: the error string, the version it appears in, the version it was fixed in.

Done when every candidate any of them named is on one list with the kind that named it, the unpromising ones included, and a scout with nothing says so.

## Narrow

The list, at most three, each with its name, why it is in, and one early weakness — none found yet means the scouting was shallow, not that the candidate is clean. Then one question, discuss-style: dig into all of them, or the ones the user names. Nothing from wave two runs before that answer.

Done when the user has answered, or the list came out empty.

## Dive

Wave two, deep and narrow: one agent per chosen candidate, all at once. A lone candidate skips the fan-out, never the depth. Each brings, past the hearsay bar: what it is and what it runs on, where the documentation lives down to the page that matters, the integration shape and its best practice, the sharp edges in its issue tracker, its licence, and its maintenance signal. Problem mode: what the source reports, whether it matches this symptom, and what would prove it here.

Sources that disagree are reported as a disagreement, with both dates, never averaged. A constraint no source settles is recorded as open, and it counts against that candidate.

Done when every chosen candidate is answered constraint by constraint, and one stands ahead with the reason it does, or none does and why.

## Prove

The one claim the recommendation rests on gets a spike: a throwaway in a temp folder outside the repo, nothing installed here and nothing committed, run for real, its command and its real output kept for the report, never a predicted one. Delete the folder.

Output that contradicts the claim sends that candidate back to Narrow; it cannot be recommended. A spike that cannot run, or that was attempted and abandoned, marks the claim unverified with the reason and what was tried.

Done when the claim carries a verdict from its own output or an unverified mark, and no temp folder is left behind.

## Write

`.workspace/<issue-name>/research.md` per [RESEARCH-FORMAT.md](RESEARCH-FORMAT.md), in the user's language. You name `<issue-name>` from the question; ask nothing. A folder of that name already there: reuse it when the research belongs to that work, otherwise extend the slug until the name is free. This file is the only thing written to disk. Legacy ([MODES.md](../implementing/MODES.md)): add `.workspace/` to `.git/info/exclude` when it is not ignored.

Done when every candidate Scout named is in the file as chosen, shortlisted, or ruled out with its reason.

## Route

One question, discuss-style. What the findings leave open decides; the size of the work only sets the recommendation.

- **Settle the choice**: `/discuss-with-docs` with the path. Recommended when the decision is still the user's to make.
- **Cut it into tickets**: `/write-tickets` with the path. Recommended when nothing is left to decide.
- **Build it now**: the findings are the plan in the conversation, and the user runs `/implement`. Recommended when it is one clear change.

No candidate survived: the file is written with what was ruled out and why, and no next step is named. That is a result, not a failure.

Stop.
