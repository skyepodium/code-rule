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
- Optimize for readability at the call site. Names, branches, and constants should make intent clear without requiring readers to inspect implementation details.
- Optimize for code that can be changed safely by someone who did not write it.

## Core Engineering Principles

- Keep modules independent. A module should have one reason to change, a small public interface, and dependencies that are visible from its imports and constructor/function parameters.
- Separate layers strictly. Controllers/routes handle protocol and request/response mapping, services own business use cases, repositories own persistence queries, and adapters wrap external systems.
- Dependencies flow inward and downward only. UI/controllers may call services, services may call repositories/adapters, repositories may call storage/database clients, but lower layers must not import higher layers.
- Reuse only across stable boundaries. Do not extract shared code only because two call sites look similar; extract when the domain contract is stable or a third use proves the abstraction.
- Make data ownership explicit. Each piece of state must have one owner: server cache, URL/route, form, local view state, or global app state. Avoid duplicate sources of truth.
- Make lifecycle ownership explicit. Code that creates listeners, timers, subscriptions, caches, object URLs, native handles, or async work must also define cleanup, cancellation, or reset behavior.
- Treat memory growth as a correctness concern. Caches need limits or TTL, long-lived collections need deletion paths, and large objects should not be retained beyond their useful lifecycle.
- Keep complexity within a reviewable budget. If a function needs many branches, many parameters, or deep nesting, split it into named helpers, smaller use cases, or separate modules before adding more logic.

## Language and Naming

- Write comments, PR titles, PR bodies, issue titles, and issue bodies in English.
- Write identifiers, filenames, type names, and function names in English.
- Unnecessary abbreviated variable names, function names, and type names are forbidden. For example, use `authentication` instead of `auth`, `configuration` instead of `cfg`, `properties` instead of `props` outside React conventions, and `request` instead of `req` unless a framework contract requires the shorter name.
- Short names such as `i`, `j`, `x`, `y`, `data`, `item`, `temp`, and `value` are allowed only when their meaning is obvious from a tiny local scope. Otherwise, use a domain-specific name.
- Use `PascalCase` for classes, types, and React components.
- Use `camelCase` for functions, methods, variables, and parameters.
- Use `SCREAMING_SNAKE_CASE` for global immutable constants, and include units in the name when applicable, such as `_PX`, `_MS`, `_RATIO`, or `_COUNT`.
- Use `camelCase.ts` for regular TypeScript files and `PascalCase.tsx` for React component files.

## TypeScript Defaults

- `any` is forbidden. Accept external input as `unknown`, then use narrowing or schema validation before use.
- Function declarations are forbidden. Use arrow function expressions in the form `const functionName = (...) => {}`.
- Prefer `~/...` absolute paths for imports. Relative paths are allowed only within the same folder.
- New TypeScript projects must configure `tsconfig`, the bundler, and the test runner so they all resolve the same `~/...` alias.
- Use guard clauses and early returns aggressively. Return quickly at the start of the function for failure, missing permission, missing data, platform exclusion, disabled/no-op cases, and invalid input. Avoid nested conditionals when the branch can be expressed as an early exit.
- Treat caught values as `unknown` and use them only after `instanceof Error` or separate narrowing.
- Empty `catch` blocks are forbidden. Leave an English comment explaining the recovery strategy or logging intent.

## Structure and Entry Points

- Entry points are responsible only for bootstrap and wiring. Examples: `main.ts`, `index.tsx`, `App.tsx`, root provider, root router, native app delegate/activity.
- Do not put detailed business logic such as networking, storage, notifications, payments, authentication, or native bridge logic directly in entry points.
- When logic grows, split it into hooks, services, adapters, or pure utilities, and keep entry points as composition of meaningful function calls.
- Isolate side effects at service or adapter boundaries, and keep UI components focused on screen composition and user input wiring.
- Use controller/service/repository-style separation where it fits the platform. Protocol handlers and UI event handlers should delegate business decisions to services instead of reaching into storage, SDKs, or raw APIs directly.

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
- One-off computed values should still be assigned to named local variables when the name explains intent better than the expression alone.
- Put constants by domain under `src/shared/constants/<domain>.ts`.
- Use domain constants aggressively for repeated values, externally meaningful values, timing, sizing, limits, keys, routes, events, statuses, and configuration defaults.
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
