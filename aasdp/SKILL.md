---
name: aasdp
description: Guide a software project through question-by-question discovery, minimal specifications, approved phased implementation, verification, and completion. Use when the user invokes aasdp or asks for this full AI-assisted development workflow; do not apply to a routine isolated edit.
---

# AI-Assisted Software Development Protocol (AASDP) v1.0

Default profile: **Standard**. Apply this skill to the current project, whether new or inherited. Project instructions and the user's current request take precedence. Approval of one gate does not imply approval of a later gate or an unrelated external action.

## 1. Discover the outcome

Begin with the user's idea or the existing codebase. Inspect available project context before asking for facts already recorded. Ask **one focused question per turn**, wait for the answer, then ask the next question that most reduces uncertainty. Be direct and persistent, in a grill-me style, but do not use a fixed questionnaire or manufacture decisions. Ask for concrete examples when answers are vague. Cover, as relevant:

- The problem, affected users, and current workaround.
- Business objective, measurable success, and what failure looks like even if the code runs.
- The smallest useful outcome, critical user journey, and acceptance examples.
- Scope boundaries: required, excluded, and deferred capabilities.
- Constraints: platforms, integrations, data, security/privacy, performance, deadlines, and budget.
- Existing system behavior that must remain true, known risks, and who can approve decisions.

State assumptions explicitly and verify consequential ones. If the user does not know a detail, record it as **open** and propose the cheapest way to resolve it. Do not convert an unanswered question into a hidden default. Stop discovery when the outcome and first implementation boundary are clear enough to make a falsifiable plan. For an inherited project, inspect the relevant code and tests to check whether the current approach can achieve the stated outcome.

Present a short discovery recap with objective, success measures, in/out scope, constraints, assumptions, open questions, and proposed first release. **Gate 1:** ask the user to approve or correct this recap before treating it as the specification.

## 2. Create the minimum working documents

After Gate 1, create or update only these six project documents, using [references/document-templates.md](references/document-templates.md). Keep them short, linked, and useful to the next decision:

1. `README.md`: purpose, setup/run, checks, current status.
2. `AGENTS.md`: project-specific agent instructions, commands, boundaries, and approval rules. Preserve existing instructions; do not overwrite them blindly.
3. `PRD.md`: problem, users, outcomes, scope, acceptance criteria.
4. `ARCHITECTURE.md`: current/proposed components, data flow, interfaces, constraints.
5. `PLAN.md`: high-level phases, one detailed active phase, gates, verification, and ASCII diagrams.
6. `DECISIONS.md`: brief decision log with alternatives and reasons.

If a document already exists, update the relevant section instead of creating a competing file. If the project uses another canonical location or name, follow it and record the mapping in `README.md`. Do not create extra documents solely to satisfy a process. Keep unresolved items visible.

## 3. Plan from coarse to detailed

Show the entire route in small, outcome-based phases. Keep future phases at a coarse level; fully detail only the **next phase**. The high-level `PLAN.md` must include an ASCII diagram showing phase order and approval/verification gates. Each active phase must include its own ASCII diagram showing work flow, boundaries, and checks. Plain text diagrams must be understandable without rendering.

For the active phase, specify: outcome and user-visible behavior; in scope and out of scope; prerequisites and affected files or components; implementation steps small enough to review; acceptance examples; risk-based verification; likely failure modes and rollback/recovery; expected commit boundary. Prefer the simplest design that meets today's requirements. Explain meaningful choices and rejected alternatives in `DECISIONS.md`.

**Gate 2:** present the high-level plan, active phase detail, diagrams, and material trade-offs for approval. Do not start implementation until the user approves the architecture and this phase. At each later phase, expand that phase, refresh its assumptions and diagram, and obtain approval before implementation. If the user has already approved a precise design and phase in the current conversation, use that authorization without re-asking.

## 4. Implement one approved phase

Work only within the approved scope. Use small changes that can be inspected together. Before editing, note the repository state and isolate unrelated changes. Keep code modular and follow the project's conventions. Do not silently add features, change acceptance criteria, or change architecture.

After each meaningful slice, inspect the diff and verify the behavior affected by that slice. Run the smallest useful checks first, then broader checks when risk warrants. Critical logic needs tests for the expected path and important edge/failure paths; simple or low-risk changes need proportionate checks. Do not substitute passing tests for checking the user outcome. If a check cannot run, record why and what remains unverified. Let the user review the work and give refinement feedback; update the active phase plan when feedback changes it.

Make a **small, verified commit** at a coherent boundary when the repository and user authorization permit it. A phase can contain more than one commit. Commit only files belonging to the approved work; use a message that names the behavior changed. Never push, merge, deploy, publish, or discard user work without separate authorization. Where local project rules require approval before commit, wait for it. If verification fails, do not commit a claim of completed behavior.

**Gate 3:** show the phase result, changed files, verification evidence, deviations, and remaining risks. Ask the user to accept the phase or request refinement before detailing or starting the next one. A user can approve several clearly described phase gates in advance; do not invent blanket approval.

## 5. Handle deviations and failures

When work diverges from the approved plan, stop the affected work. Explain the observation, impact on outcome/scope, options with trade-offs, and the smallest recommended amendment. Update `PLAN.md` and, for a durable design choice, `DECISIONS.md` after the user approves the amendment. Continue unaffected work if safe.

For a failed iteration, preserve evidence and inspect the diff. Offer a targeted repair, reverting only the agent's isolated change, or restarting from a known checkpoint. Do not automatically discard code or overwrite unrelated work. Re-run relevant checks after a repair. Escalate when repeated fixes reveal a design problem, a critical assumption fails, or the success metric is no longer reachable with the approved plan.

## 6. Complete and report

At the end of the accepted scope, check the critical journey against the PRD's acceptance criteria, review the final diff and repository state, and update the six documents only where facts changed. Provide a concise completion report: delivered outcome, acceptance evidence and checks run, commits (if any), deviations/decisions, known limitations, and next actions. Separate observed results from expectations. Do not label an unverified outcome complete.

## Operating reminders

- Approval gates concern the **specification, the plan/active phase, and phase acceptance**. Ask for a concrete decision, then pause the dependent work; continue independent work where useful.
- Use the project owner's words for goals and metrics. Avoid generic KPIs and arbitrary phase counts.
- Keep documentation proportional to the project. The six named files are the complete default set, not an invitation to expand paperwork.
- The Standard profile is the default. Adjust rigor only when the user explicitly chooses another level or project risk demands stronger checks; never weaken explicit project rules.

