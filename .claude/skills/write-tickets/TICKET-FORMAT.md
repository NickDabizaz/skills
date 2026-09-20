# Ticket format

Local backend: `.workspace/<issue-name>/tickets/<nn>-<slug>.md`, beside the spec, one file per ticket, this whole document. GitHub backend: the body below the frontmatter is the issue body; the issue number is `id`, the labels are `type`, `issue:<issue-name>`, and, while being built, `in-progress`; `status` is `done` when the issue is closed, `todo` otherwise.

```md
---
id: 03
title: <short, imperative>
type: feature | bug | chore
status: todo | in-progress | done
blocked-by: [01, 02]
---

## Goal

One paragraph: what this ticket delivers and why, in the spec's words.

## Visual reference

<approved baseline path and version; link to the spec screen contract; applicable viewports/states and approved deviations; omit only when no reference applies>

## Acceptance criteria

- [ ] Given <starting state>, when <action>, then <observable result>.

## Checklist

- [ ] <Step>. Done when: <checkable condition>.

## Out of scope

- <What this ticket leaves to another ticket, or to nobody>
```

Rules:

- Every criterion comes from the spec or the investigate report, quoted or tightened, never invented.
- `<slug>` is the ticket's English identifier — own project: the `CONTEXT.md` Domain entity it belongs to, or the nearest English rendering when none fits. `title` may stay in the spec's language; the slug never does.
- Visual reference carries the spec's baseline identity verbatim into every ticket affecting that screen. Read [FIDELITY.md](../prototype/FIDELITY.md) for contract preservation and evidence; link the inventory instead of paraphrasing it.
- Checklist steps are in build order; each done-condition is checkable by someone who did not attend the discussion.
- `implement` owns the boxes and `status`. GitHub: `gh issue edit` for the boxes, `gh issue close` for `done`.
