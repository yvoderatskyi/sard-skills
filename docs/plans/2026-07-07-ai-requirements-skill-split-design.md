# AI Requirements Skill Split Design

## Context

The current `sard-creating-ai-requirements` skill summarizes a SARD-style AI-assisted requirements workflow from a vague stakeholder idea to an SRS. The workflow has seven artifact steps: business task, project context, functional requirements, use cases, data model, nonfunctional requirements, and SRS assembly.

## Decision

Use a hybrid split. Keep `sard-creating-ai-requirements` as the orchestration skill and create detailed subskills only for execution-heavy steps.

## Architecture

`sard-creating-ai-requirements` remains the entry point. It should:

- detect where the user is in the requirements lifecycle;
- enforce "no one-pass SRS";
- maintain the context ledger;
- require uncertainty checks and analyst review;
- route to step skills when a specific artifact needs detailed generation.

Step skills should each cover one artifact family:

- `sard-eliciting-business-requirements`
- `sard-modeling-system-context`
- `sard-writing-functional-requirements`
- `sard-modeling-use-cases`
- `sard-modeling-requirements-data`
- `sard-writing-nonfunctional-requirements`

`assembling-srs` should stay in the orchestrator for now. Split it later only if final SRS generation becomes frequent or too detailed for the orchestration skill.

## Step Skill Template

Each step skill should include:

- trigger conditions;
- required inputs;
- output format;
- prompt pattern;
- quality gate;
- traceability requirements;
- common failure modes.

## Tradeoffs

This avoids making seven skills by default, which would add discovery noise and testing burden. It also avoids growing the orchestrator into a long reference document that future agents might skim. The cost is that the workflow needs routing language in the orchestrator so agents know when to load a subskill.

## Validation

Each new skill must follow the writing-skills TDD process:

- define pressure scenarios before writing the skill;
- document baseline failures;
- write only the skill content needed to close those failures;
- verify frontmatter, discoverability, workflow gates, and traceability language.
