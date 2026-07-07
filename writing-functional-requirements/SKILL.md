---
name: writing-functional-requirements
description: Use when writing or checking traceable functional requirements, FR lists, priorities, grouping, or acceptance-ready statements
---

# Writing Functional Requirements

Use this skill to turn approved business context, system context, use-case notes, or stakeholder statements into traceable functional requirements. Keep requirements focused on observable system behavior.

## Required Inputs

Use available source/context items such as stakeholder quotes, interview answers, business requirement IDs, context-model rows, use-case IDs, assumptions, or decisions. If source context is missing for a provisional FR, keep the trace field populated as `Missing - open issue OI-###` and list the open issue in Notes.

## Output Format

Group FRs by the most useful lens for the work:

- Module when the system boundary or product areas are clear.
- Process when the workflow is the main organizing concept.
- Role when actor responsibilities differ materially.

Within each group, use this table:

| FR ID | Requirement | Source/context link | Priority | Notes |
| --- | --- | --- | --- | --- |

If source material contains nonfunctional requirements or quality attributes, preserve them outside the FR table:

| NFR Candidate ID | Statement | Source/context link | Suggested route | Notes |
| --- | --- | --- | --- | --- |

## FR Rules

- Use stable FR IDs that do not change between revisions, such as `FR-001`, `FR-002`, or module-prefixed IDs when already established.
- Give every FR exactly one primary source/context link and add secondary links in Notes when useful. For provisional FRs without a known source, use `Missing - open issue OI-###`; do not leave the field blank.
- Set priority for every FR with a simple scheme such as `Must`, `Should`, `Could`, or the project's existing priority labels.
- Write testable wording: one observable behavior per FR, clear trigger or condition, actor/system action, and expected result.
- Keep FRs functional: describe what the system must do, validate, calculate, display, store, send, receive, restrict, or log.
- Keep NFR-like source material out of the FR table and preserve it in `NFR Candidates` by default so source context and routing information remain visible.
- Preserve assumptions and uncertainty in Notes instead of rewriting them as confirmed requirements.

## Testability Check

Before returning, revise or flag any FR that uses vague wording such as `easy`, `fast`, `secure`, `robust`, `intuitive`, `support`, `manage`, `appropriate`, or `as needed` without a concrete behavior or measurable condition.

A testable FR should be readable as an acceptance test:

```text
Given <condition/source context>, when <actor or event> occurs, the system shall <observable behavior/result>.
```

Do not force every requirement into Given/When/Then syntax, but ensure each one can be tested that way.

## Quality Gate

Before returning, verify:

- Every FR has a stable FR ID.
- Every FR has a source/context link or a `Missing - open issue OI-###` placeholder.
- FRs are grouped by module, process, or role.
- Every FR has a priority.
- Every FR is testable and describes observable functional behavior.
- Nonfunctional requirements are excluded from the FR table and preserved in `NFR Candidates` with source/context links.
