# Review Rules

This directory defines self-review, PR review, and review response rules.

## Self-Review

- Before a PR, read the diff directly and remove unintended file changes.
- Separately check public API, migration, config, permission, and dependency changes.
- If you find a new rule violation, fix it within the same task scope.

## PR Content

- Include implementation intent, main changes, verification results, and remaining risks.
- Attach evidence for UI changes that require screenshots or video.
- If AI participated, follow the root PR rule's participants section.

## Review Response

- Technically verify review comments before accepting them as-is.
- Leave brief rationale for feedback that is not applied.
- After fixes, rerun the related tests or verification commands.
