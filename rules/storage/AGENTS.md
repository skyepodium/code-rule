# Storage Rules

This directory defines local storage, secure storage, and cache storage rules.

## Keys and Schemas

- Manage storage keys as domain constants.
- Stored values must have a version or schema.
- Treat values as external input when reading, validate from `unknown`, then convert them to domain types.
- When parsing fails, specify one strategy: fallback, migration, or deletion.

## Sensitive Information

- Do not store access tokens, refresh tokens, or personal identifiers in regular storage.
- Use platform-secure storage such as secure storage, keychain, or keystore for sensitive information.
- Do not leave raw storage values in logs or analytics.

## Lifecycle

- Caches must have TTL, invalidation, and reset criteria.
- Specify keys that must be cleared on logout, account switching, or workspace switching.
- Do not create global storage wrappers that are hard to initialize in tests.
- UI-thread or main-actor stores must not perform filesystem existence checks, directory creation, raw reads, or raw writes directly. Delegate disk IO to a persistence adapter, worker, queue, repository, or async boundary that can be tested separately.
- Keep synchronous compatibility APIs thin. If a synchronous public API must remain, isolate the blocking work behind a named persistence boundary and document why the call is safe for that lifecycle.
