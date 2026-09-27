---
name: to-tickets
description: "Splits an approved issue spec into detailed work-owned tickets with real blocking dependencies."
argument-hint: "<issue spec>"
disable-model-invocation: true
---

# To Tickets

Read [TICKET-FORMAT.md](TICKET-FORMAT.md), the approved `spec.md`, `CONTEXT.md`, and any approved design brief or prototype. Draft the smallest set of backend, frontend, infrastructure, and testing tickets that covers the spec. Separate tickets by actual work ownership, but keep each outcome demonstrable through its acceptance checks. A testing ticket owns cross-layer or selected automation scenarios not owned by implementation tickets. Map every spec criterion and scenario to an owner ticket and verify blockers form no cycle.

Show the proposed split, each ticket's deliverable and blockers, then reconcile the user's changes before publication. Local tracker: create one Markdown file per ticket in `tickets/`. GitHub tracker: create one GitHub issue per ticket with parent and blocking references; keep only a link index in local `tickets/`. If the spec has not been pushed, name that as a remote handoff prerequisite rather than claiming remote agents can read it. Ticket prose follows the user's input language; identifiers remain English.

Done when the ticket graph is acyclic, all accepted scope is assigned, test choices and prototype baseline survive the split, and ticket links resolve. Offer `find-ready-tickets` or `implement` for the first unblocked ticket.
