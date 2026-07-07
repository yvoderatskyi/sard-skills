---
name: sard-eliciting-business-requirements
description: Use when clarifying vague business ideas, stakeholder requests, goals, risks, assumptions, or success criteria before requirements
---

# Eliciting Business Requirements

Use this skill to turn uncertain business input into validated business requirements. Do not generate final requirements from a vague phrase until the missing business context is exposed.

## Required Extraction

Extract and maintain these fields:

| Field | What to capture |
| --- | --- |
| Business problem | The pain, opportunity, or decision the work addresses |
| Stakeholders | Decision makers, users, operators, affected teams, and unavailable stakeholder groups |
| Goals | Desired business outcomes, not solution features |
| Constraints | Fixed deadlines, systems, policies, budgets, legal limits, and operating boundaries |
| Success criteria | Measurable outcomes that define whether the business goal was achieved |
| Assumptions | Any invented, inferred, simulated, or unconfirmed detail |
| Risks | Ambiguity, missing stakeholder access, contradictory evidence, feasibility concerns, and validation gaps |

## Clarification First

Before generating requirements, ask focused clarification questions when any required extraction field is missing, vague, or uncertain. Prefer small question sets that can change the requirements:

| Topic | Example questions |
| --- | --- |
| Problem | What business pain should this solve, and who feels it today? |
| Stakeholder | Who approves success, who uses the result, and who may object? |
| Goal | Which measurable outcome matters most: cost, revenue, risk, speed, quality, satisfaction, or compliance? |
| Constraint | What deadlines, systems, policies, budgets, or legal limits are already fixed? |
| Risk | What could make these requirements wrong or unusable? |

If stakeholder access is limited, say so explicitly and continue with provisional analysis only. Mark every inferred answer as an assumption and list what must be confirmed later.

If required fields are materially missing, stop after Known Context, Focused Questions, and Assumptions and Risks. Do not draft requirements until answers are provided or the user explicitly authorizes provisional requirements.

## Output Format

Produce these sections in order. Use the full format, including Draft Business Requirements, only after answers are provided or the user explicitly authorizes provisional requirements:

1. Known Context
2. Focused Questions
3. Q/A/Conclusion Table
4. Draft Business Requirements
5. Measurable Success Criteria
6. Assumptions and Risks

Use this table for answers and conclusions:

| ID | Question | Answer or assumption | Conclusion | Confidence | Follow-up |
| --- | --- | --- | --- | --- | --- |

Use `Answer or assumption` to distinguish confirmed stakeholder input from invented details. Conclusions must trace to an answer, source note, or labeled assumption.
Keep the trace chain visible from question to conclusion to requirement.

## Business Requirements Rules

- Write requirements only after questions and the Q/A/conclusion table.
- Do not draft requirements from vague input when material fields are missing unless the user explicitly authorizes provisional requirements.
- Keep requirements at the business level: outcomes, policies, decisions, constraints, and user/business capabilities.
- Label likely goals as assumptions until confirmed.
- Each requirement must link to a conclusion ID.
- Each success criterion must be measurable with a metric, target, timeframe, and source or assumption.
- Preserve uncertainty rather than smoothing it into confident language.

## Minimal Requirement Template

| ID | Requirement | Source conclusion | Priority | Uncertainty |
| --- | --- | --- | --- | --- |

## Success Criteria Template

| ID | Metric | Target | Timeframe | Source or assumption |
| --- | --- | --- | --- | --- |

## Quality Check

Before returning, verify:

- Business problem, stakeholder groups, goals, constraints, success criteria, assumptions, and risks are present.
- Clarification questions appear before draft requirements.
- Q/A/conclusion table is present.
- Success criteria are measurable.
- Invented details are marked as assumptions.
