# Drawably Wireframes

Use [Drawably](https://www.drawably.dev/) as the small visual layer for barebones frontend work. It keeps real HTML controls in the DOM and draws the rough chrome with SVG.

## Setup

- Install `drawably` only when the project can accept an npm dependency. If dependencies are explicitly forbidden or the platform is unsupported, keep native controls and apply only minimal wireframe layout CSS.
- Import `drawably/style.css` once.
- In React, use the components from `drawably/react`. In vanilla JavaScript, use the matching attach functions from `drawably`.
- Drawably has React wrappers and vanilla functions, but no Vue or Svelte adapters. Use the vanilla functions from the framework's client lifecycle when that is straightforward; otherwise retain native controls.

Supported controls include buttons, checkbox/radio wrappers, toggles, input/textarea/select wrappers, dividers, cards, badges, and lists. Use only the controls the requested interface needs.

## Barebones Defaults

Use one paper color and four restrained ink colors:

```css
:root {
  --wire-ink: #111;
  --wire-action: #2457d6;
  --wire-success: #188a42;
  --wire-danger: #d12724;
  --wire-paper: #fff;

  --drawably-stroke: var(--wire-ink);
  --drawably-fill: var(--wire-ink);
  --drawably-paper: var(--wire-paper);
  --drawably-error: var(--wire-danger);
  --drawably-success: var(--wire-success);
}
```

- Use black for structure, text, borders, and ordinary controls.
- Use blue only for links, focus, selection, and primary actions.
- Use green only for success or completion.
- Use red only for errors, warnings that require action, or destructive controls.
- Color must communicate state or interaction. Never use these inks to distinguish page regions, decorate content, or imply surface depth.
- Pass `boil={0}` in React or `boil: 0` to vanilla attach functions. Motion is product polish, not part of the default wireframe.
- Prefer outline buttons. Use solid or scribble variants only when the requested behavior needs a visibly primary action.
- Drawably's `state="success"`, `state="error"`, and `tone="danger"` are appropriate for their matching semantic meanings. Avoid `tone="neutral"`, which introduces an unnecessary warm grey.
- Do not use highlights, circles, arrows, optional pen fonts, or custom rough shapes unless the user explicitly asks for annotation or decoration.
- Do not fake Drawably controls with CSS borders. Attach Drawably to the real semantic control and retain labels, keyboard behavior, forms, and accessibility.
- Do not restyle Drawably's SVG paths directly. Theme through its CSS custom properties.

Use ordinary structural CSS for layout, but keep every header, sidebar, panel, card, and content area on the same paper color. A bordered box is acceptable when grouping is needed; a differently colored surface is not. Do not tint a panel blue, green, or red—the semantic ink belongs on the relevant control, label, or status mark only.
