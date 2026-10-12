# Minimal project document templates

Adapt these headings to an existing project. Write only known facts; mark unresolved items `Open:`. Do not fill templates with generic promises.

## `README.md`

```markdown
# <Project name>

<One-sentence purpose and intended user outcome.>

## Start
<Prerequisites and exact local run command, or Open: ...>

## Verify
<Exact checks and what each proves.>

## Status
<Current phase, working/not working, and known limits.>

## Project docs
<Links to PRD, ARCHITECTURE, PLAN, DECISIONS, AGENTS.>
```

## `AGENTS.md`

```markdown
# Agent instructions

## Goal and boundaries
<The measurable outcome and what must not change.>

## How to work here
<Project-specific conventions, approved scope, approval gates, commands.>

## Verification
<Relevant tests, manual check, and risky areas.>

## Repository care
<How to handle existing changes and commit boundaries.>
```

If `AGENTS.md` exists, read and preserve its binding instructions. Add only missing project-specific guidance and flag conflicts for the owner.

## `PRD.md`

```markdown
# Product requirements

## Problem and users
<Who is affected, current pain, evidence or examples.>

## Objective and measures
<Business objective, measurable success, and failure conditions.>

## Scope
- Must: <minimum useful capabilities>
- Excluded: <explicitly out of scope>
- Deferred: <ideas requiring a later decision>

## Critical journey
<Start-to-finish user behavior.>

## Acceptance criteria
- Given <context>, when <action>, then <observable result>.

## Constraints and open questions
<Facts, assumptions to validate, unresolved decisions.>
```

## `ARCHITECTURE.md`

```markdown
# Architecture

## Current state
<Relevant existing behavior and constraints, or new-project baseline.>

## Proposed components and responsibilities
<Only components needed for approved scope.>

## Data flow and interfaces
<Inputs, transformations, outputs, external systems, failure handling.>

## Invariants and risks
<What must remain true; important operational/security risks.>
```

## `PLAN.md`

```markdown
# Delivery plan

## High-level route
<One line per phase: outcome, acceptance gate. Future phases stay coarse.>

Idea -> Discovery [approve] -> Docs/Plan [approve]
     -> Phase 1 [verify + accept] -> Phase 2 [verify + accept] -> Done

## Active phase: <name>
Outcome: <observable result>
In scope: <items>
Out of scope: <items>
Prerequisites: <facts and dependencies>
Affected areas: <files/components if known>
Steps: <small reviewable slices>

Input -> <change boundary> -> Output
              |
              v
        <checks> -> Review -> Commit/accept gate

Acceptance examples: <expected and important edge/failure cases>
Verification: <tests, manual journey, risk-based checks>
Failure modes/recovery: <likely problems and safe response>
Commit boundary: <coherent verified slice>
Status: <not started/in progress/blocked/accepted>

## Later phases
<Outcome and dependency only; detail each when it becomes active.>
```

Replace both sample diagrams with diagrams of the actual project. Keep ASCII shapes simple and label gates explicitly.

## `DECISIONS.md`

```markdown
# Decisions

## D-001: <short title> — <date>
Status: proposed | accepted | superseded
Context: <problem or constraint>
Chosen: <approach>
Rejected: <real alternative(s)>
Why: <reason tied to objective and trade-off>
Consequence: <risk, cost, or follow-up>
```

Record only consequential choices; do not log every implementation detail.

