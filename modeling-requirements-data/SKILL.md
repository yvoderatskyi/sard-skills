---
name: modeling-requirements-data
description: Use when modeling requirements data, glossaries, data dictionaries, CRUD matrices, entity traceability, or justified class/state diagrams
---

# Modeling Requirements Data

Use this skill to turn approved use cases and requirements context into traceable requirements data artifacts. Do not invent entities, attributes, or states that are not supported by use-case steps, FRs, business rules, stakeholder terms, or explicit assumptions.

## Required Inputs

Use available UC details, FRs, actor model, business rules, glossary terms, workflow notes, and approved assumptions. If a data element lacks support, list it as an unresolved data question instead of filling it in.

## Required Output

Produce these sections in order:

1. Glossary
2. Data Dictionary
3. Entity Source Links
4. CRUD Matrix by Actor/Use Case
5. Diagrams, if justified
6. Unresolved Data Questions

## Glossary

Define all domain terms used in entities, attributes, statuses, identifiers, business rules, and diagrams.

| Term | Definition | Source |
| --- | --- | --- |

Rules:
- Use stakeholder or requirements wording where available.
- Do not leave key entity, attribute, status, or actor terms undefined.
- If a definition is uncertain, mark the source as an assumption or unresolved question.

## Data Dictionary

Document every supported entity and attribute.

| Entity | Attribute | Type/format | Required? | Allowed values/rules | Source |
| --- | --- | --- | --- | --- | --- |

Rules:
- Every entity and attribute must cite a UC step, FR, business rule, stakeholder statement, or approved assumption.
- Prefer requirement-level types and constraints over implementation types.
- Exclude implementation-only fields unless they are required by a UC, audit rule, integration, or business constraint.

## Entity Source Links

Show why each entity exists.

| Entity | Supporting UC step(s) | Supporting FR/rule/source | Notes |
| --- | --- | --- | --- |

Rules:
- Link each entity to one or more UC steps using stable IDs such as `UC-001 step 3`.
- If an entity cannot be linked to a UC step, mark it as `unsupported` and move it to unresolved questions unless another approved source explicitly justifies it.
- If an attribute, relationship, state, or transition lacks support, remove it or move it to unresolved questions.
- Route convenience entities for likely implementation needs to unresolved questions unless they have a requirement source.

## CRUD Matrix by Actor/Use Case

Account for create, read, update, and delete/archive behavior by actor and use case.

| Actor | Use case | Entity | Create | Read | Update | Delete/archive | Source |
| --- | --- | --- | --- | --- | --- | --- | --- |

Rules:
- Use `yes`, `no`, or `unclear`.
- Cover every entity from the data dictionary across relevant actors and use cases.
- Treat missing delete/archive, retention, and correction rules as data questions, not silent omissions.
- If an entity has no CRUD coverage, either remove it as unsupported or list the missing coverage question.

## Diagrams, If Justified

Create a class diagram or state diagram only when it clarifies reviewed requirements.

Rules:
- Use a class diagram when relationships, multiplicity, ownership, or composition are important to validate.
- Use a state diagram when lifecycle states, transitions, guards, or terminal outcomes are important to validate.
- Do not include class or state diagrams as decoration.
- Every diagram entity, relationship, state, and transition must trace to a UC step, FR, rule, or data question.
- Do not invent relationships, lifecycle states, guards, or transitions to make a class diagram or state diagram look complete.

## Unresolved Data Questions

List every missing or conflicting data decision.

| Question ID | Location | Question | Blocks | Send back to |
| --- | --- | --- | --- | --- |

`Send back to` should name the likely source to clarify, such as `use case`, `FR`, `business rule`, `stakeholder`, `integration contract`, or `retention policy`.

## Quality Gate

Before returning, verify:

- Glossary covers all domain terms used in the data dictionary, CRUD matrix, and diagrams.
- Data dictionary includes every supported entity and attribute, with sources.
- Every entity has source links to UC steps or an explicit approved non-UC source.
- CRUD matrix accounts for each entity by relevant actor/use case.
- Missing create, read, update, delete/archive, retention, correction, and ownership rules are listed as unresolved data questions.
- Class diagram and state diagram outputs are included only when justified by requirements complexity.
- Unsupported entities, attributes, relationships, states, and transitions are removed or routed to unresolved data questions.
