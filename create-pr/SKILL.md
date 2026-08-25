---
name: create-pr
description: Prepare and create a pull request for completed work, including validation evidence, deployment impact, post-deploy actions, verification, and rollback notes. Use when the user asks to open or create a PR, not merely to review local changes.
---

# Create PR

Turn the current completed change into a reviewable pull request with an accurate operational handoff. Creating the PR authorizes the normal branch push and PR creation needed for this repository, but not merging, deploying, or performing post-deploy actions.

## 1. Inspect the Change

Read repository instructions and relevant `.context/` documents. Inspect:

- current branch and base branch
- working tree, staged changes, and commits
- complete diff against the intended base
- related plan and ADRs
- repository PR template and contribution rules

Do not include unrelated user changes. If the change cannot be separated safely, stop and ask the user.

## 2. Check Readiness

Before creating the PR:

1. Confirm the implementation matches the plan or stated request.
2. Confirm relevant context documents were updated.
3. Run the narrowest sufficient tests, type checks, linting, builds, or manual checks.
4. Review for debug code, secrets, generated noise, accidental files, and risky destructive changes.
5. Confirm commits and branch naming meet repository conventions.

Fix small in-scope readiness issues. Ask before making a meaningful product or scope change. Never claim a check ran when it did not.

## 3. Identify Deployment Work

Inspect the diff and plan for operational actions, including:

- database migrations, backfills, or data repair
- environment variables, secrets, or configuration
- feature flags and rollout order
- queues, scheduled jobs, workers, or one-off commands
- caches, indexes, search reindexing, or asset generation
- third-party setup, webhooks, permissions, or credentials
- monitoring, dashboards, alerts, and manual verification
- compatibility requirements during rolling deployment

Separate actions into:

- **Before deploy**
- **During deploy**
- **After deploy**
- **Verification**
- **Rollback**

For each real action, state when it happens, what must be done, and how success is verified. Include exact commands only when they are established by the repository or implementation. Do not invent operational steps.

If no special action is required, say `None` explicitly.

## 4. Prepare the PR

Follow the repository's template. Otherwise use:

```md
## Summary

- What changed and why.

## Implementation

- Important design details and affected areas.

## Testing

- Checks run and their results.

## Deployment

### Before deploy

- None.

### During deploy

- None.

### After deploy

- None.

### Verification

- Observable checks that confirm the change works.

### Rollback

- How to disable or reverse the change safely.

## Context

- Plan and ADR links, when applicable.
```

Keep the title concise and outcome-focused. The body should explain the change without repeating the entire diff.

Use checkboxes only for actions someone must perform. Leave future actions unchecked; mark completed checks accurately.

## 5. Create the PR

1. Ensure the work is on an appropriate non-protected branch.
2. Commit only intended changes when uncommitted work belongs to this task.
3. Push the branch.
4. Create the PR against the correct base using the prepared title and body.
5. Return the PR link.

If authentication, permissions, branch protection, or remote configuration blocks creation, stop after preserving the prepared PR content and report the exact blocker. Do not retry repeatedly or change repository access settings.

## Handoff

Report:

- PR link
- checks run
- deployment or post-deploy actions
- anything blocked or intentionally excluded

Do not merge, deploy, change production configuration, run migrations, or complete post-deploy actions unless the user separately asks.
