# Documentation Rules

This directory defines README, ADR, runbook, and development documentation rules.

## README

- README files must include installation, execution, verification, environment variables, and the main structure.
- Command examples must follow the project's package manager.
- Do not leave stale template text or unused commands.

## Design Documents

- Record important architecture decisions with intent, alternatives, decision, and impact.
- Specify temporary constraints and removal conditions.
- If documentation diverges from code, update it in the same change.

## Operations Documents

- Deployment, rollback, migration, and incident response procedures must include executable commands and verification methods.
- Do not write sensitive secret values directly in documentation.
