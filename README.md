# SRS Skills

Codex skill suite for AI-assisted software requirements creation, based on the SRS-style workflow from "How to write an AI technical specification from one customer phrase": https://systems.education/ai-ts

The suite treats AI as a systems-analysis partner, not an autonomous SRS writer. Requirements are created as chained artifacts with explicit context, traceability, uncertainty handling, and human review.

## Workflow

Use `srs-ai-creating-ai-requirements` as the entry point. It owns the context ledger and routes detailed artifact work to focused subskills.

| Step | Artifact | Skill |
| --- | --- | --- |
| 1 | Business task, questions, success criteria | `srs-ai-eliciting-business-requirements` |
| 2 | System boundary, actors, external systems, context flows | `srs-ai-modeling-system-context` |
| 3 | Functional requirements | `srs-ai-writing-functional-requirements` |
| 4 | Use cases and use-case diagram | `srs-ai-modeling-use-cases` |
| 5 | Glossary, data dictionary, CRUD, class/state diagrams | `srs-ai-modeling-requirements-data` |
| 6 | Measurable nonfunctional requirements | `srs-ai-writing-nonfunctional-requirements` |
| 7 | SRS assembly and review | `srs-ai-creating-ai-requirements` |

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

The article's GPT invisibility example is documented in [docs/examples/article-workflow.md](docs/examples/article-workflow.md). Keep the README short and use that file for the full walk-through.

## Validation

Run frontmatter validation for every skill:

```bash
for f in */SKILL.md; do
  awk 'NR==1&&$0!="---"{bad=1} NR==2&&$0!~/^name: [A-Za-z0-9-]+$/{bad=1} NR==3&&$0!~/^description: Use when /{bad=1} NR==4&&$0!="---"{bad=1} END{exit bad}' "$f" || exit 1
done
```

Check orchestrator routing:

```bash
rg -n "srs-ai-eliciting-business-requirements|srs-ai-modeling-system-context|srs-ai-writing-functional-requirements|srs-ai-modeling-use-cases|srs-ai-modeling-requirements-data|srs-ai-writing-nonfunctional-requirements" srs-ai-creating-ai-requirements/SKILL.md
```

Check traceability language:

```bash
rg -n "source|trace|ID|context ledger|assumption|uncertainty" */SKILL.md
```
