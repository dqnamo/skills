---
name: implement-plan
description: Implement an active feature plan from .context/plans/ as validated vertical slices, keep the plan and project context aligned with reality, and complete the plan when its acceptance criteria pass. Use when the user asks to execute or implement an existing plan.
---

# Implement Plan

Implement an existing plan completely and keep code, tests, and `.context/` consistent. Do not create a PR or deploy unless the user also asks.

## 1. Select the Plan

Use the plan named by the user. Otherwise read `.context/plans/index.md` and select the only clearly relevant active plan. If multiple plans could apply, ask which one to implement.

Read:

```text
AGENTS.md
.context/concepts.md
.context/architecture.md
.context/decisions/index.md
.context/plans/<feature-name>.md
.context/guidance.md
```

Open relevant ADRs, nested instructions, and files named by the plan.

## 2. Verify the Plan

Inspect the current code before editing. Confirm that the plan's description of current behaviour, affected areas, dependencies, and implementation order still matches reality.

Resolve discrepancies before proceeding:

- **Discoverable:** investigate and update the plan.
- **Product ambiguity:** ask the user.
- **Significant technical decision:** explain the tradeoffs, resolve it, and record an ADR when warranted.

Do not blindly implement a stale assumption.

## 3. Implement Vertical Slices

Work through the plan in vertical slices. For each slice:

1. Implement the smallest complete behaviour described by the slice.
2. Follow existing project patterns and avoid unrelated refactors.
3. Add or update tests for meaningful behaviour.
4. Run the narrowest useful validation.
5. Update the plan if implementation changes its design, scope, or remaining work.

Keep the repository usable after each slice where practical.

## 4. Handle Discoveries

When implementation reveals new information:

- incorrect plan detail → correct the plan
- changed domain concept or invariant → update `concepts.md`
- changed current system structure → update `architecture.md`
- significant decision → create an ADR and update `decisions/index.md`
- new project convention → update `guidance.md`

Do not preserve an outdated plan for historical purity. The completed plan should describe the work that was actually delivered.

Stop and ask the user only when a product decision, meaningful scope change, destructive action, or unavailable dependency prevents safe progress.

## 5. Validate the Whole Feature

Before completion:

1. Check every acceptance criterion against observable behaviour.
2. Run relevant tests, type checks, linting, builds, or focused manual checks in proportion to risk.
3. Review the final diff for missing files, accidental changes, debug code, secrets, and unrelated scope.
4. Confirm migrations, configuration, permissions, failure paths, and backwards compatibility where relevant.

Do not claim a check passed unless it ran successfully. Report checks that could not run and why.

## 6. Complete the Plan

Only after implementation and validation are complete:

1. Set the plan status to `Completed`.
2. Add `**Completed:** YYYY-MM-DD`.
3. Ensure the plan reflects the delivered design and decisions.
4. Move it from Active to Completed in `.context/plans/index.md`.
5. Ensure durable knowledge is captured in concepts, architecture, decisions, or guidance.

If required work remains, keep the plan active and record what remains.

## Completion Report

Tell the user:

- what was implemented
- important plan or design changes
- validation performed and its result
- anything still blocked or requiring later operational work

## Do Not

- invent requirements or silently expand scope
- implement from the plan without checking current code
- postpone necessary context updates
- mark the plan completed with failing or unchecked acceptance criteria
- create a PR, merge, deploy, or perform post-deploy work unless requested
