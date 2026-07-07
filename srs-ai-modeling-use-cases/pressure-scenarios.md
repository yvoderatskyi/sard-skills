# Pressure Scenarios

These RED scenarios define failures this skill must prevent when modeling use cases from requirements context.

## RED Scenario 1: Use cases without FR traceability

Prompt: "Create use cases for a clinic appointment reminder app from these FRs: FR-001 import appointments from EHR, FR-002 send reminder, FR-003 prevent duplicate reminders."

Expected unskilled failure:
- Invents use cases without citing FR IDs.
- Drops one or more FRs from the UC register.
- Adds behavior that cannot be traced back to an FR or stated context.

Required correction in skill:
- Require stable UC IDs.
- Require linked FR IDs for every use case.
- Send uncovered or unsupported behavior back to FR/context as a gap.

Pass criteria:
- Each UC row includes at least one linked FR ID.
- Every named FR is covered or listed as a gap.
- New behavior not supported by FR/context is flagged instead of silently added.

## RED Scenario 2: Missing alternate and error flows

Prompt: "Write use cases for password reset where email delivery may fail, token may expire, and the user may already be signed in."

Expected unskilled failure:
- Writes only the happy path.
- Treats variations and failures as notes instead of flows.
- Omits alternate and error flow labels.

Required correction in skill:
- Require main, alternate, and error flows for each use case.
- Use explicit flow IDs or labels.
- Capture recovery or terminal outcomes for error flows.

Pass criteria:
- Each UC includes a main flow plus alternate flows and error flows.
- Expired token and email failure appear as error flows.
- Already signed in appears as an alternate flow or a justified gap.

## RED Scenario 3: UI steps confused with user goals

Prompt: "Make use cases for a returns portal: user clicks Returns, opens the item dropdown, taps Continue, uploads photo, and presses Submit."

Expected unskilled failure:
- Names use cases after screens, clicks, forms, or buttons.
- Describes UI navigation as the user goal.
- Omits actor intent, trigger, preconditions, and postconditions.

Required correction in skill:
- Model use cases as actor goals, not UI procedures.
- Require primary actor, trigger, preconditions, and postconditions.
- Keep UI details only when they clarify a flow step, not as the use-case identity.

Pass criteria:
- UC names are goal-oriented, such as `Request Return`, not `Click Submit`.
- Each UC states primary actor, trigger, preconditions, and postconditions.
- Flow steps describe meaningful actor/system interaction rather than raw UI gestures.

## RED Scenario 4: Weak PlantUML diagram

Prompt: "Create a use-case diagram for patient reminders with patient, clinic admin, EHR import, send reminder, view reminder history, and duplicate suppression."

Expected unskilled failure:
- Places actors and UCs together with no system boundary.
- Draws UCs outside the boundary or actors inside it.
- Adds include/extend relationships between most UCs even when they do not clarify required behavior.

Required correction in skill:
- Require PlantUML with actors outside the system boundary and UCs inside it.
- Require actor-to-use-case associations.
- Avoid include/extend relationships unless they clarify required behavior.

Pass criteria:
- Diagram has a visible system boundary containing UCs.
- Patient and clinic admin are outside the boundary.
- Include/extend is absent unless justified by the FR/context.

## GREEN Verification Targets

- Skill frontmatter contains only `name` and `description`.
- Skill description starts with `Use when`.
- Skill requires UC IDs and linked FR IDs.
- Skill requires every provided FR to be covered, excluded with reason, or routed to FR/context gaps.
- Skill requires primary actor, trigger, preconditions, and postconditions.
- Skill requires main, alternate, and error flows.
- Skill requires alternate and error flows to reference the originating main-flow step unless global.
- Skill requires a PlantUML use-case diagram with actors outside the boundary, UCs inside, and useful include/extend only.
- Skill requires gaps to be routed back to FR/context.
