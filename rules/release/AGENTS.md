# Release Rules

This directory defines versioning, changelog, artifact, and rollout rules.

## Versioning

- Match version bump criteria to the project's release policy.
- Apps track versionName/versionCode or build number changes.
- Packages record public API changes and semver impact.
- Define one version source of truth and derive bundle metadata, filenames, documentation, update feeds, checksums, and workflow inputs from it. Do not scatter a future release number across scripts and code.

## Changelog

- Record user-impacting changes in the changelog or release notes.
- Include migration notes for breaking changes.
- Do not exaggerate user-facing wording when a change is only an internal refactor.

## Rollout

- Document release artifact creation commands and verification commands.
- Specify staged rollout, rollback, and hotfix criteria.
- Check lint, typecheck, test, and build evidence before deployment.
- Build releases in an isolated or freshly cleaned output directory so stale artifacts cannot be signed or uploaded as the current version.
- Verify the final distributable, not only the staging directory. Mount or unpack it, copy the application/package outside the repository and build tree, and validate the layout from that isolated copy.
- A native release gate should verify version metadata, required resources and frameworks, loadability of native libraries or plugins, supported architectures, signatures, notarization or platform trust where applicable, and an app-owned headless smoke test.
- Publication must be ordered after artifact verification. A failed structure, smoke, signature, architecture, checksum, notarization, or update-feed check must make upload or rollout impossible.
- After publication, download the public assets and re-run checksum, signature/trust, package-layout, and update-metadata checks against what users actually receive.
