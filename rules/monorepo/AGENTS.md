# Monorepo Rules

This directory defines workspace, package boundary, and internal import rules.

## Workspace

- Specify workspace scope in `pnpm-workspace.yaml`.
- Make package names, ownership, and publish/private status clear.
- Distinguish root dependencies from package dependencies.

## Package Boundaries

- Do not deep import internal files from other packages.
- Import through public entry points.
- Shared packages must not import app implementation details.
- If a circular dependency appears, move common types/utilities to a lower-level package.

## Scripts

- Root scripts own the contract for the whole workspace.
- Package scripts must be independently executable within that package.
- Specify generated output locations and commit policy per package.
