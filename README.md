# code-rule

`code-rule` is a portable engineering rulebook for projects that use AI coding agents, TypeScript, React, Next.js, React Native, and pnpm.

It is meant to be copied into real projects as `AGENTS.md` guidance, not read as a directory catalog. The goal is to make every project start with clear defaults for architecture, naming, type safety, testing, package management, UI tokens, review discipline, and release hygiene.

## What This Gives a Project

- A root engineering contract that defines the default coding style and architecture boundaries.
- Optional rule packs for specific stacks such as TypeScript, React, Next.js, React Native, Expo, Tailwind, Storybook, Android, and iOS.
- Operational rules for testing, linting, CI, dependency decisions, release process, documentation, security, storage, logging, and performance.
- Clear priority behavior: broad rules live at the project root, and narrower `AGENTS.md` files override them closer to the code they govern.

## Recommended Setup

Start with the root rulebook:

```text
AGENTS.md
```

Then add scoped rule packs only where they apply. A typical web app setup uses:

```text
AGENTS.md
rules/typescript/AGENTS.md
rules/react/AGENTS.md
rules/next/AGENTS.md
rules/pnpm/AGENTS.md
rules/testing/AGENTS.md
rules/eslint/AGENTS.md
rules/classnames/AGENTS.md
rules/constants/AGENTS.md
rules/design-tokens/AGENTS.md
rules/security-privacy/AGENTS.md
rules/review/AGENTS.md
```

A React Native or Expo app usually adds the mobile-specific packs:

```text
rules/react-native/AGENTS.md
rules/expo/AGENTS.md
rules/android/AGENTS.md
rules/ios/AGENTS.md
rules/navigation/AGENTS.md
rules/storage/AGENTS.md
rules/accessibility/AGENTS.md
rules/responsive-layout/AGENTS.md
```

A monorepo usually adds:

```text
rules/monorepo/AGENTS.md
rules/dependencies/AGENTS.md
rules/ci/AGENTS.md
rules/release/AGENTS.md
```

## How to Apply It

1. Copy the root `AGENTS.md` into the target project root.
2. Copy the stack-specific rule packs into the directories where they should apply.
3. Keep broad rules near the root and specialized rules near the relevant code.
4. Merge overlapping rules only when the target project needs a single consolidated `AGENTS.md`.
5. When project reality differs from a rule, update the rule and the code together so the contract stays current.

Example layout:

```text
my-app/
  AGENTS.md
  app/
    AGENTS.md
  src/
    AGENTS.md
  src/components/
    AGENTS.md
  ios/
    AGENTS.md
  android/
    AGENTS.md
```

## Rule Philosophy

The rules are intentionally opinionated:

- Prefer explicit boundaries over clever coupling.
- Prefer strict layer separation over convenient cross-layer imports.
- Prefer `unknown` plus validation over `any`.
- Prefer arrow function expressions over function declarations.
- Prefer pnpm-only workflows over mixed package manager usage.
- Prefer constants and design tokens over inline magic values.
- Prefer services, adapters, hooks, and pure utilities over bloated entry points.
- Prefer tests and verification evidence before claiming completion.
- Prefer lifecycle ownership, bounded memory use, and clear cleanup paths over implicit long-lived state.

These defaults are designed to reduce ambiguous code review debates and give AI agents the same baseline a senior engineer would enforce manually.

## Maintenance

Treat these files as living project contracts. If a rule no longer matches how a project should work, do not ignore it silently. Update the rule, update examples if needed, and keep the project-specific `AGENTS.md` files aligned with the codebase.
