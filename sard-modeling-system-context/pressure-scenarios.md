# Pressure Scenarios

These RED scenarios define failures this skill must prevent when modeling a system context.

## RED Scenario 1: Actor/component confusion

Prompt: "Model the context for an appointment reminder service with a scheduler, API, notification worker, patient, and clinic admin."

Expected unskilled failure:
- Treats the scheduler, API, and notification worker as system actors.
- Mixes internal components with people and organizations outside the system.
- Produces a context diagram that looks like an internal architecture diagram.

Required correction in skill:
- Classify actors as external people, roles, groups, or organizations.
- Classify internal components separately and keep them out of the context diagram unless the user changes the boundary.

## RED Scenario 2: External systems omitted

Prompt: "Patients receive SMS reminders and appointments come from the clinic EHR. Draw the system context."

Expected unskilled failure:
- Shows only patients and clinic staff.
- Omits the SMS provider and EHR as external systems.
- Does not show what data crosses between the system and those systems.

Required correction in skill:
- Identify every external system named or implied by integrations, data sources, destinations, identity, payments, messaging, storage, analytics, or compliance.
- Require an input/output data-flow table for each actor and external system.

## RED Scenario 3: Unclear boundary

Prompt: "Make a context diagram for a returns portal, warehouse operations, courier pickup, refunds, and support."

Expected unskilled failure:
- Draws all domains as boxes with no declared system boundary.
- Leaves it unclear whether warehouse operations, courier pickup, and refunds are inside or outside the modeled system.
- Does not surface boundary questions while diagramming uncertain scope.

Required correction in skill:
- State the explicit system boundary before diagramming.
- Mark ambiguous items as inside, outside, or unresolved.
- List unresolved boundary questions when scope cannot be determined from the prompt.

## GREEN Verification Targets

- Skill requires an explicit system boundary.
- Skill distinguishes actors, external systems, internal components, and unresolved boundary items.
- Skill requires an input/output data-flow table.
- Skill requires DOT context diagram output with a clear boundary.
- Skill requires unresolved boundary questions when scope is ambiguous.
