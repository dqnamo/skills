---
name: greenfield
description: Use when working on a new app or feature where backwards compatibility is not required. Existing code does not need to be preserved for legacy users, but changes should stay scoped to the user's request.
---
# Greenfield

No backwards-compatibility requirements unless explicitly stated. Implement things cleanly and completely.

- **Stay scoped.** Make the requested change well — don't rewrite unrelated code just because it could be cleaner.
- **Delete freely.** Remove or replace existing code when it's in the way, and clean up any dead code left behind.
- **Wire it up fully.** Update callers, tests, types, routes, and configs so the change works end to end.
- **No legacy scaffolding.** Skip compatibility shims, migration paths, feature flags, and dual implementations unless asked.
- **Preserve the unrelated.** Don't touch user data, secrets, env files, or work outside the scope of the request.
