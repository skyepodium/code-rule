# Dependency Rules

This directory defines standards for adopting packages and SDKs.

## Adoption Standards

- Do not add a new dependency when existing utilities or platform APIs can solve the problem.
- Before adding a dependency, check maintenance, license, bundle size, native requirements, and security issues.
- Put runtime imports in `dependencies`, and build/test/type-only packages in `devDependencies`.
- Use `workspace:*` for internal workspace packages when possible.

## Changes

- For major upgrades, check breaking changes and migration guides.
- Update lockfiles through pnpm commands; do not edit them manually.
- When adding a native dependency, document the iOS/Android build impact and installation steps.

## Removal

- Before removing an unused dependency, check imports and script usage.
- After removing a dependency, run lint, typecheck, test, and build.
