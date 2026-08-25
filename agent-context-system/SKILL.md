---
name: agent-context-system
description: Set up or maintain a lightweight .context knowledge system and root AGENTS.md for a codebase. Use when the user wants durable documentation of domain concepts, current architecture, architectural decisions, planned changes, or project-specific guidance.
---

# Agent Context System

Create and maintain a concise `.context/` system for knowledge that is expensive to reconstruct from code. Do not document facts that are obvious from the code or duplicate generic framework documentation.

## Structure

```text
.context/
  README.md
  concepts.md
  architecture.md
  decisions/
    index.md
    0001-example.md
  plans/
    index.md
    feature-name.md
  guidance.md
  skills/
```

Keep a root `AGENTS.md` that routes agents to `.context/`. Preserve and integrate useful existing instructions instead of replacing them.

## Documents

### `concepts.md`

Define important domain vocabulary, relationships, distinctions, and invariants. Exclude classes, controllers, services, and implementation details that are clear from code.

### `architecture.md`

Describe the current high-level architecture: major components, boundaries, data stores, background processing, external services, and important flows. Use Mermaid only when it materially improves understanding.

This file describes how the system works now. Keep planned architecture and historical reasoning elsewhere.

### `decisions/`

Create an ADR when a decision is difficult to reverse, establishes an important pattern, introduces significant infrastructure or dependencies, involves a meaningful tradeoff, or is likely to be questioned later.

Use:

```md
# 0001 — Decision title

**Status:** Accepted
**Date:** YYYY-MM-DD

## Context

Why the decision is needed.

## Options

Relevant alternatives.

## Decision

What was chosen.

## Consequences

Important tradeoffs.

## Revisit when

Conditions that may justify reconsidering it.
```

Maintain `decisions/index.md`:

```md
# Decisions

| # | Decision | Status | Summary |
|---|---|---|---|
| [0001](./0001-example.md) | Example | Accepted | Short summary. |
```

When a decision changes, create a new ADR and mark the previous one as superseded. Do not rewrite history.

### `plans/`

Plans describe meaningful features, refactors, migrations, or architectural work that benefits from planning before implementation. They are working documents and should evolve as the work changes.

A plan normally contains:

```md
# Feature Name

**Status:** Active

## Goal
## Current System
## Proposed Behaviour
## Design
## Implementation
## Edge Cases
## Decisions
## Acceptance Criteria
```

Maintain `plans/index.md`:

```md
# Plans

## Active

- [Feature name](./feature-name.md) — Short summary.

## Completed

- [Previous feature](./previous-feature.md) — Short summary.
```

When work finishes, mark the plan `Completed`, add the completion date, move it to the Completed index section, and reflect durable knowledge in concepts, architecture, or ADRs where needed. Completed plans are historical context, not the source of truth for current behaviour.

### `guidance.md`

Store project-specific development conventions such as architectural patterns, testing expectations, database and frontend conventions, dependency rules, and preferred patterns. Exclude generic framework guidance.

### Root `AGENTS.md`

Tell agents to read:

```text
.context/concepts.md
.context/architecture.md
.context/decisions/index.md
.context/plans/index.md
.context/guidance.md
```

Tell them to open relevant ADRs and active plans before changing affected areas.

## Initial Setup

1. Inspect the repository and existing documentation.
2. Identify core domain concepts and the current architecture.
3. Identify significant existing decisions whose reasoning can be established.
4. Identify meaningful work already in progress.
5. Create the `.context/` structure and concise documents based on evidence.
6. Add or update root `AGENTS.md`.

Do not invent historical reasoning. If the reason for an existing choice is unknown, say so. Do not write speculative architecture for a new project.

## Maintenance

After meaningful work, check:

```text
New or changed domain concept?  -> concepts.md
Current architecture changed?   -> architecture.md
Important decision made?        -> ADR + decisions/index.md
Planned work changed?            -> its plan
New project convention?         -> guidance.md
```

Ship documentation changes with the code changes that require them.

## Mental Model

```text
Concepts      -> WHAT things are
Architecture  -> HOW the system works now
Decisions     -> WHY it works that way
Plans         -> WHERE it is changing
Guidance      -> HOW we work
Skills        -> HOW agents perform workflows
Code          -> EXACT implementation
Tests         -> VERIFIED behaviour
```

Keep `.context/` small and useful.
