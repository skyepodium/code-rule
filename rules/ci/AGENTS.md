# CI Rules

This directory defines CI job, cache, and verification order rules.

## Default Jobs

- CI uses lockfile-based installation.
- The default verification order is install, lint, typecheck, test, and build.
- Do not bypass failed jobs; fix the cause.

## pnpm

- Use the pnpm store cache, but ensure it invalidates accurately when the lockfile changes.
- CI command examples must use pnpm only.
- Workspaces must not break the root-level contract even when using change-scope-based jobs.

## Artifacts

- Store build artifacts, coverage, and test reports only in jobs that need them.
- Ensure secrets are not included in artifacts.
