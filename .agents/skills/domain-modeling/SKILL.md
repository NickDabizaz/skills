---
name: domain-modeling
description: "Sharpen a fuzzy domain term, or record a hard-to-reverse decision, the moment either surfaces. Reached by discussing, implementing, and investigate when a term or a decision needs settling; callable directly too."
---

Domain modeling is active, not a read: challenging a term until it is precise, or a decision until its trade-off is named, then writing it down before the conversation moves past it. Reading `CONTEXT.md` for vocabulary already settled is not this skill — every skill does that on its own.

## Sharpen a term

Fires when a term the plan depends on could mean two different things in this conversation, or the code already uses it inconsistently. Ask one question, discuss-style: state both readings, recommend one, leave room for a third. Own project: fold the settled term into `CONTEXT.md`'s Domain section — the entity, its identifier, its relations, the invariant that must hold. Legacy: state it in the conversation; there is no file here to hold it.

## Record a decision

Fires when a choice just made is hard to reverse, would surprise someone new to the repo, and carries a real trade-off — missing any one of the three, it is an ordinary decision and needs nothing here. Own project: append it to `DECISIONS.md` per [DECISIONS-FORMAT.md](DECISIONS-FORMAT.md); create the file if it does not exist yet, and append it to `.gitignore` when missing there. Legacy: state it in the conversation.

## Done when

The term or decision that triggered this is settled and, in an own project, written down. Called from another skill: return to it. Called directly: tell the user what triggered this is now resolved, and stop.
