# Pressure Scenarios

These RED scenarios document failures this skill must prevent when an agent writes functional requirements under incomplete or messy context.

## RED Scenario 1: Vague, untestable requirements

Prompt: "Write FRs for a clinic reminder app so missed appointments go down."

Expected unskilled failure:
- Writes requirements such as "The system should be user-friendly" or "The app should support reminders."
- Combines several behaviors in one broad requirement.
- Does not include trigger, actor/system behavior, or expected result.

Required correction in skill:
- Require testable FR wording with observable behavior.
- Require one behavior per FR.
- Flag vague terms that cannot become acceptance tests.

Pass criteria:
- Each FR can be restated as Given/When/Then without adding new facts.
- No FR relies on vague quality words as the required behavior.

## RED Scenario 2: Functional and nonfunctional mixing

Prompt: "Create functional requirements and include security, performance, usability, and reminder behavior."

Expected unskilled failure:
- Places performance, security, availability, and usability statements in the FR table.
- Treats quality attributes as ordinary system behavior.
- Produces an FR list that cannot cleanly route to NFR work.

Required correction in skill:
- Define FRs as observable system behavior.
- Exclude nonfunctional requirements from the FR table.
- Place nonfunctional items in a separate `NFR Candidates` section with source links by default.

Pass criteria:
- Reminder behavior appears only in the FR list.
- Security, performance, availability, and usability statements appear only in `NFR Candidates`.
- Every NFR candidate preserves its source/context link and suggested route.

## RED Scenario 3: Lost source links

Prompt: "Use these interview notes and context rows to write module-level FRs with priorities: BR-003 says patients need reminders before appointments; CTX-FLOW-02 says the clinic calendar sends appointment updates; INT-07 says 'patients must not receive duplicate reminders'; ASM-01 says SMS is provisional."

Expected unskilled failure:
- Drops stakeholder quote, context row, business requirement, assumption, or use-case references.
- Renumbers FRs on revision, breaking traceability.
- Assigns priorities without preserving the source or rationale.

Required correction in skill:
- Require stable FR IDs.
- Require a source/context link per FR.
- Require module, process, or role grouping plus priority on every FR.

Pass criteria:
- FR rows cite concrete links such as `BR-003`, `CTX-FLOW-02`, `INT-07`, or `ASM-01`.
- No source-backed FR uses a blank, generic, or invented source link.
- Any provisional FR without a source uses `Missing - open issue OI-###`.

## GREEN Verification Targets

- Skill frontmatter contains only `name` and `description`.
- Skill description starts with `Use when`.
- Skill requires stable FR IDs, source/context links, grouping, priority, testable wording, and preservation of NFR-like material in `NFR Candidates`.
- Pressure scenarios cover vague FRs, FR/NFR mixing, and lost source links.
