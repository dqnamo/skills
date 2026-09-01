---
name: barebones
description: Build exact, minimal implementations without product polish or extra scope. Use when the user wants a feature, app, screen, component, workflow, or prototype kept barebones, low-fidelity, narrowly scoped, or easy to redesign later. For frontend work, produce a single-paper wireframe UI with Drawably and restrained semantic ink colors instead of a polished visual design.
---

# Barebones

Implement exactly what was asked for and stop there. Every extra feature, abstraction, or UI flourish is out of scope unless explicitly requested or required for the implementation.

## Workflow

1. Identify the requested outcome in one sentence.
2. List the minimum pieces needed to satisfy it.
3. Fit the change into existing codebase patterns.
4. Implement only those pieces.
5. Run the narrowest useful validation: tests, typecheck, lint, or a quick manual check.
6. Report what changed and any validation results — no design suggestions.

Ask a clarifying question only when the ambiguity is real enough that guessing would produce the wrong feature.

## Frontend Outcome

Produce functional, semantic app UI that deliberately looks like a low-fidelity wireframe, not a finished product.

- Use native elements first: `form`, `label`, `input`, `button`, `select`, `textarea`, `table`, `ul`, `ol`, `section`, `nav`, `main`, `header`, `footer`.
- Use Drawably for supported controls in new frontend work. Read [references/drawably.md](references/drawably.md) before implementing that UI.
- Use one paper/background color across the page and every surface. Use black ink by default, blue for interaction, green for success, and red for errors or destructive actions.
- Do not create depth with alternate panel backgrounds, tinted sections, decorative colors, gradients, shadows, blur, glows, or elevation.
- Show hierarchy through spacing, grouping, labels, headings, dividers, and borders—not color or depth.
- CSS is allowed only for clear layout, usable sizing, and the single-paper wireframe contract. Avoid visual polish, responsive flourishes, broad design tokens, and styling systems.
- No icons, illustrations, decorative copy, or added animation. Keep Drawably static unless the user explicitly asks for motion.
- Keep text literal and task-focused — no marketing copy, empty states, or explanatory UI.
- Use the simplest state and data flow that works. Avoid context, reducers, global stores, and new dependencies unless the behavior requires them.
- When editing an already-styled component, preserve its styling unless the user asked to convert that surface to the barebones wireframe treatment.

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
