---
name: barebones
description: Build exact, minimal implementations without product polish or extra scope. Use when the user wants to build a feature, app, screen, component, workflow, or prototype but explicitly wants the result kept barebones, unstyled, narrowly scoped, or ready for the user to design manually later. Especially use for frontend work where new CSS, classes, styling systems, decorative UI, layout polish, animations, icons, marketing copy, or unsolicited features should be avoided.
---

# Barebones

Implement exactly what was asked for and stop there. Every extra feature, abstraction, UI flourish, or dependency is out of scope unless explicitly requested or the codebase requires it.

## Workflow

1. Identify the requested outcome in one sentence.
2. List the minimum pieces needed to satisfy it.
3. Fit the change into existing codebase patterns.
4. Implement only those pieces.
5. Run the narrowest useful validation: tests, typecheck, lint, or a quick manual check.
6. Report what changed and any validation results — no design suggestions.

Ask a clarifying question only when the ambiguity is real enough that guessing would produce the wrong feature.

## Frontend Rules

Produce functional, semantic, unstyled markup by default.

- Use native elements first: `form`, `label`, `input`, `button`, `select`, `textarea`, `table`, `ul`, `ol`, `section`, `nav`, `main`, `header`, `footer`.
- No new CSS, Tailwind classes, inline styles, styled components, animations, icons, or layout polish.
- No `class`, `className`, or `style` attributes unless the user asks for styling or an existing framework requires it for functionality.
- Keep text literal and task-focused — no marketing copy, empty states, or explanatory UI.
- Use the simplest state and data flow that works. Avoid context, reducers, global stores, and new dependencies unless the behavior requires them.
- When editing an already-styled component, preserve existing styling without expanding it.

## Scope Control

Before adding anything, ask: "Did the user explicitly request this, or is it required for the feature to work?" If no, leave it out.

Common things to skip unless asked: additional pages, routes, auth flows, analytics, notifications, seed data, refactors outside the touched path, reusable component libraries, responsive design, and "nice to have" error handling.

## Code Quality

Barebones means minimal scope, not sloppy code.

- Readable, idiomatic, easy to inspect and manually edit later.
- Straightforward control flow over cleverness or premature abstraction.
- Use existing helpers, conventions, and data access patterns.
- Plain, domain-specific names. Small files and functions.
- Add tests when behavior is non-trivial, shared, or likely to regress.
