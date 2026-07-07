# SARD Skills

Codex skill suite for AI-assisted software requirements creation, based on the SARD-style workflow from "How to write an AI technical specification from one customer phrase": https://systems.education/ai-ts

The suite treats AI as a systems-analysis partner, not an autonomous SRS writer. Requirements are created as chained artifacts with explicit context, traceability, uncertainty handling, and human review.

## Workflow

Use `creating-ai-requirements` as the entry point. It owns the context ledger and routes detailed artifact work to focused subskills.

| Step | Artifact | Skill |
| --- | --- | --- |
| 1 | Business task, questions, success criteria | `eliciting-business-requirements` |
| 2 | System boundary, actors, external systems, context flows | `modeling-system-context` |
| 3 | Functional requirements | `writing-functional-requirements` |
| 4 | Use cases and use-case diagram | `modeling-use-cases` |
| 5 | Glossary, data dictionary, CRUD, class/state diagrams | `modeling-requirements-data` |
| 6 | Measurable nonfunctional requirements | `writing-nonfunctional-requirements` |
| 7 | SRS assembly and review | `creating-ai-requirements` |

## Core Rules

- Do not generate a final SRS from one vague phrase.
- Build one artifact at a time and pass approved context forward.
- Keep a context ledger with source, decision, IDs, status, and risk.
- Mark assumptions, uncertainty, and missing sources instead of smoothing them into confident requirements.
- Preserve traceability across business goals, FRs, UCs, data entities, and NFRs.

## Skill Layout

Each skill directory contains:

- `SKILL.md`: the reusable skill instructions.
- `pressure-scenarios.md`: RED-phase failure scenarios and verification targets used to harden the skill.

`pressure-scenarios.md` files are maintenance tests, not runtime references. They document failure modes for editing and reviewing skills; normal skill execution uses `SKILL.md`.

Planning docs are in `docs/plans/`.

## Example Usage

The article's demonstration starts from this customer phrase:

```text
Help me make GPT so invisible that people stop fearing the singularity.
```

Use the skills as an artifact chain, not as one large SRS prompt.

### 1. Start the Workflow

```text
Use creating-ai-requirements.

Initial customer phrase:
"Help me make GPT so invisible that people stop fearing the singularity."

Do not generate an SRS yet. Create the context ledger and route me to the first artifact step.
```

### 2. Elicit Business Requirements

```text
Use eliciting-business-requirements.

Business idea:
"Help me make GPT so invisible that people stop fearing the singularity."

Create interview questions, a Q/A/conclusion table template, measurable success criteria, assumptions, and risks.
If information is missing, stop before drafting requirements.
```

Expected focus: goals, fear drivers, target users, acceptable autonomy, transparency, safety, escalation rules, and success metrics.

### 3. Model System Context

```text
Use modeling-system-context.

Approved context:
- Goal: AI assistance should feel predictable and non-intrusive.
- Users: everyday users, professional users, administrators.
- External systems: smart home, calendar, communication tools, professional AI agents.
- Open issue: exact autonomy boundaries are not confirmed.

Produce actors, external systems, data flows, unresolved boundary questions, and a DOT context diagram.
```

### 4. Write Functional Requirements

```text
Use writing-functional-requirements.

Input:
- Context model for Invisible AI
- Actor: everyday user
- Module: ambient assistance

Write MVP functional requirements only for this actor/module.
Use stable FR IDs, source links, priority, and testable wording.
Preserve NFR-like material in NFR Candidates.
```

Example requirement shape:

```text
FR-001 | The system shall detect when the user is asking for background assistance and respond without opening a full chat interface. | Source: BR-002, CTX-FLOW-01 | High
```

### 5. Model Use Cases

```text
Use modeling-use-cases.

Input FRs:
FR-001 ambient assistance
FR-002 explain autonomous action
FR-003 escalate uncertainty to the user

Create a UC register, FR coverage table, main/alternate/error flows, and PlantUML use-case diagram.
```

Example use-case candidates from the article's scenario include naming the AI for friendly communication, activating an autonomous alarm clock, teaching the AI a new function, generating a report by voice request, and ordering flowers for a birthday.

### 6. Model Requirements Data

```text
Use modeling-requirements-data.

Input:
- UC register and UC flows for Invisible AI
- FR IDs and context model

Create glossary, data dictionary, entity source links to UC steps, CRUD matrix, and only justified class/state diagrams.
Do not invent unsupported entities or states.
```

Possible entities might include `UserPreference`, `AutonomousAction`, `ExplanationRequest`, and `TrustSignal`, but each must trace to a UC step or requirement.

### 7. Write Nonfunctional Requirements

```text
Use writing-nonfunctional-requirements.

Input:
- Success criteria
- FRs
- Risks: user fear, over-automation, lack of transparency
- Operating context: ambient AI interactions across user devices

Create measurable NFRs with NFR IDs, category, threshold, environment, source link, and verification method.
```

Example NFR shape:

```text
NFR-001 | Usability | 90% of first-time users shall understand why an autonomous action occurred within 10 seconds of viewing its explanation. | Environment: mobile and desktop | Source: SC-003, RISK-002 | Verify by moderated usability test
```

### 8. Assemble and Review

```text
Use creating-ai-requirements.

Assemble the approved artifacts into an SRS outline.
Then review for completeness, consistency, testability, traceability, and feasibility.
Report missing sections, contradictions, unclear requirements, and open questions.
```

## Validation

Run frontmatter validation for every skill:

```bash
for f in */SKILL.md; do
  awk 'NR==1&&$0!="---"{bad=1} NR==2&&$0!~/^name: [A-Za-z0-9-]+$/{bad=1} NR==3&&$0!~/^description: Use when /{bad=1} NR==4&&$0!="---"{bad=1} END{exit bad}' "$f" || exit 1
done
```

Check orchestrator routing:

```bash
rg -n "eliciting-business-requirements|modeling-system-context|writing-functional-requirements|modeling-use-cases|modeling-requirements-data|writing-nonfunctional-requirements" creating-ai-requirements/SKILL.md
```

Check traceability language:

```bash
rg -n "source|trace|ID|context ledger|assumption|uncertainty" */SKILL.md
```
