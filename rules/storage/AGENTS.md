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
