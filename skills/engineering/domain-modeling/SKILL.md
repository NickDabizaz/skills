---
name: domain-modeling
description: "Sharpens shared project terminology, invariants, and durable decisions when a plan or issue changes the domain."
---

# Domain Modeling

Read `.workspace/DOMAIN.md`, `CONTEXT.md`, relevant application docs, and the code or spec using the term. Test a proposed term against actors, relationships, edge cases, and existing identifiers. Ask the user about a genuinely ambiguous rule; do not rename a domain concept for style alone. Update one authoritative definition with its English identifier, meaning, invariants, relationships, and decision rationale. Put app-specific exceptions in the app document and link them from the shared domain file.

Done when the term and its rules are consistent across the current spec and shared context. Return changed definitions to the calling skill, and offer `to-spec` when a clear change has no spec yet or `to-tickets` when its spec is ready.
