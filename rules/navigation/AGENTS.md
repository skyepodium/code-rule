# Navigation Rules

This directory defines route, navigation params, and deep link rules.

## Routes

- Constantize route paths/names.
- Explicitly type route params.
- Screen components must split params parsing into adapters/helpers.
- Optional params must handle fallbacks and invalid states.

## Navigation

- Use the project's standard navigation API for internal navigation.
- Distinguish the meaning of push, replace, back, and reset.
- Collect authentication guards, permission guards, and onboarding guards in one boundary.

## Deep Links

- Document deep link schemas and route mapping.
- Send unknown deep links to a safe fallback.
- Before opening external URLs, validate them with an allowlist or scheme check.
