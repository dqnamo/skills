---
name: next-start
description: Use when the user wants to scaffold a fresh Next.js app with current create-next-app defaults, Tailwind CSS, Inter and JetBrains Mono fonts, a cn classname helper, all Radix color CSS variables exposed to Tailwind theme tokens with grayscale and accent aliases, Base UI installed, and Biome formatting configured.
---

# Next Start

Scaffold a fresh Next.js app with the preferred baseline. Keep it current by using `create-next-app@latest`, then inspect generated files before editing because CLI defaults change.

## Workflow

1. Inspect the target directory first. Preserve unrelated files and avoid overwriting meaningful work.
2. Scaffold with the user's package manager if specified; otherwise prefer `pnpm`:
   ```bash
   pnpm create next-app@latest <app-name> --yes
   ```
3. Install runtime dependencies:
   ```bash
   pnpm add clsx tailwind-merge @radix-ui/colors @base-ui/react
   ```
4. Install Biome:
   ```bash
   pnpm add -D @biomejs/biome
   ```
5. Add `helpers/classname-helper.ts` under `src/` if the app uses `src/`; otherwise add it at the app root:
   ```ts
   import { type ClassValue, clsx } from "clsx";
   import { twMerge } from "tailwind-merge";

   export function cn(...inputs: ClassValue[]) {
     return twMerge(clsx(inputs));
   }
   ```
6. Configure fonts in `app/layout.tsx` or `src/app/layout.tsx` with `next/font/google`:
   - Sans: `Inter`, variable `--font-inter`
   - Mono: `JetBrains_Mono`, variable `--font-jetbrains-mono`
   - Apply both variables to the root `<html>` className.
   - Add `bg-grayscale-1` to the `<body>` className, preserving any existing body classes.
7. Create `app/colors.css` or `src/app/colors.css` for Radix imports and Tailwind color tokens.
8. Keep `globals.css` lean:
   ```css
   @import "tailwindcss";
   @import "./colors.css";

   @theme inline {
     --font-sans: var(--font-inter), ui-sans-serif, system-ui, sans-serif;
     --font-mono: var(--font-jetbrains-mono), ui-monospace, monospace;
     --text-tiny: 11px;
   }

   .root {
     isolation: isolate;
   }

   body {
     position: relative;
   }
   ```
9. Add Biome scripts without deleting useful existing scripts:
   - `format`: `biome format --write .`
   - `check`: `biome check --write .`
10. Add `biome.json` with simple 2-space formatting unless the repo already has a stronger convention.
11. Run install and non-server validation only. Do not run `dev`, `next dev`, or any dev server unless the user explicitly asks.

## Radix Colors

Use `app/colors.css` instead of `src/app/colors.css` when the app does not use `src/`.

The app's `colors.css` must:

- Import every Radix CSS file needed from `@radix-ui/colors`, including light and dark variants.
- Expose the Radix CSS variables as Tailwind v4 `@theme inline` color tokens.
- Add `--color-grayscale-1` through `--color-grayscale-12` from the chosen grayscale scale.
- Add `--color-accent-1` through `--color-accent-12` from the chosen accent scale.

Default aliases:

- Grayscale: `gray`
- Accent: `blue`

If the user asks for a different grayscale or accent, update the imports and aliases to use those Radix scale names.

## Biome

Use this minimal config when no repo-specific config exists:

```json
{
  "formatter": {
    "enabled": true,
    "indentStyle": "space",
    "indentWidth": 2
  },
  "organizeImports": {
    "enabled": true
  },
  "linter": {
    "enabled": true,
    "rules": {
      "recommended": true
    }
  }
}
```

## Validation

Run the narrowest useful checks:

- `pnpm install` if dependencies were changed and install did not already run.
- `pnpm check`
- `pnpm build` when time and dependencies allow.

Never run a dev server unless explicitly requested.
