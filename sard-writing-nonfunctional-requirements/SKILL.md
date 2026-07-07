---
name: sard-writing-nonfunctional-requirements
description: Use when writing or checking measurable nonfunctional requirements, NFR thresholds, quality attributes, constraints, SLAs, or SLOs
---

# Writing Nonfunctional Requirements

Use this skill to turn approved goals, constraints, risks, operating context, and usage expectations into measurable nonfunctional requirements. Do not accept vague quality words as requirements.
Keep the trace chain visible from goal, constraint, or risk to each NFR and verification method.

## Required Inputs

Use available success criteria, business goals, constraints, risks, compliance notes, architecture limits, use-case volumes, operating environments, stakeholder statements, and approved assumption IDs/references. If the source for an NFR is missing, keep it provisional with `Missing - open issue OI-###`.

## Output Format

Group NFRs by quality category or by the project's existing structure.

| NFR ID | Quality category | Requirement | Threshold/metric | Operating context/environment | Source link | Verification method | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |

## NFR Rules

- Use stable NFR IDs, such as `NFR-001`, `NFR-002`, or category-prefixed IDs when already established.
- Assign a quality category to every NFR, such as performance, security, availability, usability, privacy, compliance, interoperability, maintainability, observability, recoverability, or scalability.
- Include a measurable threshold for every NFR. The threshold must define pass/fail using a metric, limit, percentile, time window, volume, rate, score, standard, or audit criterion.
- State the operating context/environment where the threshold applies, including relevant users, load, device, network, deployment, region, vendor, regulatory boundary, or peak/normal condition.
- Give every NFR a source link to a success criterion, constraint, risk, use-case context, business goal, stakeholder statement, or approved assumption ID/reference.
- Define a verification method that can prove the threshold, such as load test, security test, penetration test, accessibility audit, failover drill, recovery exercise, monitoring review, log inspection, compliance audit, or contract test.
- Treat generic quality requirements without a source as provisional candidates with `Missing - open issue OI-###`.

## Measurability Check

Revise or flag any NFR that relies on vague wording such as `fast`, `secure`, `reliable`, `scalable`, `robust`, `intuitive`, `easy`, `usable`, `high availability`, or `appropriate` without a metric and context.

Prefer this shape:

```text
Under <operating context>, the system shall meet <threshold/metric> because of <source link>; verify by <method>.
```

## Quality Gate

Before returning, verify:

- Every NFR has a stable NFR ID.
- Every NFR has a quality category.
- Every NFR has a measurable threshold/metric.
- Every NFR states the operating context/environment.
- Every NFR has a source link to a success criterion, constraint, risk, context item, goal, stakeholder statement, or approved assumption ID/reference.
- Every NFR has a verification method that can determine pass/fail.
- Unsupported NFR candidates are marked with `Missing - open issue OI-###` instead of being presented as confirmed requirements.
