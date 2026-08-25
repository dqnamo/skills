---
name: plan-feature
description: Turn a feature idea into a codebase-informed implementation plan by investigating first, grilling the user on material unknowns, resolving decisions, and writing a plan under .context/plans/. Use when the user wants to plan a feature without implementing it.
---

# Plan Feature

Produce a clear implementation plan grounded in the existing codebase. Do not implement the feature.

## Workflow

### 1. Understand the Request

Identify the desired outcome, expected user behaviour, obvious constraints, affected areas, and ambiguous terminology. Do not immediately ask questions; investigate first.

### 2. Read Project Context

Read the relevant parts of:

```text
.context/concepts.md
.context/architecture.md
.context/decisions/index.md
.context/plans/index.md
.context/guidance.md
```

Open relevant ADRs and existing plans. Understand the project's terminology, current architecture, decisions, and conventions before designing anything.

### 3. Explore the Codebase

Inspect the implementation related to the request. Understand current behaviour, relevant concepts, data flow, existing patterns, system boundaries, similar functionality, and constraints created by the code.

Do not ask the user questions that the repository can answer.

### 4. Classify Unknowns

Build this mental model:

```text
Current behaviour
-> Desired behaviour
-> Areas affected
-> Constraints
-> Decisions required
-> Unknowns
```

Classify unknowns:

- **Discoverable:** investigate the code or context yourself.
- **Product decisions:** ask what the user wants.
- **Technical decisions:** explain meaningful options and tradeoffs, then resolve them with the user.

### 5. Grill the User

Ask targeted questions until the important behaviour is clear. Probe only where relevant:

- exact user behaviour and scope boundaries
- lifecycle, states, and permissions
- edge cases and failure behaviour
- data ownership and backwards compatibility
- interactions with existing features

Prefer concrete questions. For example, ask “If execution fails, should it retry automatically, show a failed state, or both?” instead of “How should failures work?”

Group related questions without overwhelming the user. Do not ask questions purely for completeness.

### 6. Challenge the Design

Look for unnecessary new concepts, duplication, contradictions with existing concepts, architectural complexity, unclear ownership, missing states, and surprising edge cases. Surface a simpler approach when it achieves the same outcome.

### 7. Handle Decisions

When planning produces a significant architectural decision:

1. Create an ADR in `.context/decisions/`.
2. Update `.context/decisions/index.md`.
3. Link the ADR from the plan.

Do not create ADRs for ordinary implementation details. Do not update `architecture.md` to describe planned work as if it already exists.

### 8. Write the Plan

Once material ambiguity is resolved, create `.context/plans/<feature-name>.md`:

```md
# Feature Name

**Status:** Active

## Goal

What the feature should achieve.

## Current System

How the relevant system works today.

## Proposed Behaviour

What changes from the user's perspective.

## Design

How the feature fits the existing architecture and concepts.

Include Mermaid diagrams only when they materially improve understanding.

## Implementation

### 1. Vertical Slice

Working behaviour introduced by this slice.

Relevant areas:
- ...

### 2. Vertical Slice

...

## Data Changes

Schema or persistence changes, if any.

## Edge Cases

Important behaviour the implementation must handle.

## Decisions

Important decisions made during planning, with ADR links where applicable.

## Acceptance Criteria

Observable conditions that mean the feature is complete.
```

Add the plan to the Active section of `.context/plans/index.md`.

## Prefer Vertical Slices

Prefer:

```text
Create scheduled execution end-to-end
-> expose schedule in UI
-> support editing
-> add failure handling
```

over layer-by-layer work such as database, models, API, then frontend. Each slice should produce useful working behaviour where practical.

## Plan Lifecycle

The plan may change during implementation. When an assumption proves wrong, update the plan, record significant new decisions as ADRs, and keep the plan aligned with reality.

When implementation finishes:

1. Mark the plan `Completed` and add the completion date.
2. Move it to the Completed section of `plans/index.md`.
3. Update `concepts.md` if the domain changed.
4. Update `architecture.md` if the current architecture changed.
5. Ensure significant decisions have ADRs.

Completed plans remain historical context. Code, tests, concepts, and architecture describe the current system.

## Do Not

- implement code during planning
- invent requirements
- ask questions answerable from the repository
- introduce abstractions for hypothetical future needs
- create unnecessary ADRs
- describe planned architecture as current architecture
- finalise the plan while major ambiguity remains

Planning is complete when desired behaviour is clear, relevant code is understood, important edge cases and decisions are resolved, affected systems are known, and implementation can be divided into concrete vertical slices.
