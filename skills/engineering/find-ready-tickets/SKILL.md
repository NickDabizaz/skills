---
name: find-ready-tickets
description: "Finds tickets whose blocking work is done and shows what can be implemented next."
argument-hint: "[issue or project]"
disable-model-invocation: true
---

# Find Ready Tickets

Read `CONTEXT.md` for the tracker backend and inspect ticket state from that backend. A ticket is ready only when its blockers are done, required spec/design decisions are settled, and no user action still gates its start. Do not use a stale local status mirror when GitHub is the backend. Show title, work type, owner if assigned, blockers cleared, and the outcome; group parallel-ready tickets together. If none are ready, identify the exact blocker or decision.

Done when the user can choose an unblocked ticket without opening every issue. Offer `implement` with the selected ticket reference, or the concrete preceding skill needed to unblock it.
