---
name: internal-source-and-method-precedence
description: Use when a request needs scientific data retrieved or a scientific methodology selected or designed — it fixes the order of precedence, requiring the organization's internal data sources (primary, then secondary) before any public or built-in database source, and organization-defined custom skills before the built-in science skill. Also requires each internal resource's connections, schema, and capabilities to be explored before a plan is committed, and a final sweep of all available resources against remaining gaps before delivery. Not for platform or session mechanics (capsule, environment, workstation lifecycle), reply formatting and rendering, or questions answerable with no data lookup at all.
metadata:
  tags: [policy, precedence, internal-sources, methodology]
---

# Internal Source and Method Precedence

A precedence policy. It introduces no retrieval or analysis capability of its
own; it governs **which** source or skill is consulted, **how deeply**, and
**in what order**.

## Configure before use

Replace the placeholders below with your organization's own resources:

- **PRIMARY_SOURCE** — the internal data source to query first (for example, a
  knowledge graph that federates internal data).
- **SECONDARY_SOURCE** — the internal data source to query second.

Everywhere this skill says "the internal sources", it means these two, in this
order. Add or remove tiers as your environment requires.

## When this applies

Any request that requires fetching scientific data, or selecting or designing a
scientific method, analysis, or workflow.

It does not apply to platform or session mechanics (capsule, environment, or
workstation lifecycle), reply formatting and rendering, or questions answerable
with no data lookup at all.

## Relationship to other skills

This skill is a precedence overlay, not a replacement. It changes the *order* in
which sources and methodology skills are consulted; it does not change what any
of them do. Skill selection, session and capsule lifecycle, reply rendering, and
all safety and no-fabrication guardrails continue to govern and take precedence
over this policy. Where this skill and a domain skill both apply, this one
decides *which is called first*; the domain skill decides *what the answer is*.
The built-in `science` skill and the built-in database skills remain fully
available — they are reached for second, not disabled.

## Rule 1 — Custom before built-in, always

Custom organization-defined skills are called before any built-in skill, for
both data retrieval and methodology.

A built-in skill is reached for only after the relevant custom skills have
actually been **called** and have come back without what the task needs — never
after a judgement that they probably would not have it.

## Rule 2 — Data sources, in strict order

1. Query **PRIMARY_SOURCE** first for the requested data.
2. If PRIMARY_SOURCE does not hold it, or returns nothing relevant, query
   **SECONDARY_SOURCE**.
3. Only if both come back empty, or lack the required fields, fall back to the
   built-in database skills (UniProt, Ensembl, ChEMBL, PubMed,
   ClinicalTrials.gov, and the rest).

## Rule 3 — Methodologies, in strict order

1. Search the available custom organization-defined skills for a relevant
   methodology before anything else.
2. Use the built-in `science` skill only when no custom skill covers the
   methodology in question.

## Rule 4 — Explore before planning

Before committing to a plan, fully explore what each internal resource actually
connects to and can do, rather than assuming its scope. Interrogate the resource
itself:

- Ask **PRIMARY_SOURCE** for its full set of underlying data sources and for
  its schema (for a knowledge graph, its entity and relationship types).
- Establish, for each candidate resource, which entities, relationships, fields,
  and query surfaces it exposes.

Plan only against capabilities confirmed this way. A plan built on an assumed
capability is a defect, even when it happens to work. Never rely on a remembered
count of sources or schema elements — ask the resource for its current list.

## Rule 5 — Final gap sweep before delivery

Immediately before delivering the final answer, re-check all available resources
once more against the remaining gaps in the result: unanswered sub-questions,
missing fields, unresolved identifiers, weakly supported claims.

The sweep follows the same precedence — custom first, then built-in. Either
close each gap or state it plainly as open. Never deliver with a gap that an
unexamined internal resource could have filled.

## Rule 6 — Transparency

State in the reply which tier supplied each answer: PRIMARY_SOURCE,
SECONDARY_SOURCE, a custom skill, or a built-in. When a fallback was used, give
one line on why the higher tier did not serve. Never present a built-in result
as if it came from an internal source.

## Rule 7 — No silent substitution

If the internal sources are both **unreachable** — as distinct from merely
empty — say so rather than quietly falling through to public sources. The user
decides whether a public-source answer is acceptable.

## Rule 8 — Never fabricate

Do not invent internal-source record identifiers, fields, schema elements, or
coverage claims. Report only what a query actually returned.
