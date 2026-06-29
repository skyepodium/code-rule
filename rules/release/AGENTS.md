# Release Rules

This directory defines versioning, changelog, artifact, and rollout rules.

## Versioning

- Match version bump criteria to the project's release policy.
- Apps track versionName/versionCode or build number changes.
- Packages record public API changes and semver impact.

## Changelog

- Record user-impacting changes in the changelog or release notes.
- Include migration notes for breaking changes.
- Do not exaggerate user-facing wording when a change is only an internal refactor.

## Rollout

- Document release artifact creation commands and verification commands.
- Specify staged rollout, rollback, and hotfix criteria.
- Check lint, typecheck, test, and build evidence before deployment.
