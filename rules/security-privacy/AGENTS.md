# Security and Privacy Rules

This directory defines secret, permission, privacy, and external SDK rules.

## Secrets

- Do not commit secrets, tokens, private keys, or service account JSON.
- Put placeholders instead of real values in `.env.example`.
- Distinguish public env prefixes from private env prefixes.
- If a secret is exposed, state that rotation is needed separately from code changes.

## Privacy

- Do not leave raw PII in logs, analytics, or crash reports.
- Pass user identifiers only within the necessary scope, and define masking/hash policies.
- Permission request text must explain the required feature and usage purpose.

## External SDKs

- Before adding an external SDK, check collected data, permissions, network endpoints, and license.
- Review opt-in/consent requirements for tracking, ads, and analytics SDKs.
- Security-related logic must not rely on client-only validation.
