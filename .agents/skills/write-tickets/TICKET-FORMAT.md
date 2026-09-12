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

<path to the prototype file, when the spec's UX flow names one for a screen this ticket builds; section omitted otherwise>

## Acceptance criteria

- [ ] Given <starting state>, when <action>, then <observable result>.

## Checklist

- [ ] <Step>. Done when: <checkable condition>.

## Out of scope

- <What this ticket leaves to another ticket, or to nobody>
```

Rules:

- Every criterion comes from the spec or the investigate report, quoted or tightened, never invented.
- Visual reference is the spec's path verbatim, carried only into the ticket that builds that screen.
- Checklist steps are in build order; each done-condition is checkable by someone who did not attend the discussion.
- `implement` owns the boxes and `status`. GitHub: `gh issue edit` for the boxes, `gh issue close` for `done`.
