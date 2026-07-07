---
name: creating-ai-requirements
description: Use when turning vague product ideas or stakeholder requests into traceable requirements, SRS artifacts, or requirements-analysis workflows
---

# Creating AI Requirements

## Overview

Use AI as a systems-analysis partner, not an autonomous SRS writer. Convert a vague idea into requirements through chained artifacts, a trace chain, and human review.

Based on the SARD-style article "How to write an AI technical specification from one customer phrase" at https://systems.education/ai-ts.

## When to Use

- Stakeholder gives a vague product idea or problem, not requirements.
- Need AI-assisted SRS, FR/NFR, use cases, context diagrams, UML, data model, CRUD matrix, or RTM.
- Need requirements under high uncertainty, limited stakeholder access, or presales speed.
- Do not use for coding tasks, implementation plans, or architecture decisions without first producing and validating requirements.

## Core Rule

Never generate the final SRS in one pass. Build one artifact at a time, feed approved context forward, and revise earlier artifacts when later work reveals contradictions.

## Workflow

| Step | Input | Output | Gate |
| --- | --- | --- | --- |
| 1. Business task | phrase/problem | questions, Q/A/conclusion table, success criteria | measurable goals; assumptions marked |
| 2. Project context | approved step 1 | actors, external systems, data flows, DOT context diagram | explicit boundary |
| 3. Functional requirements | Context description | coded FR grouped by module/process/role | Each FR is clear, testable, prioritized |
| 4. Use cases | FR list | UC register, flows, PlantUML use-case diagram | UC references FR IDs |
| 5. Data model | UC steps | glossary, data dictionary, CRUD, class/state diagrams | entities cover UC data |
| 6. Nonfunctional requirements | success criteria, FR, constraints | measurable NFR by environment, external quality, usage quality | metrics and thresholds |
| 7. SRS assembly | all approved artifacts | SRS plus review report | Completeness, consistency, feasibility checked |

## Step Skill Routing

The orchestrator keeps ownership of the context ledger and routes detailed artifact work to subskills.

| Need | Use |
| --- | --- |
| clarify business task, interview questions, goals | `eliciting-business-requirements` |
| system boundary, actors, external systems, context diagram | `modeling-system-context` |
| FR list, modules, priorities, acceptance-ready requirements | `writing-functional-requirements` |
| UC register, main/alternate/error flows, use-case diagram | `modeling-use-cases` |
| glossary, data dictionary, CRUD matrix, class/state diagrams | `modeling-requirements-data` |
| measurable quality attributes, constraints, NFR thresholds | `writing-nonfunctional-requirements` |

## Required Context Ledger

Maintain this ledger after every step and pass relevant rows forward:

| Field | Meaning |
| --- | --- |
| `source` | quote, interview answer, artifact ID, or assumption |
| `decision` | requirement, term, actor, entity, constraint, or question |
| `ids` | linked goal/FR/UC/entity/NFR identifiers |
| `status` | proposed, approved, rejected, changed |
| `risk` | ambiguity, contradiction, missing stakeholder confirmation |

The trace chain is the linked path from source material to goal, FR, UC, entity, NFR, and SRS section. Keep it intact across every artifact.

## Prompt Pattern

Use this structure for every artifact prompt:

```text
Role: Act as an experienced systems analyst.
Task: Produce only [artifact] for [system/module/role].
Approved context: [ledger rows + previous approved artifact]
Rules: use these IDs, output format, naming rules, priority scheme, and trace links.
Uncertainty check: if required information is missing, either ask focused clarification questions or generate a clearly provisional artifact with unresolved questions when the active step allows that.
Quality gate: verify completeness, consistency, testability, and trace chain.
Output: [exact table, Markdown, DOT, PlantUML, or SRS section only].
```

## Example

Input idea: "Help clinics reduce missed appointments."

Step 1 output is not FRs. First produce interview questions and measurable success criteria: reduction target, appointment types, channels, cancellation policy, user groups, legal constraints, integrations. Mark invented detail as an assumption.

## Quality Checks

| Check | Pass condition |
| --- | --- |
| Completeness | goals, actors, FR, UC, data, NFR, constraints, glossary |
| Trace chain | FR -> source; UC -> FR; entity -> UC; NFR -> success criterion, constraint, risk, goal, use-case context, stakeholder statement, or approved assumption |
| Testability | vague terms have measurable thresholds |
| Consistency | names, IDs, actors, modules, entities match |
| Feasibility | risks, dependencies, boundaries, open questions included |

## Common Mistakes

| Mistake | Fix |
| --- | --- |
| Generating a polished SRS from one vague sentence | Start with interview questions and success criteria |
| Treating simulated stakeholder answers as truth | Label them training assumptions; confirm with a real stakeholder |
| Losing context between prompts | Use the context ledger and pass approved artifacts forward |
| Creating unlinked diagrams and tables | Require IDs and references in every artifact |
| Accepting AI text as final | Analyst reviews and corrects completeness, contradictions, and feasibility |
