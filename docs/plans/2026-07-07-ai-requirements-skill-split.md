# AI Requirements Skill Split Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Split the AI requirements workflow into an orchestrator skill plus focused step skills for detailed artifact generation.

**Architecture:** Keep `creating-ai-requirements` as the entry point and routing layer. Add six subskills for detailed artifact work, each created with the `superpowers:writing-skills` RED-GREEN-REFACTOR process. Leave SRS assembly in the orchestrator until final SRS generation proves large enough to split.

**Tech Stack:** Codex skills as Markdown (`SKILL.md`), pressure-scenario Markdown files, shell validation with `awk`, `python3`, `rg`, and `wc`.

**Repository Note:** If `git status --short` fails, skip commit steps. If it succeeds, commit after validation.

---

### Task 1: Update Orchestrator Routing

**Files:**
- Modify: `creating-ai-requirements/SKILL.md`
- Modify: `creating-ai-requirements/pressure-scenarios.md`

**Step 1: Write the RED pressure scenario**

Add a scenario where the user asks for one specific artifact, such as functional requirements, and an unskilled agent either writes a full SRS or ignores the step-specific workflow.

Expected scenario text:

```markdown
## RED Scenario 4: Step routing pressure

Prompt: "I already have goals and context. Write the functional requirements only."

Expected unskilled failure:
- Generates unrelated SRS sections.
- Does not route to step-specific guidance.
- Drops approved context and traceability links.

Required correction in skill:
- Route specific artifact requests to the matching step skill.
- Keep the context ledger as the shared contract.
```

**Step 2: Update the orchestrator**

Add a compact "Step Skill Routing" table to `creating-ai-requirements/SKILL.md`:

```markdown
## Step Skill Routing

| Need | Use |
| --- | --- |
| clarify business task, interview questions, goals | `eliciting-business-requirements` |
| system boundary, actors, external systems, context diagram | `modeling-system-context` |
| FR list, modules, priorities, acceptance-ready requirements | `writing-functional-requirements` |
| UC register, main/alternate/error flows, use-case diagram | `modeling-use-cases` |
| glossary, data dictionary, CRUD matrix, class/state diagrams | `modeling-requirements-data` |
| measurable quality attributes, constraints, NFR thresholds | `writing-nonfunctional-requirements` |
```

**Step 3: Validate**

Run:

```bash
rg -n "Step Skill Routing|eliciting-business-requirements|writing-functional-requirements|context ledger" creating-ai-requirements
wc -w creating-ai-requirements/SKILL.md
```

Expected: routing section and all six skill names found; word count remains reasonable.

**Step 4: Commit if git is available**

```bash
git status --short
git add creating-ai-requirements/SKILL.md creating-ai-requirements/pressure-scenarios.md
git commit -m "docs: route ai requirements step skills"
```

Skip if `git status` reports this is not a repository.

### Task 2: Create `eliciting-business-requirements`

**Files:**
- Create: `eliciting-business-requirements/SKILL.md`
- Create: `eliciting-business-requirements/pressure-scenarios.md`

**Step 1: Use required skill**

Load `superpowers:writing-skills` before creating this skill.

**Step 2: Write RED scenarios**

Cover at least:

- founder gives one vague phrase and asks for requirements;
- stakeholder access is limited;
- agent invents goals instead of asking focused questions.

**Step 3: Write minimal skill**

The skill must require:

- extracting business problem, stakeholders, goals, assumptions, risks;
- asking focused clarification questions before generating requirements;
- producing Q/A/conclusion tables and measurable success criteria;
- marking invented details as assumptions.

**Step 4: Validate**

Run:

```bash
awk 'NR==1&&$0!="---"{bad=1} NR==2&&$0!~/^name: [A-Za-z0-9-]+$/{bad=1} NR==3&&$0!~/^description: Use when /{bad=1} NR==4&&$0!="---"{bad=1} END{exit bad}' eliciting-business-requirements/SKILL.md
rg -n "questions|success criteria|assumptions|stakeholder|uncertainty" eliciting-business-requirements
```

Expected: frontmatter passes; required terms are present.

### Task 3: Create `modeling-system-context`

**Files:**
- Create: `modeling-system-context/SKILL.md`
- Create: `modeling-system-context/pressure-scenarios.md`

**Step 1: Write RED scenarios**

Cover:

- agent confuses system actors with internal components;
- agent omits external systems;
- agent draws a diagram without a clear boundary.

**Step 2: Write minimal skill**

The skill must require:

- explicit system boundary;
- actor and external-system classification;
- input/output data-flow table;
- DOT context diagram output;
- unresolved boundary questions.

**Step 3: Validate**

Run:

```bash
awk 'NR==1&&$0!="---"{bad=1} NR==2&&$0!~/^name: [A-Za-z0-9-]+$/{bad=1} NR==3&&$0!~/^description: Use when /{bad=1} NR==4&&$0!="---"{bad=1} END{exit bad}' modeling-system-context/SKILL.md
rg -n "boundary|actor|external system|data flow|DOT" modeling-system-context
```

Expected: frontmatter passes; boundary and diagram rules are present.

### Task 4: Create `writing-functional-requirements`

**Files:**
- Create: `writing-functional-requirements/SKILL.md`
- Create: `writing-functional-requirements/pressure-scenarios.md`

**Step 1: Write RED scenarios**

Cover:

- agent writes vague, untestable requirements;
- agent mixes functional and nonfunctional requirements;
- agent loses source links.

**Step 2: Write minimal skill**

The skill must require:

- stable FR IDs;
- source/context link per FR;
- module/process/role grouping;
- priority;
- testable wording;
- exclusion of NFRs unless flagged separately.

**Step 3: Validate**

Run:

```bash
awk 'NR==1&&$0!="---"{bad=1} NR==2&&$0!~/^name: [A-Za-z0-9-]+$/{bad=1} NR==3&&$0!~/^description: Use when /{bad=1} NR==4&&$0!="---"{bad=1} END{exit bad}' writing-functional-requirements/SKILL.md
rg -n "FR|source|priority|testable|nonfunctional|NFR" writing-functional-requirements
```

Expected: frontmatter passes; FR quality gates are present.

### Task 5: Create `modeling-use-cases`

**Files:**
- Create: `modeling-use-cases/SKILL.md`
- Create: `modeling-use-cases/pressure-scenarios.md`

**Step 1: Write RED scenarios**

Cover:

- agent creates use cases that do not reference FRs;
- agent omits alternate and error flows;
- agent confuses UI steps with user goals.

**Step 2: Write minimal skill**

The skill must require:

- UC IDs and linked FR IDs;
- primary actor, trigger, preconditions, postconditions;
- main, alternate, and error flows;
- PlantUML use-case diagram;
- gaps sent back to FR/context.

**Step 3: Validate**

Run:

```bash
awk 'NR==1&&$0!="---"{bad=1} NR==2&&$0!~/^name: [A-Za-z0-9-]+$/{bad=1} NR==3&&$0!~/^description: Use when /{bad=1} NR==4&&$0!="---"{bad=1} END{exit bad}' modeling-use-cases/SKILL.md
rg -n "UC|FR|alternate|error flow|PlantUML|precondition|postcondition" modeling-use-cases
```

Expected: frontmatter passes; use-case structure is present.

### Task 6: Create `modeling-requirements-data`

**Files:**
- Create: `modeling-requirements-data/SKILL.md`
- Create: `modeling-requirements-data/pressure-scenarios.md`

**Step 1: Write RED scenarios**

Cover:

- agent invents entities not supported by use cases;
- agent skips glossary definitions;
- agent omits CRUD coverage.

**Step 2: Write minimal skill**

The skill must require:

- glossary and data dictionary;
- entity source links to UC steps;
- CRUD matrix by actor/use case;
- class/state diagrams only when justified;
- unresolved data questions.

**Step 3: Validate**

Run:

```bash
awk 'NR==1&&$0!="---"{bad=1} NR==2&&$0!~/^name: [A-Za-z0-9-]+$/{bad=1} NR==3&&$0!~/^description: Use when /{bad=1} NR==4&&$0!="---"{bad=1} END{exit bad}' modeling-requirements-data/SKILL.md
rg -n "glossary|data dictionary|CRUD|entity|UC|state diagram|class diagram" modeling-requirements-data
```

Expected: frontmatter passes; data model gates are present.

### Task 7: Create `writing-nonfunctional-requirements`

**Files:**
- Create: `writing-nonfunctional-requirements/SKILL.md`
- Create: `writing-nonfunctional-requirements/pressure-scenarios.md`

**Step 1: Write RED scenarios**

Cover:

- agent writes vague NFRs such as "fast" or "secure";
- agent creates NFRs without metrics;
- agent does not link NFRs to goals, constraints, or usage context.

**Step 2: Write minimal skill**

The skill must require:

- NFR IDs;
- quality category;
- measurable threshold;
- operating context/environment;
- source link to success criteria, constraint, or risk;
- verification method.

**Step 3: Validate**

Run:

```bash
awk 'NR==1&&$0!="---"{bad=1} NR==2&&$0!~/^name: [A-Za-z0-9-]+$/{bad=1} NR==3&&$0!~/^description: Use when /{bad=1} NR==4&&$0!="---"{bad=1} END{exit bad}' writing-nonfunctional-requirements/SKILL.md
rg -n "NFR|threshold|metric|environment|verification|constraint|risk" writing-nonfunctional-requirements
```

Expected: frontmatter passes; measurable NFR gates are present.

### Task 8: Cross-Skill Consistency Review

**Files:**
- Modify as needed: all `*/SKILL.md`
- Modify as needed: all `*/pressure-scenarios.md`

**Step 1: Validate naming and frontmatter for every skill**

Run:

```bash
for f in */SKILL.md; do
  awk 'NR==1&&$0!="---"{bad=1} NR==2&&$0!~/^name: [A-Za-z0-9-]+$/{bad=1} NR==3&&$0!~/^description: Use when /{bad=1} NR==4&&$0!="---"{bad=1} END{exit bad}' "$f" || exit 1
done
```

Expected: command exits 0.

**Step 2: Validate routing coverage**

Run:

```bash
rg -n "eliciting-business-requirements|modeling-system-context|writing-functional-requirements|modeling-use-cases|modeling-requirements-data|writing-nonfunctional-requirements" creating-ai-requirements/SKILL.md
```

Expected: all six subskills are listed.

**Step 3: Validate traceability language**

Run:

```bash
rg -n "source|trace|ID|context ledger|assumption|uncertainty" */SKILL.md
```

Expected: each skill contains relevant traceability or uncertainty language.

**Step 4: Commit if git is available**

```bash
git status --short
git add creating-ai-requirements eliciting-business-requirements modeling-system-context writing-functional-requirements modeling-use-cases modeling-requirements-data writing-nonfunctional-requirements docs/plans
git commit -m "docs: split ai requirements workflow skills"
```

Skip if `git status` reports this is not a repository.
