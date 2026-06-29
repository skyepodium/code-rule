# pnpm Rules

This directory defines pnpm-based package management rules. In target projects, place it at the root or workspace root.

## Package Manager

- Use pnpm as the only package manager.
- Forbid `npm install`, `npm run`, `npx`, `yarn`, and `bun install`.
- Do not create `package-lock.json`, `yarn.lock`, or `bun.lockb`.
- `pnpm-lock.yaml` is committed.
- Apps and packages with `package.json` should specify `"packageManager": "pnpm@<version>"` when possible.

## Commands

- Use `pnpm add <package>` to add dependencies.
- Use `pnpm add -D <package>` to add development dependencies.
- Use `pnpm exec <command>` or `pnpm dlx <package>` for one-off execution.
- CI installation must use a command that pins the lockfile.
- README, docs, CI, and script examples must use pnpm commands only.

## Script Contract

- Use `lint`, `typecheck`, `test`, `build`, and `format` as default script names.
- Next apps must support at least `pnpm lint`, `pnpm typecheck`, and `pnpm build`.
- Scripts must not depend on OS-specific shell features.
- If a script becomes long, split it into a separate TypeScript or JavaScript script file.

## Workspace

- Monorepos specify workspace scope with `pnpm-workspace.yaml`.
- Use the `workspace:*` protocol for internal workspace package references when possible.
- Before adding dependencies to the root, first confirm they are actually needed at the root.
- App-only dependencies belong in that app package.

## Dependency Standards

- Packages imported by runtime code belong in `dependencies`.
- Build-, test-, type-, and lint-only packages belong in `devDependencies`.
- Add new dependencies only when existing utilities cannot solve the problem.
- Resolve version conflicts with pnpm commands instead of manually editing the lockfile.
