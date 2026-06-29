# Yulmoc - Coding Rules and Architecture Contract

This is the single-source rules document for senior-engineer-level standards. This document applies to all files under the repository root.

## Priority

1. The `AGENTS.md` closest to the current file
2. Root `AGENTS.md`
3. `docs/plan.md`
4. `DESIGN.md`
5. General practice

When rules conflict, follow the narrower-scope `AGENTS.md`. When changing rules, update the related documentation and examples together.

## Meta Rules

- If you find a rule violation and can safely fix it within the same task scope, fix it immediately.
- Do not mix unrelated cleanup into the same PR.
- Code modified by AI follows the same rules.
- When you introduce a new magic number or magic string, immediately move it to a domain constants file.
- If you determine that a rule is older than the code, first record the evidence, then update the rule.

## Language and Naming

- Write comments, PR titles, PR bodies, issue titles, and issue bodies in English.
- Write identifiers, filenames, type names, and function names in English.
- Avoid unnecessary abbreviations. For example, use `authentication` instead of `auth`, and `configuration` instead of `cfg`.
- Use `PascalCase` for classes, types, and React components.
- Use `camelCase` for functions, methods, variables, and parameters.
- Use `SCREAMING_SNAKE_CASE` for global immutable constants, and include units in the name when applicable, such as `_PX`, `_MS`, `_RATIO`, or `_COUNT`.
- Use `camelCase.ts` for regular TypeScript files and `PascalCase.tsx` for React component files.

## TypeScript Defaults

- `any` is forbidden. Accept external input as `unknown`, then use narrowing or schema validation before use.
- Function declarations are forbidden. Use arrow function expressions in the form `const functionName = (...) => {}`.
- Prefer `~/...` absolute paths for imports. Relative paths are allowed only within the same folder.
- New TypeScript projects must configure `tsconfig`, the bundler, and the test runner so they all resolve the same `~/...` alias.
- Prefer guard clauses and early returns over nested conditionals. Return quickly at the start of the function for failure, missing permission, missing data, platform exclusion, and similar cases.
- Treat caught values as `unknown` and use them only after `instanceof Error` or separate narrowing.
- Empty `catch` blocks are forbidden. Leave an English comment explaining the recovery strategy or logging intent.

## Structure and Entry Points

- Entry points are responsible only for bootstrap and wiring. Examples: `main.ts`, `index.tsx`, `App.tsx`, root provider, root router, native app delegate/activity.
- Do not put detailed business logic such as networking, storage, notifications, payments, authentication, or native bridge logic directly in entry points.
- When logic grows, split it into hooks, services, adapters, or pure utilities, and keep entry points as composition of meaningful function calls.
- Isolate side effects at service or adapter boundaries, and keep UI components focused on screen composition and user input wiring.

## Next.js Defaults

- Use App Router as the default routing model.
- Use server components by default, and place `"use client"` only on the smallest component that needs browser APIs or interaction.
- Do not mix the roles of `page.tsx`, `layout.tsx`, `loading.tsx`, `error.tsx`, and `route.ts`.
- Route handlers must also use arrow function expressions, such as `export const GET = async (...) => {}`, instead of function declarations.

## Packages and Tools

- Use pnpm as the only package manager.
- Do not introduce `package-lock.json`, `yarn.lock`, npm commands, or yarn commands.
- Apps and packages should specify the pnpm version in the `packageManager` field when possible.
- Use `pnpm add` to add dependencies and `pnpm add -D` to add development dependencies.
- Before a PR, pass `pnpm lint` and `pnpm typecheck` by default, and also `pnpm test` and `pnpm build` when needed.

## UI className

- Use `classnames` for conditional `className` composition.
- Do not compose conditional class strings directly with `+`, template literals, or array `join`.
- Inline static class strings are allowed. If a condition is involved, use `classNames(...)`.

## Magic Numbers and Constants

- Inline numbers and domain strings are forbidden by default.
- Put constants by domain under `src/shared/constants/<domain>.ts`.
- When three or more constants are strongly related, group them into a feature-level object and make it immutable with `Object.freeze` or `as const`.
- Call sites must expose meaning clearly, such as `VIEWPORT_TOOLTIP.OFFSET_X_PX`.

## Design Tokens

- Manage colors, spacing, radius, typography, elevation, opacity, and component dimensions as design tokens.
- Do not declare visual values such as hex colors, `rgba(...)`, font size, spacing, radius, or opacity directly in UI components.
- Put tokens in `src/shared/design/tokens.ts` or a platform-specific design token boundary.
- Do not mix product/domain constants with design tokens. For example, a polling interval belongs in constants, while a button radius belongs in design tokens.

## PR Rules

- The target branch for PRs is `develop`.
- PR bodies must include a `## Participants` section and list the participating AI agents.
- Write PR intent, verification results, and remaining risks in English.
