# Pressure Scenarios

These RED scenarios define failures this skill must prevent when modeling requirements data from use cases and requirements context.

## RED Scenario 1: Invented entities under domain pressure

Prompt: "From UC-001 Schedule Appointment and UC-002 Send Reminder, create the data model for a clinic reminder app. Make it complete."

Expected unskilled failure:
- Adds entities such as BillingAccount, InsurancePolicy, ProviderSchedule, or ConsentForm without UC step or FR support.
- Treats likely implementation convenience as requirements truth.
- Does not show why each entity exists.

Required correction in skill:
- Require entity source links to UC steps or explicit approved sources.
- Route unsupported entities to unresolved data questions instead of including them.

Pass criteria:
- Each entity links to a UC step such as `UC-001 step 3`.
- Unsupported entities are absent from the data dictionary or listed as questions.
- Notes distinguish requirement-backed entities from assumptions.

## RED Scenario 2: Glossary skipped for familiar terms

Prompt: "Create a data dictionary for returns, refunds, RMAs, item eligibility, and exception approvals. The terms are obvious."

Expected unskilled failure:
- Produces entities and attributes without defining domain terms.
- Uses similar terms inconsistently, such as return, refund, RMA, and approval.
- Leaves status and identifier meanings implicit.

Required correction in skill:
- Require a glossary before the data dictionary.
- Require definitions for all domain terms, statuses, identifiers, and diagram labels.

Pass criteria:
- Glossary defines every domain term used in the data artifacts.
- Uncertain definitions are marked as assumptions or unresolved questions.
- Data dictionary terms match the glossary names.

## RED Scenario 3: CRUD coverage omitted

Prompt: "We have patient, clinic admin, and support agent use cases. Create entities and attributes for reminders, appointments, and notification history."

Expected unskilled failure:
- Lists entities and attributes but omits who creates, reads, updates, or deletes/archives each entity.
- Ignores actor differences and use-case-specific permissions.
- Leaves retention, correction, and archive behavior unspecified.

Required correction in skill:
- Require a CRUD matrix by actor/use case.
- Require every data dictionary entity to be covered or questioned.
- Treat missing delete/archive, retention, and correction rules as unresolved data questions.

Pass criteria:
- CRUD matrix includes actor, use case, entity, and create/read/update/delete/archive columns.
- Every entity appears in relevant actor/use-case rows.
- Missing CRUD behavior is listed as a data question instead of silently omitted.

## RED Scenario 4: Decorative diagrams invent lifecycle

Prompt: "Add a class diagram and state diagram for appointment reminders. We only know UC-002 sends a reminder and FR-003 prevents duplicates."

Expected unskilled failure:
- Produces class/state diagrams because diagrams feel expected.
- Invents relationships such as ReminderBatch owns ReminderAttempt without UC/FR support.
- Invents states and transitions such as Draft, Queued, Retrying, Escalated, and Archived without lifecycle requirements.

Required correction in skill:
- Require class diagrams and state diagrams only when they clarify reviewed requirements.
- Require every relationship, state, guard, and transition to trace to a UC step, FR, rule, or data question.
- Route unsupported diagram content to unresolved data questions.

Pass criteria:
- Decorative diagrams are omitted when they do not clarify requirements.
- Any included class diagram or state diagram has traceable relationships, states, and transitions.
- Unsupported attributes, relationships, states, and transitions are removed or listed as questions.

## GREEN Verification Targets

- Skill frontmatter contains only `name` and `description`.
- Skill description starts with `Use when`.
- Skill requires a glossary and data dictionary.
- Skill requires entity source links to UC steps.
- Skill requires a CRUD matrix by actor/use case.
- Skill allows class diagram and state diagram outputs only when justified.
- Skill requires unresolved data questions.
- Skill routes unsupported attributes, relationships, states, and transitions to unresolved data questions.
