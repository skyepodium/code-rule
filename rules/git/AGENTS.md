# Git Rules

This directory defines branch, commit, and history hygiene rules.

## Branches

- The default PR target branch follows the root rules or project rules.
- Name work branches so they reveal the intent of the feature, fix, or documentation work.
- Do not mix unrelated changes into the same commit/PR.

## Commits

- Write commit messages that reveal the intent of the change.
- Commit generated files, lockfiles, and migrations together with the related source changes.
- Do not commit failed experiments, temporary logs, or commented-out code.

## Safety

- Do not run `git reset --hard`, `git checkout --`, or force push without an explicit request.
- Do not revert changes made by someone else.
- When resolving conflicts, leave the rationale for which side was chosen.
